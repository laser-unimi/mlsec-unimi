# Categorical data: Feature crosses  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/categorical-data/feature-crosses

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Categorical data: Feature crosses Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Feature crosses are created by combining two or more categorical or bucketed features to capture interactions and nonlinearities within a dataset.
* They enable linear models to handle nonlinearities similar to polynomial transforms, but feature crosses work with categorical data while polynomial transforms are applied to numerical data.
* Feature crosses can be particularly effective when guided by domain expertise, but using neural networks can automate the process of discovering valuable combinations.
* Overuse of feature crosses with sparse features should be avoided, as it can lead to excessive sparsity in the resulting feature set.

[**Feature crosses**](https://developers.google.com/machine-learning/glossary#feature-cross) are created by
crossing (taking the Cartesian product of) two or more categorical or bucketed
features of the dataset. Like [polynomial
transforms](/machine-learning/crash-course/numerical-data/polynomial-transforms),
feature crosses allow linear models to handle nonlinearities. Feature crosses
also encode interactions between features.

For example, consider a leaf dataset with the categorical features:

* `edges`, containing values `smooth`, `toothed`, and `lobed`
* `arrangement`, containing values `opposite` and `alternate`

Assume the order above is the order of the feature columns in a one-hot
representation, so that a leaf with `smooth` edges and `opposite` arrangement
is represented as `{(1, 0, 0), (1, 0)}`.

The feature cross, or Cartesian product, of these two features would be:

`{Smooth_Opposite, Smooth_Alternate, Toothed_Opposite, Toothed_Alternate,
Lobed_Opposite, Lobed_Alternate}`

where the value of each term is the product of the base feature values, such
that:

* `Smooth_Opposite = edges[0] * arrangement[0]`
* `Smooth_Alternate = edges[0] * arrangement[1]`
* `Toothed_Opposite = edges[1] * arrangement[0]`
* `Toothed_Alternate = edges[1] * arrangement[1]`
* `Lobed_Opposite = edges[2] * arrangement[0]`
* `Lobed_Alternate = edges[2] * arrangement[1]`

For example, if a leaf has a `lobed` edge and an `alternate` arrangement, the
feature-cross vector will have a value of 1 for `Lobed_Alternate`, and a value
of 0 for all other terms:

`{0, 0, 0, 0, 0, 1}`

This dataset could be used to classify leaves by tree species, since these
characteristics do not vary within a species.

**Click here to compare polynomial transforms
with feature crosses**

Feature crosses are somewhat analogous to
[Polynomial transforms](/machine-learning/crash-course/numerical-data/polynomial-transforms).
Both combine multiple features into a new synthetic feature that the model can
train on to learn nonlinearities. Polynomial transforms typically combine
numerical data, while feature crosses combine categorical data.

## When to use feature crosses

Domain knowledge can suggest a useful combination of features
to cross. Without that domain knowledge, it can be difficult to determine
effective feature crosses or polynomial transforms by hand. It's often possible,
if computationally expensive, to use
[neural networks](/machine-learning/crash-course/neural-networks) to
*automatically* find and apply useful feature combinations during training.

Be careful—crossing two sparse features produces an even sparser new
feature than the two original features. For example, if feature A is a
100-element sparse feature and feature B is a 200-element sparse feature,
a feature cross of A and B yields a 20,000-element sparse feature.

**Key terms:**

* [Feature cross](https://developers.google.com/machine-learning/glossary#feature-cross)
* [Neural network](https://developers.google.com/machine-learning/glossary#neural_network)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Common issues with categorical data (5 min)](/machine-learning/crash-course/categorical-data/issues)

[Next

Feature cross exercises (15 min)

arrow\_forward](/machine-learning/crash-course/categorical-data/feature-cross-exercises)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]