---
layout: default
title: Scale aws RDS
parent: Kubernetes
grand_parent: Spring Boot
nav_order: 3
---
# Scale aws RDS
You can scale an `Amazon RDS` instance depending on the number of connections by using Amazon `CloudWatch Alarms` and Amazon RDS `Auto Scaling`. Here's how to set it up:

* Create a `CloudWatch Alarm` to monitor the number of connections: In the `CloudWatch` console, create an alarm that triggers when the number of connections to the `RDS` instance exceeds a specified threshold.

* Create an RDS `Auto Scaling policy`: In the RDS console, create an RDS `Auto Scaling` policy that specifies the desired minimum and maximum capacity for the RDS instance.

* Link the `CloudWatch` Alarm and RDS Auto Scaling policy: In the RDS Auto Scaling policy, link the CloudWatch Alarm to the RDS Auto Scaling policy.

* Monitor the RDS instance: In the `CloudWatch` console, monitor the number of connections to the RDS instance. When the number of connections exceeds the threshold, the `CloudWatch` Alarm triggers and the RDS `Auto Scaling policy`222222222 scales the RDS instance up or down to meet the desired capacity.

By using this setup, you can ensure that your RDS instance can handle an increase in the number of connections, without any downtime or disruption to your application.


Here's an example of how you can write a Terraform script to scale an Amazon RDS instance depending on the number of connections:
```yml
provider "aws" {
  region = "us-west-2"
}

module "rds_instance" {
  source = "terraform-aws-modules/rds/aws"
  version = "5.6.0"

  identifier = "mydb"
  engine     = "postgres"
  size       = "db.t2.micro"

  max_capacity = 5
  min_capacity = 1

  alarm_actions = [module.scale_policy.arn]

  vpc_security_group_ids = [aws_security_group.rds.id]
}

module "scale_policy" {
  source = "terraform-aws-modules/appautoscaling/aws"
  version = "4.0.0"

  name                 = "rds-instance-scale-policy"
  policy_type          = "TargetTrackingScaling"
  service_namespace    = "rds"
  resource_id          = aws_db_instance.rds.id
  scalable_dimension    = "rds:dbInstance:ReadReplicaCount"
  target_tracking_config = {
    target_value = 1000
    predefined_metric_specification = {
      predefined_metric_type = "RDSReaderAverageConnections"
    }
  }
}

resource "aws_security_group" "rds" {
  name        = "rds-security-group"
  description = "Allow all inbound traffic"

  ingress {
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```
This Terraform script creates an Amazon RDS instance and sets up the necessary scaling policy using the AWS Application Auto Scaling module. The `rds_instance` module sets the minimum and maximum capacity for the RDS instance, and links the scaling policy to the `CloudWatch` Alarm using the `alarm_actions` argument. The `scale_policy` module creates the scaling policy and sets the target value for the number of connections. The Terraform script also creates a security group that allows all inbound traffic to the RDS instance.



