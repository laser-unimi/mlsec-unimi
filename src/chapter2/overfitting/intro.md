# Datasets, generalization, and overfitting  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Datasets, generalization, and overfitting Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* This module emphasizes the critical role of data quality in machine learning projects, highlighting that it significantly impacts model performance more than algorithm choice.
* Machine learning practitioners typically dedicate a substantial portion of their project time (around 80%) to data preparation and transformation, including tasks like dataset construction and feature engineering.
* The module covers key concepts in data preparation, such as identifying data characteristics, handling unreliable data, understanding data labels, and splitting datasets for training and evaluation.
* Learners will gain insights into techniques for improving data quality, mitigating issues like overfitting, and interpreting loss curves to assess model performance.
* This module builds upon foundational machine learning concepts, assuming familiarity with topics like linear regression, numerical and categorical data handling, and basic machine learning principles.

**Estimated module length:** 105 minutes
**Learning objectives**

* Identify four different characteristics of data and datasets.
* Identify at least four different causes of data unreliability.
* Determine when to discard missing data and when to impute it.
* Differentiate between direct and derived labels.
* Identify two different ways to improve the quality of human-rated
  labels.
* Explain why to subdivide a dataset into a training set, validation set,
  and test set; identify a potential problem in data splits.
* Explain overfitting and identify three possible causes for it.
* Explain the concept of regularization. In particular, explain the
  following:
  + Bias versus variance (adaptation to outliers…)
  + L2 regularization, including Lambda (regularization
    rate)
  + Early stopping
* Interpret different kinds of loss curves; detect convergence and
  overfitting in loss curves.
**Prerequisites:**

This module assumes you are familiar with the concepts covered in the
following modules:

* [Introduction to Machine Learning](/machine-learning/intro-to-ml)
* [Linear regression](/machine-learning/crash-course/linear-regression)
* [Working with numerical data](/machine-learning/crash-course/numerical-data)
* [Working with categorical data](/machine-learning/crash-course/categorical-data)

## Introduction

This module begins with a leading question.
Choose one of the following answers:

If you had to prioritize improving one of the following areas
in your machine learning project, which would have the most
impact?

Improving the quality of your dataset

Data trumps all.
The quality and size of the dataset matters much more than which
shiny algorithm you use to build your model.

Applying a more clever loss function to training your model

True, a better loss function can help a model train faster, but
it's still a distant second to another item in this list.

And here's an even more leading question:

Take a guess: In your machine learning project, how much time
do you typically spend on data preparation and transformation?

More than half of the project time

Yes, ML practitioners spend the majority of their time
constructing datasets and doing feature engineering.

Less than half of the project time

Plan for more! Typically, 80% of the time on a machine learning
project is spent constructing datasets and transforming data.

In this module, you'll learn more about the characteristics of machine learning
datasets, and how to prepare your data to ensure high-quality results when
training and evaluating your model.

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Test your knowledge (10 min)](/machine-learning/crash-course/categorical-data/test-your-knowledge)

[Next

Data characteristics (10 min)

arrow\_forward](/machine-learning/crash-course/overfitting/data-characteristics)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]