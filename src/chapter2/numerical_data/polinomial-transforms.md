# Numerical data: Polynomial transforms

Sometimes, when the ML practitioner has domain knowledge suggesting
that one variable is related to the square, cube, or other power of another
variable, it's useful to create a
[**synthetic feature**](https://developers.google.com/machine-learning/glossary#synthetic_feature) from one
of the existing numerical [**features**](https://developers.google.com/machine-learning/glossary#feature).

Consider the following spread of data points, where pink circles represent
one class or category (for example, a species of tree) and green triangles
another class (or species of tree):

![IMAGE: Figure 17. y=x^2 spread of data points, with triangles below the curve and circles above the curve.](/static/chapter2/numerical/polynomial-transforms/ft_cross2.png)

**Figure 17.** Two classes that can't be separated by a line.

It's not possible to draw a straight line that cleanly separates the two
classes, but it *is* possible to draw a curve that does so:

![IMAGE: Figure 18. Same image as Figure 17, only this time with y=x^2 overlaid to create a clear boundary between the triangles and circles.](/static/chapter2/numerical/polynomial-transforms/ft_cross1.png)

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
