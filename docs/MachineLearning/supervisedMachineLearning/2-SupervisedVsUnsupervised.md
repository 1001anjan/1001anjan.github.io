---
layout: default
title: Supervised Vs Unsupervised
parent: Supervised Machine Learning
grand_parent: Machine Learning
nav_order: 2
---
# Supervised Vs Unsupervised Machine Learning
## Supervised Machine Learning
Supervised machine learning is a type of machine learning where the algorithm is trained on a labeled dataset, which means that each example in the training dataset is associated with a known output or target. The goal of supervised learning is to learn a mapping or relationship between the input data and the corresponding output, so the algorithm can make predictions or decisions on new, unseen data.

Here are the key components and characteristics of supervised machine learning:

* Labeled Data: In supervised learning, you have a dataset that consists of input-output pairs, where each input is associated with a correct output. For example, in a spam email classifier, the input could be an email, and the output (label) is whether it's spam or not spam.
* Training Phase: During the training phase, the algorithm processes the labeled training data and learns to identify patterns, relationships, and features that map the inputs to the correct outputs. The goal is to minimize the difference between the predicted outputs and the true labels.
* Model Building: Supervised learning algorithms build a model based on the training data. This model can take various forms, such as decision trees, support vector machines, neural networks, or linear regression models, depending on the specific task.
* Prediction: Once the model is trained, it can be used to make predictions or classifications on new, unseen data. It takes the input data and produces an output, which is compared to the actual (known) output to assess its accuracy.
* Evaluation: The performance of the supervised learning model is evaluated using various metrics, such as accuracy, precision, recall, F1 score, and others, depending on the nature of the problem. These metrics measure how well the model generalizes to unseen data.

Common use cases of supervised learning include:
* Classification: Assigning inputs to predefined categories or labels, such as spam vs. non-spam email, sentiment analysis, image classification, and disease diagnosis.
* Regression: Predicting a continuous numerical value, such as predicting house prices based on features like size, location, and number of bedrooms.
* Natural Language Processing (NLP): Tasks like language translation, text classification, and chatbot responses.

Supervised learning is a powerful approach when you have access to labeled data and want to build predictive models or make decisions based on historical patterns. It is widely used in various applications across industries, including healthcare, finance, marketing, and more.

## Unsupervised Machine Learning
Unsupervised machine learning is a type of machine learning where the algorithm is trained on unlabeled data, meaning there are no explicit output labels or target values provided during the training process. Instead, the algorithm's objective is to discover patterns, structures, or relationships within the data without any guidance regarding what it should be looking for.

Here are the key characteristics and concepts of unsupervised machine learning:

* Unlabeled Data: In unsupervised learning, the input data consists of features, but there are no corresponding output labels. The algorithm explores the data to identify inherent structures or patterns.
* Clustering: Clustering is a common task in unsupervised learning, where the algorithm groups similar data points together into clusters or groups. Examples include customer segmentation based on purchase behavior or grouping similar news articles.
* Dimensionality Reduction: Unsupervised learning can be used for dimensionality reduction, which involves reducing the number of features in the data while retaining essential information. Principal Component Analysis (PCA) and t-Distributed Stochastic Neighbor Embedding (t-SNE) are common techniques for this purpose.
* Anomaly Detection: Unsupervised learning can identify anomalies or outliers in the data by learning what is considered normal behavior. Applications include fraud detection, network intrusion detection, and quality control.
* Association Rule Mining: This technique finds associations or relationships between items in a dataset. For example, in retail, it can discover that customers who buy product A are also likely to buy product B.

Common use cases of unsupervised learning include:

* Clustering: Grouping customers based on their purchasing behavior for targeted marketing campaigns.
* Anomaly Detection: Identifying unusual patterns in network traffic that might indicate security breaches.
* Dimensionality Reduction: Reducing the number of features in an image dataset while preserving important information for image classification.
* Recommendation Systems: Discovering patterns in user behavior to recommend products, movies, or content.
* Unsupervised learning is particularly useful when dealing with large and complex datasets where it may be challenging to manually label the data or when you want to explore the data to gain insights and uncover hidden structures. It is a valuable tool for pattern discovery and data exploration.

