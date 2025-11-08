# Numerical data: Polynomial transforms  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/numerical-data/polynomial-transforms

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Numerical data: Polynomial transforms Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Synthetic features, like polynomial transforms, enable linear models to represent non-linear relationships by introducing new features based on existing ones.
* Polynomial transforms involve raising an existing feature to a power, often informed by domain knowledge, such as physical laws involving squared terms.
* By incorporating synthetic features, linear regression models can effectively separate data points that are not linearly separable using curves instead of straight lines.
* This approach maintains the simplicity of linear regression while expanding its capacity to capture complex patterns within the data.
* Feature crosses, a related concept for categorical data, synthesize new features by combining existing features, further enhancing model flexibility.

Sometimes, when the ML practitioner has domain knowledge suggesting
that one variable is related to the square, cube, or other power of another
variable, it's useful to create a
[**synthetic feature**](https://developers.google.com/machine-learning/glossary#synthetic_feature) from one
of the existing numerical [**features**](https://developers.google.com/machine-learning/glossary#feature).

Consider the following spread of data points, where pink circles represent
one class or category (for example, a species of tree) and green triangles
another class (or species of tree):

![IMAGE: Figure 17. y=x^2 spread of data points, with triangles below the
curve and circles above the curve.]()

**Figure 17.** Two classes that can't be separated by a line.

It's not possible to draw a straight line that cleanly separates the two
classes, but it *is* possible to draw a curve that does so:

![IMAGE: Figure 18. Same image as Figure 17, only this time with y=x^2
overlaid to create a clear boundary between the triangles and
circles.]()

**Figure 18.** Separating the classes with *y = x2*.

As discussed in the
[Linear regression module](/machine-learning/crash-course/linear-regression),
a linear model with one feature, \\(x\_1\\), is described by the linear equation:

\\[y = b + w\_1x\_1\\]

Additional features are handled by the addition of terms \(w\_2x\_2\),
\(w\_3x\_3\), etc.

[**Gradient descent**](https://developers.google.com/machine-learning/glossary#gradient_descent) finds the
[**weight**](https://developers.google.com/machine-learning/glossary#weight) \\(w\_1\\) (or weights
\(w\_1\), \(w\_2\), \(w\_3\), in the case of additional features) that minimizes
the loss of the model. But the data points shown cannot be separated by a line.
What can be done?

It's possible to keep both the linear equation *and* allow nonlinearity
by defining a new term, \(x\_2\), that is simply \(x\_1\) squared:

\\[x\_2 = x\_1^2\\]

This synthetic feature, called a polynomial transform, is treated like any
other feature. The previous linear formula becomes:

\\[y = b + w\_1x\_1 + w\_2x\_2\\]

This can still be treated like a
[**linear regression**](https://developers.google.com/machine-learning/glossary#linear_regression)
problem, and the weights determined through gradient descent, as usual, despite
containing a hidden squared term, the polynomial transform. Without changing
how the linear model trains, the addition of a polynomial transform allows the
model to separate the data points using a curve of the
form \\(y = b + w\_1x + w\_2x^2\\).

Usually the numerical feature of interest is multiplied by itself, that is,
raised to some power. Sometimes an ML practitioner can make an informed guess
about the appropriate exponent. For example, many relationships in the physical
world are related to squared terms,
including acceleration due to gravity, the
attenuation of light or sound over distance, and elastic potential energy.

If you transform a feature in a way that changes its scale, you should consider
experimenting with normalizing it as well. Normalizing after transforming
might make the model perform better. For more information, see
[Numerical Data: Normalization](/machine-learning/crash-course/numerical-data/normalization).

A related concept in
[**categorical data**](https://developers.google.com/machine-learning/glossary#categorical_data) is the
[**feature cross**](https://developers.google.com/machine-learning/glossary#feature_cross), which more
frequently synthesizes two different features.

**Key terms:**

* [Categorical data](https://developers.google.com/machine-learning/glossary#categorical_data)
* [Feature](https://developers.google.com/machine-learning/glossary#feature)
* [Feature cross](https://developers.google.com/machine-learning/glossary#feature_cross)
* [Gradient descent](https://developers.google.com/machine-learning/glossary#gradient_descent)
* [Linear regression](https://developers.google.com/machine-learning/glossary#linear_regression)
* [Synthetic feature](https://developers.google.com/machine-learning/glossary#synthetic_feature)
* [Weight](https://developers.google.com/machine-learning/glossary#weight)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Qualities of good numerical features (5 min)](/machine-learning/crash-course/numerical-data/qualities-of-good-numerical-features)

[Next

Test your knowledge (10 min)

arrow\_forward](/machine-learning/crash-course/numerical-data/test-your-knowledge)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]