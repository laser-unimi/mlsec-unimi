# Numerical data: Qualities of good numerical features

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
