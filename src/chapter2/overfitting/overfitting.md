# Overfitting  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting/overfitting

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Overfitting Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Overfitting occurs when a model performs well on training data but poorly on new, unseen data.
* A model is considered to generalize well if it accurately predicts on new data, indicating it hasn't overfit.
* Overfitting can be detected by observing diverging loss curves for training and validation sets on a generalization curve.
* Common causes of overfitting include unrepresentative training data and overly complex models.
* Dataset conditions for good generalization include examples being independent, identically distributed, and stationary, with similar distributions across partitions.

[**Overfitting**](https://developers.google.com/machine-learning/glossary#overfitting) means creating a model
that matches (*memorizes*) the
[**training set**](https://developers.google.com/machine-learning/glossary#training-set) so
closely that the model fails to make correct predictions on new data.
An overfit model is analogous to an invention that performs well in the lab but
is worthless in the real world.

**Tip:**
Overfitting is a common problem in machine learning, not an academic
hypothetical.

In Figure 11, imagine that each geometric shape represents a tree's position
in a square forest. The blue diamonds mark the locations of healthy trees,
while the orange circles mark the locations of sick trees.

![IMAGE: Figure 11. This figure contains about 60 dots, half of which are
healthy trees and the other half sick trees.
The healthy trees are mainly in the northeast quadrant, though a few
healthy trees sneak into the northwest quadrants. The sick trees
are mainly in the southeast quadrant, but a few of the sick trees
spill into other quadrants.]()

**Figure 11.** Training set: locations of healthy and sick trees in a square forest.

Mentally draw any shapes—lines, curves, ovals...anything—to separate the
healthy trees from the sick trees. Then, expand the next line to examine
one possible separation.

#### Expand to see one possible solution (Figure 12).

![IMAGE: Figure 12. The same arrangement of healthy and sick trees as in
Figure 11. However, a model of complex geometric shapes separates
nearly all of the healthy trees from the sick trees.]()

**Figure 12.** A complex model for distinguishing sick from healthy trees.

The complex shapes shown in Figure 12 successfully categorized all but two of
the trees. If we think of the shapes as a model, then this is a fantastic
model.

Or is it? A truly excellent model successfully categorizes *new* examples.
Figure 13 shows what happens when that same model makes predictions on new
examples from the test set:

![IMAGE: Figure 13. A new batch of healthy and sick trees overlaid on the
model shown in Figure 12. The model miscategorizes many of the
trees.]()

**Figure 13.**Test set: a complex model for distinguishing sick from healthy trees.

So, the complex model shown in Figure 12 did a great job on the training set
but a pretty bad job on the test set. This is a classic case of a model
*overfitting* to the training set data.

## Fitting, overfitting, and underfitting

A model must make good predictions on *new* data.
That is, you're aiming to create a model that "fits" new data.

As you've seen, an overfit model makes excellent predictions on the training
set but poor predictions on new data. An
[**underfit**](https://developers.google.com/machine-learning/glossary#underfitting) model
doesn't even make good predictions on the training data. If an overfit model is
like a product that performs well in the lab but poorly in the real world,
then an underfit model is like a product that doesn't even do well in
the lab.

![IMAGE: Figure 14. Cartesian plot. X-axis is labeled 'quality of predictions
on training set.' Y-axis is labeled 'quality of predictions on
real-world data.' A curve starts at the origin and rises gradually,
but then falls just as quickly. The lower-left portion of the curve
(low quality of predictions on real-world data and low quality of
predictions on training set) is labeled 'underfit models.' The
lower-right portion of the curve (low quality of predictions on
real-world data but high quality of predictions on training set)
is labeled 'overfit models.' The peak of the curve (high quality
of predictions on real-world data and medium quality of predictions
on training set) is labeled 'fit models.']()

**Figure 14.** Underfit, fit, and overfit models.

[**Generalization**](https://developers.google.com/machine-learning/glossary#generalization) is the
opposite of overfitting. That is, a model that *generalizes well* makes good
predictions on new data. Your goal is to create a model that generalizes
well to new data.

## Detecting overfitting

The following curves help you detect overfitting:

* loss curves
* generalization curves

A [**loss curve**](https://developers.google.com/machine-learning/glossary#loss-curve) plots a model's loss
against the number of training iterations.
A graph that shows two or more loss curves is called a [**generalization
curve**](https://developers.google.com/machine-learning/glossary#generalization-curve). The following
generalization curve shows two loss curves:

![IMAGE: Figure 15. The loss function for the training set gradually
declines. The loss function for the validation set also declines,
but then it starts to rise after a certain number of iterations.]()

**Figure 15.** A generalization curve that strongly implies overfitting.

Notice that the two loss curves behave similarly at first and then diverge.
That is, after a certain number of iterations, loss declines or
holds steady (converges) for the training set, but increases
for the validation set. This suggests overfitting.

In contrast, a generalization curve for a well-fit model shows two loss curves
that have similar shapes.

## What causes overfitting?

Very broadly speaking, overfitting is caused by one or both of the following
problems:

* The training set doesn't adequately represent real life data (or the
  validation set or test set).
* The model is too complex.

## Generalization conditions

A model trains on a training set, but the real test of a model's worth is how
well it makes predictions on new examples, particularly on real-world data.
While developing a model, your test set serves as a proxy for real-world data.
Training a model that generalizes well implies the following dataset conditions:

* Examples must be
  [**independently and identically distributed**](https://developers.google.com/machine-learning/glossary#independently-and-identically-distributed-i.i.d),
  which is a fancy way of saying that your
  examples can't influence each other.
* The dataset is
  [**stationary**](https://developers.google.com/machine-learning/glossary#stationarity), meaning the
  dataset doesn't change significantly over time.
* The dataset partitions have the same distribution.
  That is, the examples in the training set are statistically similar to the
  examples in the validation set, test set, and real-world data.

Explore the preceding conditions through the following exercises.

## Exercises: Check your understanding

Consider the following dataset partitions.
![IMAGE: A horizontal bar divided into three pieces: 70% of the bar
is the training set, 15% the validation set, and 15%
the test set]()
What should you do to ensure that the examples in the training set
have a similar statistical distribution to the examples in
the validation set and the test set?

Shuffle the examples in the dataset extensively before
partitioning them.

Yes. Good shuffling of examples makes partitions much more
likely to be statistically similar.

Sort the examples from earliest to most recent.

If the examples in the dataset are not stationary, then
sorting makes the partitions *less*
similar.

Do nothing. Given enough examples, the law of averages
naturally ensures that the distributions will be
statistically similar.

Unfortunately, this is not the case. The examples
in certain sections of the dataset may differ from those in other
sections.

A streaming service is developing a model to predict the popularity
of potential new television shows for the next three years. The
streaming service plans to train the model on a dataset
containing hundreds of millions of examples, spanning the previous
ten years. Will this model encounter a problem?

Probably. Viewers' tastes change in ways that past behavior can't
predict.

Yes. Viewer tastes are not stationary. They constantly change.

Definitely not. The dataset is large enough to make good
predictions.

Unfortunately, viewers' tastes are nonstationary.

Probably not. Viewers' tastes change in predictably cyclical ways.
Ten years of data will enable the model to make good predictions
on future trends.

Although certain aspects of entertainment are somewhat cyclical, a
model trained from past entertainment history will almost certainly
have trouble making predictions about the next few years.

A model aims to predict the time it takes for people to walk a mile
based on weather data (temperature, dew point, and
precipitation) collected over one year in a city whose weather varies
significantly by season. Can you build and test a model from this
dataset, even though the weather readings change dramatically by
season?

Yes

Yes, it is possible to build and test a model from this dataset.
You just have to ensure that the data is partitioned equally, so
that data from all four seasons is distributed equally into the
different partitions.

No

Assuming this dataset contains enough examples of temperature, dew
point, and precipitation, then you can build and test a model from
this dataset. You just have to ensure that the data is partitioned
equally, so that data from all four seasons is distributed equally
into the different partitions.

### Challenge exercise

You are creating a model that predicts the ideal date for riders to buy a
train ticket for a particular route. For example, the model might recommend
that users buy their ticket on July 8 for a train that departs July 23.
The train company updates prices hourly, basing their updates on a variety
of factors but mainly on the current number of available seats. That is:

* If a lot of seats are available, ticket prices are typically low.
* If very few seats are available, ticket prices are typically high.

Your model exhibits low
loss on the validation set and the test set but sometimes makes
terrible predictions on real-world data. Why?

Click here to see the answer

**Answer:** The real world model is struggling with a
**[feedback loop](https://developers.google.com/machine-learning/glossary#feedback-loop)**.

For example, suppose the model recommends that users buy tickets on July 8.
Some riders who use the model's recommendation buy their tickets at 8:30
in the morning on July 8. At 9:00, the train company raises prices because
fewer seats are now available. Riders using the model's recommendation have
altered prices. By evening, ticket prices might be much higher than in the
morning.

**Key terms:**

* [Feedback loop](https://developers.google.com/machine-learning/glossary#feedback-loop)
* [Generalization](https://developers.google.com/machine-learning/glossary#generalization)
* [Generalization curve](https://developers.google.com/machine-learning/glossary#generalization-curve)
* [Independently and identically distributed (i.i.d)](https://developers.google.com/machine-learning/glossary#independently-and-identically-distributed-i.i.d)
* [Loss curve](https://developers.google.com/machine-learning/glossary#loss-curve)
* [Overfitting](https://developers.google.com/machine-learning/glossary#overfitting)
* [Stationarity](https://developers.google.com/machine-learning/glossary#stationarity)
* [Training set](https://developers.google.com/machine-learning/glossary#training-set)
* [Underfitting](https://developers.google.com/machine-learning/glossary#underfitting)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Generalization (5 min)](/machine-learning/crash-course/overfitting/generalization)

[Next

Model complexity (10 min)

arrow\_forward](/machine-learning/crash-course/overfitting/model-complexity)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]