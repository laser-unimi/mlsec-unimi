# Datasets: Transforming data  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting/transforming-data

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Datasets: Transforming data Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Machine learning models require all data, including features like street names, to be transformed into numerical (floating-point) representations for training.
* Normalization is crucial for optimizing model training by converting existing floating-point features to a specific range.
* When dealing with large datasets, selecting a relevant subset of data for training is essential for model performance.
* Protecting user privacy by excluding Personally Identifiable Information (PII) from datasets is a critical consideration.

Machine learning models can only train on floating-point values.
However, many dataset features are *not* naturally floating-point values.
Therefore, one important part of machine learning is transforming
non-floating-point features to floating-point representations.

For example, suppose `street names` is a feature. Most street names
are strings, such as "Broadway" or "Vilakazi".
Your model can't train on "Broadway", so you must transform "Broadway"
to a floating-point number. The [Categorical Data
module](/machine-learning/crash-course/categorical-data)
explains how to do this.

Additionally, you should even transform most floating-point features.
This transformation process, called
[**normalization**](https://developers.google.com/machine-learning/glossary#normalization), converts
floating-point numbers to a constrained range that improves model training.
The [Numerical Data
module](/machine-learning/crash-course/numerical-data)
explains how to do this.

## Sample data when you have too much of it

Some organizations are blessed with an abundance of data.
When the dataset contains too many examples, you must select a *subset*
of examples for training. When possible, select the subset that is most
relevant to your model's predictions.

## Filter examples containing PII

Good datasets omit examples containing Personally Identifiable Information
(PII). This policy helps safeguard privacy but can influence the model.

See the Safety and Privacy module later in the course for more on these topics.

**Key terms:**

* [Normalization](https://developers.google.com/machine-learning/glossary#normalization)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Dividing the original dataset (10 min)](/machine-learning/crash-course/overfitting/dividing-datasets)

[Next

Generalization (5 min)

arrow\_forward](/machine-learning/crash-course/overfitting/generalization)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]