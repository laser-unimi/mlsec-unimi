# Categorical data: Vocabulary and one-hot encoding  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/categorical-data/one-hot-encoding

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Categorical data: Vocabulary and one-hot encoding Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Dimension refers to the number of elements in a feature vector, and some categorical features have low dimensionality.
* Machine learning models require numerical input; therefore, categorical data like strings must be converted to numerical representations.
* One-hot encoding transforms categorical values into numerical vectors where each category is represented by a unique element with a value of 1.
* For high-dimensional categorical features with numerous categories, one-hot encoding might be inefficient, and embeddings or hashing are recommended.
* Sparse representation efficiently stores one-hot encoded data by only recording the position of the '1' value to reduce memory usage.

The term **dimension** is a synonym for the number of elements in a
[**feature vector**](https://developers.google.com/machine-learning/glossary#feature_vector).
Some categorical features are low dimensional. For example:

| Feature name | # of categories | Sample categories |
| --- | --- | --- |
| snowed\_today | 2 | True, False |
| skill\_level | 3 | Beginner, Practitioner, Expert |
| season | 4 | Winter, Spring, Summer, Autumn |
| day\_of\_week | 7 | Monday, Tuesday, Wednesday |
| planet | 8 | Mercury, Venus, Earth |

When a categorical feature has a low number of possible categories, you can
encode it as a **vocabulary**. With a vocabulary encoding, the model treats each
possible categorical value as a *separate feature*. During training, the
model learns different weights for each category.

For example, suppose you are creating a model to predict a car's price based,
in part, on a categorical feature named `car_color`.
Perhaps red cars are worth more than green cars.
Since manufacturers offer a limited number of exterior colors, `car_color` is
a low-dimensional categorical feature.
The following illustration suggests a vocabulary (possible values) for
`car_color`:

![IMAGE: Figure 1. Each color in the palette is represented as a separate
feature. That is, each color is a separate feature in the feature vector.
For instance, 'Red' is a feature, 'Orange' is a separate feature,
and so on.]()

**Figure 1.** A unique feature for each category.

## Exercise: Check your understanding

True or False: A machine learning model can train *directly* on
raw string values, like "Red" and "Black", without
converting these values to numerical vectors.

True

During training, a model can only manipulate floating-point numbers.
The string `"Red"` is not a floating-point number. You
must convert strings like `"Red"` to floating-point numbers.

False

A machine learning model can only train on features with
floating-point values, so you'll need to convert those strings to
floating-point values before training.

## Index numbers

Machine learning models can only manipulate floating-point numbers.
Therefore, you must convert each string to a unique index number, as in
the following illustration:

![IMAGE: Figure 2. Each color is associated with a unique integer value. For
example, 'Red' is associated with the integer 0, 'Orange' with the
integer 1, and so on.]()

**Figure 2.** Indexed features.

After converting strings to unique index numbers, you'll need to process the
data further to represent it in ways that help the model learn meaningful
relationships between the values. If the categorical feature data is left as
indexed integers and loaded into a model, the model would treat the indexed
values as continuous floating-point numbers. The model would then consider
"purple" six times more likely than "orange."

## One-hot encoding

The next step in building a vocabulary is to convert each index number to
its [**one-hot encoding**](https://developers.google.com/machine-learning/glossary#one-hot_encoding).
In a one-hot encoding:

* Each category is represented by a vector (array) of N elements, where N
  is the number of categories. For example, if `car_color` has eight possible
  categories, then the one-hot vector representing will have eight elements.
* Exactly *one* of the elements in a one-hot vector has the value 1.0;
  all the remaining elements have the value 0.0.

For example, the following table shows the one-hot encoding for each color in
`car_color`:

| Feature | Red | Orange | Blue | Yellow | Green | Black | Purple | Brown |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| "Red" | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| "Orange" | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| "Blue" | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| "Yellow" | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| "Green" | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| "Black" | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| "Purple" | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| "Brown" | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |

It is the one-hot vector, not the string or the index number, that gets passed
to the feature vector. The model learns a separate weight for each element of
the feature vector.

**Note:** In a true one-hot encoding, only one element has the value 1.0.
In a variant known as **multi-hot encoding**, multiple values
can be 1.0.

The following illustration suggests the various transformations in the
vocabulary representation:

![IMAGE: Figure 3. Diagram of the end-to-end process to map categories to
feature vectors. In the diagram, the input features are 'Yellow',
'Orange', 'Blue', and 'Blue' a second time. The system uses a stored
vocabulary ('Red' is 0, 'Orange' is 1, 'Blue' is 2, 'Yellow' is 3, and
so on) to map the input value to an ID. Thus, the system maps 'Yellow',
'Orange', 'Blue', and 'Blue' to 3, 1, 2, 2. The system then converts
those values to a one-hot feature vector. For example, given a system
with eight possible colors, 3 becomes 0, 0, 0, 1, 0, 0, 0, 0.]()

**Figure 3.** The end-to-end process to map categories to feature vectors.

### Sparse representation

A feature whose values are predominantly zero (or empty) is termed a
[**sparse feature**](https://developers.google.com/machine-learning/glossary#sparse-feature). Many
categorical features, such as `car_color`, tend to be sparse features.
[**Sparse representation**](https://developers.google.com/machine-learning/glossary#sparse-representation)
means storing the *position* of the 1.0
in a sparse vector. For example, the one-hot vector for `"Blue"` is:

> [0, 0, 1, 0, 0, 0, 0, 0]

Since the `1` is in position 2 (when starting the count at 0), the
sparse representation for the preceding one-hot vector is:

> 2

Notice that the sparse representation consumes far less memory than the
eight-element one-hot vector. Importantly, the model must *train* on the
one-hot vector, not the sparse representation.

**Note:** The sparse representation of a multi-hot encoding stores the
positions of *all* the nonzero elements. For example, the sparse
representation of a car that is both `"Blue"` and
`"Black"` is `2, 5`.

## Outliers in categorical data

Like numerical data, categorical data also contains outliers. Suppose
`car_color` contains not only the popular colors, but also some rarely used
outlier colors, such as `"Mauve"` or `"Avocado"`.
Rather than giving each of these outlier colors a separate category, you
can lump them into a single "catch-all" category called *out-of-vocabulary
(OOV)*. In other words, all the outlier colors are binned into a single
outlier bucket. The system learns a single weight for that outlier bucket.

## Encoding high-dimensional categorical features

Some categorical features have a high number of dimensions, such as
those in the following table:

| Feature name | # of categories | Sample categories |
| --- | --- | --- |
| words\_in\_english | ~500,000 | "happy", "walking" |
| US\_postal\_codes | ~42,000 | "02114", "90301" |
| last\_names\_in\_Germany | ~850,000 | "Schmidt", "Schneider" |

When the number of categories is high, one-hot encoding is usually a bad choice.
*Embeddings*, detailed in a separate
[Embeddings module](/machine-learning/crash-course/embeddings), are usually
a much better choice. Embeddings substantially reduce the number of
dimensions, which benefits models in two important ways:

* The model typically trains faster.
* The built model typically infers predictions more quickly. That is, the
  model has lower latency.

[**Hashing**](https://developers.google.com/machine-learning/glossary#hashing) (also called the *hashing
trick*) is a less common way to reduce the number of dimensions.

**Click here to learn about hashing**

In brief, hashing maps a category (for example, a color) to a small
integer—the number of the "bucket" that will hold that category.

In detail, you implement a hashing algorithm as follows:

1. Set the number of bins in the vector of categories to N,
   where N is less than the total number of remaining categories.
   As an arbitrary example, say N = 100.
2. Choose a hash function. (Often, you will choose the range of hash
   values as well.)
3. Pass each category (for example, a particular color) through that
   hash function, generating a hash value, say 89237.
4. Assign each bin an index number of the output hash value modulo N.
   In this case, where N is 100 and the hash value is 89237, the modulo
   result is 37 because 89237 % 100 is 37.
5. Create a one-hot encoding for each bin with these new index numbers.

For more details about hashing data, see the
[Randomization](/machine-learning/crash-course/production-ml-systems/monitoring#randomization)
section of the
[Production machine learning systems](/machine-learning/crash-course/production-ml-systems/monitoring)
module.

**Key terms:**

* [Categorical data](https://developers.google.com/machine-learning/glossary#categorical_data)
* [Dimensions](https://developers.google.com/machine-learning/glossary#dimensions)
* [Discrete feature](https://developers.google.com/machine-learning/glossary#discrete_feature)
* [Feature cross](https://developers.google.com/machine-learning/glossary#feature_cross)
* [Feature vector](https://developers.google.com/machine-learning/glossary#feature_vector)
* [Hashing](https://developers.google.com/machine-learning/glossary#hashing)
* [One-hot encoding](https://developers.google.com/machine-learning/glossary#one-hot_encoding)
* [Sparse feature](https://developers.google.com/machine-learning/glossary#sparse-feature)
* [Sparse representation](https://developers.google.com/machine-learning/glossary#sparse-representation)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Introduction (5 min)](/machine-learning/crash-course/categorical-data)

[Next

Common issues with categorical data (5 min)

arrow\_forward](/machine-learning/crash-course/categorical-data/issues)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]