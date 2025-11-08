# Linear regression: Loss

**Loss** is a numerical metric that describes
how wrong a model's **predictions**
are. Loss measures the distance between the model's predictions and the actual
labels. The goal of training a model is to minimize the loss, reducing it to its
lowest possible value.

In the following image, you can visualize loss as arrows drawn from the data
points to the model. The arrows show how far the model's predictions are from
the actual values.

![IMAGE: Figure 8. Loss lines connect the data points to the model.](/static/chapter1/linear-regression/loss/loss-lines.png)

**Figure 8**. Loss is measured from the actual value to the predicted value.

## Distance of loss

In statistics and machine learning, loss measures the difference between the
predicted and actual values. Loss focuses on the *distance* between the values,
not the direction. For example, if a model predicts 2, but the actual value is
5, we don't care that the loss is negative (\\( 2-5=-3 \\)).
Instead, we care that the *distance* between the values is \\( 3 \\). Thus, all
methods for calculating loss remove the sign.

The two most common methods to remove the sign are the following:

* Take the absolute value of the difference between the actual value and the
  prediction.
* Square the difference between the actual value and the prediction.

## Types of loss

In linear regression, there are five main types of loss, which are outlined in
the following table.

| Loss type | Definition | Equation |
| --- | --- | --- |
| **L1 loss** | The sum of the absolute values of the difference between the predicted values and the actual values. | \\( ∑ \| actual\ value - predicted\ value \| \\) |
| **Mean absolute error (MAE)** | The average of L1 losses across a set of *N* examples. | \\( \frac{1}{N} ∑ \| actual\ value - predicted\ value \| \\) |
| **L2 loss** | The sum of the squared difference between the predicted values and the actual values. | \\( ∑(actual\ value - predicted\ value)^2 \\) |
| **Mean squared error (MSE)** | The average of L2 losses across a set of *N* examples. | \\( \frac{1}{N} ∑ (actual\ value - predicted\ value)^2 \\) |
| **Root mean squared error (RMSE)** | The square root of the mean squared error (MSE). | \\( \sqrt{\frac{1}{N} ∑ (actual\ value - predicted\ value)^2} \\) |

The functional difference between L1 loss and L2 loss
(or between MAE/RMSE and MSE) is squaring. When the difference between the
prediction and label is large, squaring makes the loss even larger. When the
difference is small (less than 1), squaring makes the loss even smaller.

Loss metrics like MAE and RMSE may be preferable to L2 loss or MSE in
some use cases because they tend to be more human-interpretable, as they measure
error using the same scale as the model's predicted value.

**Note:** MAE and RMSE can differ quite widely. MAE represents the average
prediction error, whereas RMSE represents the "spread" of the errors, and is
more skewed by larger errors.

When processing multiple examples at once, we recommend averaging the losses
across all the examples, whether using MAE, MSE, or RMSE.

## Calculating loss example

