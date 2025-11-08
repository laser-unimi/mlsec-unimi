# Working with numerical data

**Learning objectives**

* Understand feature vectors.
* Explore your dataset's potential features visually and
  mathematically.
* Identify outliers.
* Understand four different techniques to normalize numerical data.
* Understand binning and develop strategies for binning numerical
  data.
* Understand the characteristics of good continuous numerical
  features.

ML practitioners spend far more time evaluating, cleaning, and transforming
data than building models.
Data is so important that this course devotes three entire units to the topic:

* Working with numerical data (this unit)
* [Working with categorical data](/chapter2/categorical_data/intro.html)
* [Datasets, generalization, and overfitting](/machine-learning/crash-course/overfitting)

This unit focuses on
[**numerical data**](https://developers.google.com/machine-learning/glossary#numerical-data),
meaning integers or floating-point values
that behave like numbers. That is, they are additive, countable, ordered,
and so on. The next unit focuses on
[**categorical data**](https://developers.google.com/machine-learning/glossary#categorical-data), which can
include numbers that behave like categories. The third unit focuses on how to
prepare your data to ensure high-quality results when training and evaluating
your model.

Examples of numerical data include:

* Temperature
* Weight
* The number of deer wintering in a nature preserve

In contrast, US postal codes, despite
being five-digit or nine-digit numbers, don't behave like numbers or represent
mathematical relationships. Postal code 40004 (in Nelson County, Kentucky) is
not twice the quantity of postal code 20002 (in Washington, D.C.). These numbers
represent categories, specifically geographic areas, and are considered
categorical data.

**Key terms:**

* [Categorical data](https://developers.google.com/machine-learning/glossary#categorical-data)
* [Numerical data](https://developers.google.com/machine-learning/glossary#numerical-data)
