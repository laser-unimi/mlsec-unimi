# Overfitting: L2 regularization  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting/regularization

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Overfitting: L2 regularization Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* L2 regularization is a technique used to reduce model complexity and prevent overfitting by penalizing large weights.
* A regularization rate (lambda) controls the strength of regularization, with higher values leading to simpler models and lower values increasing the risk of overfitting.
* Early stopping is an alternative regularization method that involves ending training before the model fully converges to prevent overfitting.
* Finding the right balance between learning rate and regularization rate is crucial for optimal model performance, as they influence weights in opposite directions.

[**L2 regularization**](https://developers.google.com/machine-learning/glossary#l2-regularization)
is a popular regularization metric, which uses the following formula:

\\[L\_2\text{ regularization } = {w\_1^2 + w\_2^2 + ... + w\_n^2}\\]

For example, the following table shows the calculation of L2
regularization for a model with six weights:

|  | Value | Squared value |
| --- | --- | --- |
| w1 | 0.2 | 0.04 |
| w2 | -0.5 | 0.25 |
| w3 | 5.0 | 25.0 |
| w4 | -1.2 | 1.44 |
| w5 | 0.3 | 0.09 |
| w6 | -0.1 | 0.01 |
|  |  | **26.83** = total |

Notice that weights close to zero don't affect L2 regularization
much, but large weights can have a huge impact. For example, in the
preceding calculation:

* A single weight (w3) contributes about 93% of the
  total complexity.
* The other five weights collectively contribute only about 7% of the
  total complexity.

L2 regularization encourages weights *toward* 0, but never pushes
weights all the way to zero.

### Exercises: Check your understanding

If you use L2 regularization while training a model, what
will typically happen to the overall complexity of the model?

The overall complexity of the system will probably drop.

Since L2 regularization encourages weights towards 0,
the overall complexity will probably drop.

The overall complexity of the model will probably stay
constant.

This is very unlikely.

The overall complexity of the model will probably increase.

This is unlikely. Remember that L2 regularization
encourages weights towards 0.

If you use L2 regularization while training a model,
some features will be removed from the model.

True

Although L2 regularization may make some weights very
small, it will never push any weights all the way to zero.
Consequently, all features will still contribute something to
the model.

False

L2 regularization never pushes weights all the way to
zero.

## Regularization rate (lambda)

As noted, training attempts to minimize some combination of loss and complexity:

\\[\text{minimize(loss} + \text{ complexity)}\\]

Model developers tune the overall impact of complexity on model training
by multiplying its value by a scalar called the
[**regularization rate**](https://developers.google.com/machine-learning/glossary#regularization-rate).
The Greek character lambda typically symbolizes the regularization rate.

That is, model developers aim to do the following:

\\[\text{minimize(loss} + \lambda \text{ complexity)}\\]

A high regularization rate:

* Strengthens the influence of regularization, thereby reducing the chances of
  overfitting.
* Tends to produce a histogram of model weights having the following
  characteristics:
  + a normal distribution
  + a mean weight of 0.

A low regularization rate:

* Lowers the influence of regularization, thereby increasing the chances of
  overfitting.
* Tends to produce a histogram of model weights with a flat distribution.

For example, the histogram of model weights for a high regularization rate
might look as shown in Figure 18.

![IMAGE: Figure 18. Histogram of a model's weights with a mean of zero and
a normal distribution.]()

**Figure 18.** Weight histogram for a high regularization rate.
Mean is zero. Normal distribution.

In contrast, a low regularization rate tends to yield a flatter histogram, as
shown in Figure 19.

![IMAGE: Figure 19. Histogram of a model's weights with a mean of zero that
is somewhere between a flat distribution and a normal
distribution.]()

**Figure 19.** Weight histogram for a low regularization rate.
Mean may or may not be zero.

**Note:** Setting the regularization rate to zero removes regularization completely.
In this case, training focuses exclusively on minimizing loss, which
poses the highest possible overfitting risk.

### Picking the regularization rate

The ideal regularization rate produces a model that generalizes well to
new, previously unseen data.
Unfortunately, that ideal value is data-dependent,
so you must do some
tuning.

### Early stopping: an alternative to complexity-based regularization

[**Early stopping**](https://developers.google.com/machine-learning/glossary#early-stopping) is a
regularization method that doesn't involve a calculation of complexity.
Instead, early stopping simply means ending training before the model
fully converges. For example, you end training when the loss curve
for the validation set starts to increase (slope becomes positive).

Although early stopping usually increases training loss, it can decrease
test loss.

Early stopping is a quick, but rarely optimal, form of regularization.
The resulting model is very unlikely to be as good as a model trained
thoroughly on the ideal regularization rate.

### Finding equilibrium between learning rate and regularization rate

[**Learning rate**](https://developers.google.com/machine-learning/glossary#learning-rate) and
regularization rate tend to pull weights in opposite
directions. A high learning rate often pulls weights *away from* zero;
a high regularization rate pulls weights *towards* zero.

If the regularization rate is high with respect to the learning rate,
the weak weights tend to produce a model that makes poor predictions.
Conversely, if the learning rate is high with respect to the regularization
rate, the strong weights tend to produce an overfit model.

Your goal is to find the equilibrium between learning rate and
regularization rate. This can be challenging. Worst of all, once you find
that elusive balance, you may have to ultimately change the learning rate.
And, when you change the learning rate, you'll again have to find the ideal
regularization rate.

**Key terms:**

* [Early stopping](https://developers.google.com/machine-learning/glossary#early-stopping)
* [L1 regularization](https://developers.google.com/machine-learning/glossary#L1_regularization)
* [L2 regularization](https://developers.google.com/machine-learning/glossary#L2_regularization)
* [Learning rate](https://developers.google.com/machine-learning/glossary#learning-rate)
* [Regularization](https://developers.google.com/machine-learning/glossary#regularization)
* [Regularization rate](https://developers.google.com/machine-learning/glossary#regularization-rate)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Model complexity (10 min)](/machine-learning/crash-course/overfitting/model-complexity)

[Next

Interpreting loss curves (10 min)

arrow\_forward](/machine-learning/crash-course/overfitting/interpreting-loss-curves)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]