Using the previous [best fit line](/chapter1/linear-regression/linear_regression.html#linear-regression-equation),
we'll calculate L2 loss for a single example. From the
best fit line, we had the following values for weight and bias:

* \\( \small{Weight: -4.6} \\)
* \\( \small{Bias: 34} \\)

If the model predicts that a 2,370-pound car gets 23.1 miles per gallon, but it
actually gets 26 miles per gallon, we would calculate the L2 loss as
follows:

**Note:** The formula uses 2.37 because the graphs are scaled to 1000s of pounds

| Value | Equation | Result |
| --- | --- | --- |
| Prediction | \\(\small{bias + (weight \* feature\ value)}\\)  \\(\small{34 + (-4.6\*2.37)}\\) | \\(\small{23.1}\\) |
| Actual value | \\( \small{ label } \\) | \\( \small{ 26 } \\) |
| L2 loss | \\( \small{ (actual\ value - predicted\ value)^2 } \\)  \\(\small{ (26 - 23.1)^2 }\\) | \\(\small{8.41}\\) |

In this example, the L2 loss for that single data point is 8.41.

## Choosing a loss

Deciding whether to use MAE or MSE can depend on the dataset and the way you
want to handle certain predictions. Most feature values in a dataset typically
fall within a distinct range. For example, cars are normally between 2000 and
5000 pounds and get between 8 to 50 miles per gallon. An 8,000-pound car,
or a car that gets 100 miles per gallon, is outside the typical range and would
be considered an **outlier**.

An outlier can also refer to how far off a model's predictions are from the real
values. For instance, 3,000 pounds is within the typical car-weight range, and
40 miles per gallon is within the typical fuel-efficiency range. However, a
3,000-pound car that gets 40 miles per gallon would be an outlier in terms of
the model's prediction because the model would predict that a 3,000-pound car
would get around 20 miles per gallon.

When choosing the best loss function, consider how you want the model to treat
outliers. For instance, MSE moves the model more toward the outliers, while MAE
doesn't. L2 loss incurs a much higher penalty for an outlier than
L1 loss. For example, the following images show a model trained
using MAE and a model trained using MSE. The red line represents a fully
trained model that will be used to make predictions. The outliers are closer to
the model trained with MSE than to the model trained with MAE.

![IMAGE: Figure 9. The model is tilted more toward the outliers.](/static/chapter1/linear-regression/loss/model-mse.png)

**Figure 9**. MSE loss moves the model closer to the outliers.

![IMAGE: Figure 10. The model is tilted further away from the outliers.](/static/chapter1/linear-regression/loss/model-mae.png)

**Figure 10**. MAE loss keeps the model farther from the outliers.

Note the relationship between the model and the data:

* **MSE**. The model is closer to the outliers but further away from most of
  the other data points.
* **MAE**. The model is further away from the outliers but closer to most of
  the other data points.

**Choose MSE:**

* If you want to heavily penalize large errors.
* If you believe the outliers are important and indicative of true data
  variance that the model should account for.

**Note:** The mathematical properties of
MSE often make optimization smoother. Root Mean Squared Error (RMSE) is
often used to get the error back into the same units as the label.

**Choose MAE:**

* If your dataset has significant outliers that you don't want to overly
  influence the model. MAE is more robust.
* If you prefer a loss function that is more directly interpretable as
  the average error magnitude.

In practice, your metric choice can also depend on the specific business
problem and what kind of errors are more costly.

### Check Your Understanding

Consider the following two plots of a linear model fit to a dataset:

|  |  |
| --- | --- |
| ![IMAGE: A plot of 10 points. A line runs through 6 of the points. 2 points are 1 unit above the line; 2 other points are 1 unit below the line.](/static/chapter1/linear-regression/loss/mse-left.png) | ![IMAGE: A plot of 10 points. A line runs through 8 of the points. 1 point is 2 units above the line; 1 other point is 2 units below the line.](/static/chapter1/linear-regression/loss/mse-right.png) |

Which of the two linear models shown in the preceding plots
has the **higher** Mean Squared Error (MSE) when evaluated
on the plotted data points?

The model on the left.

<details>
<summary>Click to answer</summary>
The six examples on the line incur a total loss of 0. The four
examples not on the line are not very far off the line, so even
squaring their offset still yields a low value: 
$$MSE = \frac{0^2 + 1^2 + 0^2 + 1^2 + 0^2 + 1^2 + 0^2 + 1^2 + 0^2 + 0^2} {10} = 0.4$$
</details>

The model on the right.

<details>
<summary>Click to answer</summary>
The eight examples on the line incur a total loss of 0. However,
although only two points lay off the line, both of those
points are *twice* as far off the line as the outlier points
in the left figure. Squared loss amplifies those differences,
so an offset of two incurs a loss four times as great as an offset
of one: 
$$MSE = \frac{0^2 + 0^2 + 0^2 + 2^2 + 0^2 + 0^2 + 0^2 + 2^2 + 0^2 + 0^2} {10} = 0.8$$
</details>

**Key terms:**

* [Mean absolute error (MAE)](https://developers.google.com/machine-learning/glossary#mean-absolute-error-mae)
* [Mean squared error (MSE)](https://developers.google.com/machine-learning/glossary#mean-squared-error-mse)
* [L1](https://developers.google.com/machine-learning/glossary#l1-loss)
* [L2](https://developers.google.com/machine-learning/glossary#l2-loss)
* [Loss](https://developers.google.com/machine-learning/glossary#loss)
* [Outlier](https://developers.google.com/machine-learning/glossary#outliers)
* [Prediction](https://developers.google.com/machine-learning/glossary#prediction)
