# Numerical data: Qualities of good numerical features  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/numerical-data/qualities-of-good-numerical-features

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Numerical data: Qualities of good numerical features Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Good feature vectors require features that are clearly named and have obvious meanings to anyone on the project.
* Data should be checked and tested for bad data or outliers like inappropriate values before being used for training.
* Features should be sensible, avoiding "magic values" that create discontinuities; instead, use separate boolean features or new discrete values to indicate missing data.
* Continuous features should not have magic values representing the absence of measurement, but rather use separate Boolean features or discrete values.
* Discrete numerical features with missing values should be assigned a new value within the finite set, enabling the model to learn weights for each value including missing features.

This unit has explored ways to map raw data into suitable
[**feature vectors**](https://developers.google.com/machine-learning/glossary#feature_vector).
Good numerical [**features**](https://developers.google.com/machine-learning/glossary#feature) share the
qualities described in this section.

## Clearly named

Each feature should have a clear, sensible, and obvious meaning to any human on
the project. For example, the meaning of the following feature value is
confusing:

Not recommended

> house\_age: 851472000

In contrast, the following feature name and value are far clearer:

Recommended

> house\_age\_years: 27

**Note:** Although your co-workers will rebel against confusing feature
and label names, the model won't care (assuming you normalize
values properly).

## Checked or tested before training

Although this module has devoted a lot of time to
[**outliers**](https://developers.google.com/machine-learning/glossary#outliers), the topic is
important enough to warrant one final mention. In some cases, bad data
(rather than bad engineering choices) causes unclear values. For example,
the following `user_age_in_years` came from a source that didn't check for
appropriate values:

Not recommended

> user\_age\_in\_years: 224

But people *can* be 24 years old:

Recommended

> user\_age\_in\_years: 24

Check your data!

## Sensible

A "magic value" is a purposeful discontinuity in an otherwise continuous
feature. For example, suppose a continuous feature named `watch_time_in_seconds`
can hold any floating-point value between 0 and 30 but represents the *absence*
of a measurement with the magic value -1:

Not recommended

> watch\_time\_in\_seconds: -1

A `watch_time_in_seconds` of -1 would force the model to try to figure
out what it means to watch a movie backwards in time. The resulting model would
probably not make good predictions.

A better technique is to create a separate Boolean feature that indicates
whether or not a `watch_time_in_seconds`
value is supplied. For example:

Recommended

> watch\_time\_in\_seconds: 4.82  
> is\_watch\_time\_in\_seconds\_defined=True
>
> watch\_time\_in\_seconds: 0  
> is\_watch\_time\_in\_seconds\_defined=False

This is a way to handle a continuous dataset with missing values. Now consider
a [**discrete**](https://developers.google.com/machine-learning/glossary#discrete_feature)
numerical feature, like `product_category`, whose values must belong to a finite
set of values. In this
case, when a value is missing, signify that missing value using a new value in
the finite set. With a discrete feature, the model will learn different weights
for each value, including original weights for missing features.

For example, we can imagine possible values fitting in the set:

> {0: 'electronics', 1: 'books', 2: 'clothing', 3: 'missing\_category'}.

**Key terms:**

* [Outliers](https://developers.google.com/machine-learning/glossary#outliers)
* [Feature](https://developers.google.com/machine-learning/glossary#feature)
* [Feature vector](https://developers.google.com/machine-learning/glossary#feature_vector)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Scrubbing (5 min)](/machine-learning/crash-course/numerical-data/scrubbing)

[Next

Polynomial transforms (5 min)

arrow\_forward](/machine-learning/crash-course/numerical-data/polynomial-transforms)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]