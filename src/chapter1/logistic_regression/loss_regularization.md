# Logistic regression: Loss and regularization

## Log Loss

In the [Linear regression module](/chapter1/linear-regression/linear_regression.html),
you used **squared loss** (also called
L2 loss) as the
**loss function**.
Squared loss works well for a linear
model where the rate of change of the output values is constant. For example,
given the linear model \\(y' = b + 3x\_1\\), each time you increment the input
value \\(x\_1\\) by 1, the output value \\(y'\\) increases by 3.

However, the rate of change of a logistic regression model is *not* constant.
As you saw in [Calculating a probability](/chapter1/logistic_regression/sigmoid_function.html), the
**sigmoid** curve is s-shaped
rather than linear. When the log-odds (\\(z\\)) value is closer to 0, small
increases in \\(z\\) result in much larger changes to \\(y\\) than when \\(z\\) is a large
positive or negative number. The following table shows the sigmoid function's
output for input values from 5 to 10, as well as the corresponding precision
required to capture the differences in the results.

| input | logistic output | required digits of precision |
| --- | --- | --- |
| 5 | 0.993 | 3 |
| 6 | 0.997 | 3 |
| 7 | 0.999 | 3 |
| 8 | 0.9997 | 4 |
| 9 | 0.9999 | 4 |
| 10 | 0.99998 | 5 |

If you used squared loss to calculate errors for the sigmoid function, as the
output got closer and closer to `0` and `1`, you would need more memory to
preserve the precision needed to track these values.

Instead, the loss function for logistic regression is
**Log Loss**. The
Log Loss equation returns the logarithm of the magnitude of the change, rather
than just the distance from data to prediction. Log Loss is calculated as
follows:

\\(\text{Log Loss} = -\frac{1}{N}\sum\_{i=1}^{N} y\_i\log(y\_i') + (1 - y\_i)\log(1 - y\_i')\\)

where:

* \\(N\\) is the number of labeled examples in the dataset
* \\(i\\) is the index of an example in the dataset (e.g., \\((x\_3, y\_3)\\)
  is the third example in the dataset)
* \\(y\_i\\) is the label for the \\(i\\)th example. Since this is logistic
  regression, \\(y\_i\\) must either be 0 or 1.
* \\(y\_i'\\) is your model's prediction for the \\(i\\)th example
  (somewhere between 0 and 1), given the set of features in \\(x\_i\\).

This form of the Log Loss function calculates the mean Log Loss across all
points in the dataset. Using mean Log Loss (as opposed to total Log Loss) is
desirable in practice, because it enables us to decouple tuning of the batch
size and the learning rate.

## Regularization in logistic regression

**Regularization**, a mechanism for
penalizing model complexity during training, is extremely important in logistic
regression modeling. Without regularization, the asymptotic nature of logistic
regression would keep driving loss towards 0 in cases where the model has a
large number of features. Consequently, most logistic regression models use one
of the following two strategies to decrease model complexity:

* [L2 regularization](/chapter2/overfitting/regularization.html)
* [Early stopping](/chapter2/overfitting/regularization.html#early_stopping_an_alternative_to_complexity-based_regularization):
  Limiting the number of training steps to halt training while loss is
  still decreasing.

**Note:** You'll learn more about
regularization in the
[Datasets, Generalization, and Overfitting](http://umido.laser.di.unimi.it:3000/chapter2/overfitting/intro.html)
module of the course.
**Key terms:**

* [Gradient descent](https://developers.google.com/machine-learning/glossary#gradient-descent)
* [Linear regression](https://developers.google.com/machine-learning/glossary#linear_regression)
* [Log Loss](https://developers.google.com/machine-learning/glossary#Log_Loss)
* [Logistic regression](https://developers.google.com/machine-learning/glossary#logistic_regression)
* [Loss function](https://developers.google.com/machine-learning/glossary#loss-function)
* [Overfitting](https://developers.google.com/machine-learning/glossary#overfitting)
* [Regularization](https://developers.google.com/machine-learning/glossary#regularization)
* [Squared loss](https://developers.google.com/machine-learning/glossary#l2-loss)
