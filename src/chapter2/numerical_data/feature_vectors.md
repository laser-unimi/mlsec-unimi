# Numerical data: How a model ingests data using feature vectors

Until now, we've given you the impression that a model acts directly on the
rows of a dataset; however, models actually ingest data somewhat differently.

For example, suppose a dataset provides five columns, but only two of those
columns (`b` and `d`) are features in the model. When processing
the example in row 3, does the model simply grab the contents of the
highlighted two cells (3b and 3d) as follows?

![IMAGE: Figure 1. A model ingesting an example directly from a dataset. Columns b and d of Row 3 are highlighted.]()

**Figure 1.** Not exactly how a model gets its examples.

In fact, the model actually ingests an array of floating-point values called a
[**feature vector**](https://developers.google.com/machine-learning/glossary#feature-vector). You can think
of a feature vector as the floating-point values comprising one example.

![IMAGE: Figure 2. The feature vector is an intermediary between the dataset and the model.]()

**Figure 2.** Closer to the truth, but not realistic.

However, feature vectors seldom use the dataset's *raw values*.
Instead, you must typically process the dataset's values into representations
that your model can better learn from. So, a more realistic
feature vector might look something like this:

![IMAGE: Figure 3. The feature vector contains two floating-point values: 0.13 and 0.47. A more realistic feature vector.]()

**Figure 3.** A more realistic feature vector.

Wouldn't a model produce better predictions by training from the
*actual* values in the dataset than from *altered* values?
Surprisingly, the answer is no.

You must determine the best way to represent raw dataset values as trainable
values in the feature vector.
This process is called
[**feature engineering**](https://developers.google.com/machine-learning/glossary#feature-engineering),
and it is a vital part of machine learning.
The most common feature engineering techniques are:

* [**Normalization**](https://developers.google.com/machine-learning/glossary#normalization): Converting
  numerical values into a standard range.
* [**Binning**](https://developers.google.com/machine-learning/glossary#binning) (also referred to as
  [**bucketing**](https://developers.google.com/machine-learning/glossary#bucketing)): Converting numerical
  values into buckets of ranges.

This unit covers normalizing and binning. The next unit,
[Working with categorical data](/chapter2/categorical_data/intro.html),
covers other forms of
[**preprocessing**](https://developers.google.com/machine-learning/glossary#preprocessing), such as
converting non-numerical data, like strings, to floating point values.

Every value in a feature vector must be a floating-point value. However, many
features are naturally strings or other non-numerical values. Consequently,
a large part of feature engineering is representing non-numerical values as
numerical values. You'll see a lot of this in later modules.

**Key terms:**

* [Binning](https://developers.google.com/machine-learning/glossary#binning)
* [Bucketing](https://developers.google.com/machine-learning/glossary#bucketing)
* [Feature engineering](https://developers.google.com/machine-learning/glossary#feature_engineering)
* [Feature vector](https://developers.google.com/machine-learning/glossary#feature_vector)
* [Normalization](https://developers.google.com/machine-learning/glossary#normalization)
* [Preprocessing](https://developers.google.com/machine-learning/glossary#preprocessing)
