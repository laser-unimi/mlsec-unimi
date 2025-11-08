# Working with categorical data  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/categorical-data

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Working with categorical data Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* This module focuses on differentiating between categorical and numerical data within machine learning.
* You will learn how to represent categorical data using one-hot vectors and address common issues associated with it.
* The module covers encoding techniques for converting categorical data into numerical vectors suitable for model training.
* Feature crosses, a method for combining categorical features to capture interactions, are also discussed.
* It is assumed you have prior knowledge of introductory machine learning and working with numerical data.

**Estimated module length:** 50 minutes
**Learning objectives**

* Distinguish categorical data from numerical data.
* Represent categorical data with one-hot vectors.
* Address common issues with categorical data.
* Create feature crosses.
**Prerequisites:**

This module assumes you are familiar with the concepts covered in the
following modules:

* [Introduction to Machine Learning](/machine-learning/intro-to-ml)
* [Working with numerical data](/machine-learning/crash-course/numerical-data)

[**Categorical data**](https://developers.google.com/machine-learning/glossary#categorical-data) has a
*specific set* of possible values. For example:

* The different species of animals in a national park
* The names of streets in a particular city
* Whether or not an email is spam
* The colors that house exteriors are painted
* Binned numbers, which are described in the [Working with Numerical
  Data](/machine-learning/crash-course/numerical-data) module

## Numbers can also be categorical data

True [**numerical data**](https://developers.google.com/machine-learning/glossary#numerical-data)
can be meaningfully multiplied. For example, consider a
model that predicts the value of a house based on its area.
Note that a useful model for evaluating house prices typically relies on
hundreds of features. That said, all else being equal, a house of 200 square
meters should be roughly twice as valuable as an identical house of 100 square
meters.

Oftentimes, you should represent features that contain integer values as
categorical data instead of numerical data. For example, consider a postal
code feature in which the values are integers. If you represent this
feature numerically rather than categorically, you're asking the model
to find a numeric relationship
between different postal codes. That is, you're telling the model to
treat postal code 20004 as twice (or half) as large a signal as postal code
10002. Representing postal codes as categorical data lets the model
weight each individual postal code separately.

## Encoding

**Encoding** means converting categorical or other data to numerical vectors
that a model can train on. This conversion is necessary because models can
only train on floating-point values; models can't train on strings such as
`"dog"` or `"maple"`. This module explains different
encoding methods for categorical data.

**Key terms:**

* [Categorical data](https://developers.google.com/machine-learning/glossary#categorical-data)
* [Numerical data](https://developers.google.com/machine-learning/glossary#numerical-data)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Conclusion (2 min)](/machine-learning/crash-course/numerical-data/conclusion)

[Next

Vocabulary and one-hot encoding (10 min)

arrow\_forward](/machine-learning/crash-course/categorical-data/one-hot-encoding)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]