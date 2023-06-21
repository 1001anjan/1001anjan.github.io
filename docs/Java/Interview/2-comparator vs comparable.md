---
layout: default
title: Java Comparator vs Comparable  
parent: Interview Preparation
grand_parent: Java
nav_order: 2
---
# Comparator vs Comparable in java
In Java, both Comparator and Comparable are interfaces used for sorting and ordering objects, but they serve different purposes.

### Comparable interface:
* The Comparable interface is implemented by a class whose instances can be sorted.
* It defines a single method called compareTo(), which compares the object with another object of the same type.
* The compareTo() method returns a negative integer, zero, or a positive integer based on whether the current object is less than, equal to, or greater than the other object, respectively.
* By implementing Comparable, you enable the natural ordering of instances of your class.
* Example usage: Sorting a list of strings in alphabetical order using Collections.sort().

#### Comparator interface:
* The Comparator interface is used to define custom comparison logic separate from the objects being compared.
* It defines two methods: compare() and equals().
* The compare() method compares two objects and returns a negative integer, zero, or a positive integer based on the comparison.
* By using Comparator, you can sort objects based on different criteria or multiple fields.
* Comparator implementations can be passed to sorting methods like Collections.sort() or Arrays.sort() as an additional argument.

* Example usage: Sorting a list of custom objects based on a specific field or a combination of fields.
To summarize, Comparable is used for natural ordering and is implemented by the class whose instances need to be sorted. On the other hand, Comparator is used for custom ordering and can be implemented separately from the class being sorted.

````java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Employee implements Comparable<Employee> {
    private String name;
    private int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public int compareTo(Employee other) {
        return this.name.compareTo(other.name);
    }

    @Override
    public String toString() {
        return "Employee [name=" + name + ", age=" + age + "]";
    }
}

class AgeComparator implements Comparator<Employee> {
    @Override
    public int compare(Employee emp1, Employee emp2) {
        return emp1.getAge() - emp2.getAge();
    }
}

public class SortingExample {
    public static void main(String[] args) {
        List<Employee> employeeList = new ArrayList<>();
        employeeList.add(new Employee("John", 30));
        employeeList.add(new Employee("Alice", 25));
        employeeList.add(new Employee("Bob", 35));

        // Sort using Comparable (natural ordering)
        System.out.println("Sorted by name (Comparable):");
        Collections.sort(employeeList);
        for (Employee emp : employeeList) {
            System.out.println(emp);
        }

        // Sort using Comparator (custom ordering)
        System.out.println("\nSorted by age (Comparator):");
        Comparator<Employee> ageComparator = new AgeComparator();
        Collections.sort(employeeList, ageComparator);
        for (Employee emp : employeeList) {
            System.out.println(emp);
        }
    }
}
````
