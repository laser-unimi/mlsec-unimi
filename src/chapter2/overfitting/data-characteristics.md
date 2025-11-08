# Datasets: Data characteristics  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting/data-characteristics

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Datasets: Data characteristics Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* A machine learning model's performance is heavily reliant on the quality and quantity of the dataset it's trained on, with larger, high-quality datasets generally leading to better results.
* Datasets can contain various data types, including numerical, categorical, text, multimedia, and embedding vectors, each requiring specific handling for optimal model training.
* Maintaining data quality involves addressing issues like label errors, noisy features, and proper filtering to ensure the reliability of the dataset for accurate predictions.
* Incomplete examples with missing feature values should be handled by either deletion or imputation to avoid negatively impacting model training.
* When imputing missing values, use reliable methods like mean/median imputation and consider adding an indicator column to signal imputed values to the model.

A [**dataset**](https://developers.google.com/machine-learning/glossary#dataset) is a collection of
[**examples**](https://developers.google.com/machine-learning/glossary#example).

Many datasets store data in tables (grids), for example, as
comma-separated values (CSV) or directly from spreadsheets or
database tables. Tables are an intuitive input format for machine
learning [**models**](https://developers.google.com/machine-learning/glossary#model).
You can imagine each row of the table as an example
and each column as a potential feature or label.
That said, datasets may also be derived from other formats, including
log files and protocol buffers.

Regardless of the format, your ML model is only as good as the
data it trains on. This section examines key data characteristics.

## Types of data

A dataset could contain many kinds of datatypes, including but certainly
not limited to:

* numerical data, which is covered in a [separate
  unit](/machine-learning/crash-course/numerical-data)
* categorical data, which is covered in a [separate
  unit](/machine-learning/crash-course/categorical-data)
* human language, including individual words and sentences, all the way up to
  entire text documents
* multimedia (such as images, videos, and audio files)
* outputs from other ML systems
* [**embedding vectors**](https://developers.google.com/machine-learning/glossary#embedding-vector), which are
  covered in a later unit

## Quantity of data

As a rough rule of thumb, your model should train on at least an order
of magnitude (or two) more examples than trainable parameters. However, good
models generally train on *substantially* more examples than that.

Models trained on large datasets with few
[**features**](https://developers.google.com/machine-learning/glossary#feature)
generally outperform models trained on small datasets with
a lot of features.
Google has historically had great success training simple models on
large datasets.

Different datasets for different machine learning programs may require wildly
different amounts of examples to build a useful model. For some relatively
simple problems, a few dozen examples might be sufficient. For other problems,
a trillion examples might be insufficient.

It's possible to get good results from a small dataset if you are adapting
an existing model already trained on large quantities of data from the
same schema.

## Quality and reliability of data

Everyone prefers high quality to low quality, but quality is such a vague
concept that it could be defined many different ways. This course defines
**quality** pragmatically:

> A high-quality dataset helps your model accomplish its goal.
> A low quality dataset inhibits your model from accomplishing its goal.

A high-quality dataset is usually also reliable.
**Reliability** refers to the degree to which you can *trust* your data.
A model trained on a reliable dataset is more likely to yield useful
predictions than a model trained on unreliable data.

In *measuring* reliability, you must determine:

* How common are label errors? For example, if your data is
  labeled by humans, how often did your human raters make mistakes?
* Are your features *noisy*? That is, do the values in your features
  contain errors? Be realistic—you can't purge your dataset
  of all noise. Some noise is normal; for example, GPS measurements of any
  location always fluctuate a little, week to week.
* Is the data properly filtered for your problem? For example,
  should your dataset include search queries from bots? If you're
  building a spam-detection system, then likely the answer is yes.
  However, if you're trying to improve search results for humans, then no.

The following are common causes of unreliable data in datasets:

* Omitted values. For example, a person forgot to enter a value for a
  house's age.
* Duplicate examples. For example, a server mistakenly uploaded the same
  log entries twice.
* Bad feature values. For example, someone typed an extra digit, or a
  thermometer was left out in the sun.
* Bad labels. For example, a person mistakenly labeled a picture of an
  oak tree as a maple tree.
* Bad sections of data. For example, a certain feature is very reliable,
  except for that one day when the network kept crashing.

We recommend using automation to flag unreliable data. For example,
unit tests that define or rely on an external formal data schema can
flag values that fall outside of a defined range.

**Note:** Any sufficiently large or diverse dataset almost certainly contains
[**outliers**](https://developers.google.com/machine-learning/glossary#outliers) that fall outside your
data schema or unit test bands.
Determining how to handle outliers is an important part of machine learning.
The [**Numerical data
unit**](/machine-learning/crash-course/numerical-data)
details how to handle numeric outliers.

## Complete vs. incomplete examples

In a perfect world, each example is **complete**; that is, each example contains
a value for each feature.

![IMAGE: Figure 1. An example containing values for all five of its
features.]()

**Figure 1.** A complete example.

Unfortunately, real-world examples are often **incomplete**, meaning that at
least one feature value is missing.

![IMAGE: Figure 2. An example containing values for four of its five
features. One feature is marked missing.]()

**Figure 2.** An incomplete example.

Don't train a model on incomplete examples. Instead, fix or eliminate
incomplete examples by doing one of the following:

* Delete incomplete examples.
* [**Impute**](https://developers.google.com/machine-learning/glossary#value-imputation) missing values;
  that is, convert the incomplete example to a complete example by providing
  well-reasoned guesses for the missing values.

![IMAGE: Figure 3. A dataset containing three examples, two of which are
incomplete examples. Someone has stricken these two incomplete
examples from the dataset.]()

**Figure 3.** Deleting incomplete examples from the dataset.

![IMAGE: Figure 4. A dataset containing three examples, two of which were
incomplete examples containing missing data. Some entity (a human
or imputation software) has imputed values that replaced the
missing data.]()

**Figure 4.** Imputing missing values for incomplete examples.

If the dataset contains enough complete examples to train a useful model,
then consider deleting the incomplete examples.
Similarly, if only one feature is missing a significant amount of data and that
one feature probably can't help the model much, then consider deleting
that feature from the model inputs and seeing how much quality is lost by its
removal. If the model works just or almost as well without it, that's great.
Conversely, if you don't have enough complete examples to train a useful model,
then you might consider imputing missing values.

It's fine to delete useless or redundant examples, but it's bad to delete
important examples. Unfortunately, it can be difficult to differentiate
between useless and useful examples. If you can't decide whether
to delete or impute, consider building two datasets: one formed by deleting
incomplete examples and the other by imputing.
Then, determine which dataset trains the better model.

#### Click the icon to learn more about imputation handling.

Clever algorithms can impute some pretty good missing values;
however, imputed values are rarely as good as the actual values.
Therefore, a good dataset tells the model which values are imputed and
which are actual. One way to do this is to add an extra Boolean column
to the dataset that indicates whether a particular feature's value
is imputed. For example, given a feature named `temperature`,
you could add an extra Boolean feature named something like
`temperature_is_imputed`. Then, during training, the model will
probably gradually learn to trust examples containing imputed values for
feature `temperature` *less* than examples containing
actual (non-imputed) values.

---


Imputation is the process of generating well-reasoned data, not random or
deceptive data. Be careful: good imputation can improve your model; bad
imputation can hurt your model.

One common algorithm is to use the mean or median as the imputed value.
Consequently, when you represent a numerical feature with
[**Z-scores**](https://developers.google.com/machine-learning/glossary#z-score-normalization), then
the imputed value is typically 0 (because 0 is generally the mean Z-score).

### Exercise: Check your understanding

A sorted dataset, like the one in the
following exercise, can sometimes simplify imputation. However,
it is a bad idea to train on a sorted dataset. So, after
imputation, randomize the order of examples in the training set.

Here are two columns of a dataset sorted by `Timestamp`.

| Timestamp | Temperature |
| --- | --- |
| June 8, 2023 09:00 | 12 |
| June 8, 2023 10:00 | 18 |
| June 8, 2023 11:00 | missing |
| June 8, 2023 12:00 | 24 |
| June 8, 2023 13:00 | 38 |

Which of the following would be a reasonable value to impute
for the missing value of Temperature?

23

Probably. 23 is the mean of the adjacent values (12, 18, 24, and 38).
However, we aren't seeing the rest of the dataset, so it is possible
that 23 would be an outlier for 11:00 on other days.

31

Unlikely. The limited part of the dataset that we can see suggests
that 31 is much too high for the 11:00 Temperature. However,
we can't be sure without basing the imputation on a larger number of
examples.

51

Very unlikely. 51 is much higher than any of the displayed values
(and, therefore, much higher than the mean).

**Key terms:**

* [Dataset](https://developers.google.com/machine-learning/glossary#dataset)
* [Embedding vector](https://developers.google.com/machine-learning/glossary#embedding-vector)
* [Example](https://developers.google.com/machine-learning/glossary#example)
* [Feature](https://developers.google.com/machine-learning/glossary#feature)
* [Model](https://developers.google.com/machine-learning/glossary#model)
* [Value imputation](https://developers.google.com/machine-learning/glossary#value-imputation)
* [Z-score normalization](https://developers.google.com/machine-learning/glossary#z-score-normalization)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Introduction (5 min)](/machine-learning/crash-course/overfitting)

[Next

Labels (10 min)

arrow\_forward](/machine-learning/crash-course/overfitting/labels)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]