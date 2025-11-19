# Overfitting: Interpreting loss curves

Machine learning would be much simpler if all your
[**loss curves**](https://developers.google.com/machine-learning/glossary#loss_curve)
looked like this the first time you trained your model:

![IMAGE: Figure 20. A plot showing the ideal loss curve when training a machine learning model.](/static/chapter2/overfitting/loss-curves/metric-curve-ideal.svg)

**Figure 20.** An ideal loss curve.

Unfortunately, loss curves are often challenging to interpret. Use your
intuition about loss curves to solve the exercises on this page.

## Exercise 1: Oscillating loss curve

![IMAGE: Figure 21. A loss curve (loss on the y-axis; number of training steps on the x-axis) in which the loss doesn't flatten out. Instead, loss oscillates erratically.](/static/chapter2/overfitting/loss-curves/metric-curve-ex03.svg)

**Figure 21.** Oscillating loss curve.

What **three** things could you do to try improve the loss curve
shown in Figure 21?

Check your data against a data schema to detect bad examples, and
then remove the bad examples from the training set.

Yes, this is a good practice for all models.

Reduce the learning rate.

Yes, reducing learning rate is often a good idea when debugging a
training problem.

Reduce the training set to a tiny number of trustworthy examples.

Although this technique sounds artificial, it is actually a good
idea. Assuming that the model converges on the small set of
trustworthy examples, you can then gradually add more examples,
perhaps discovering which examples cause the loss curve to
oscillate.

Increase the number of examples in the training set.

This is a tempting idea, but it is extremely unlikely to fix
the problem.

Increase the learning rate.

In general, avoid increasing the learning rate when a model's
learning curve indicates a problem.

## Exercise 2. Loss curve with a sharp jump

![IMAGE: Figure 22. A loss curve plot that shows the loss decreasing up to a certain number of training steps and then suddenly increasing with further training steps.](/static/chapter2/overfitting/loss-curves/metric-curve-ex02.svg)

**Figure 22.** Sharp rise in loss.

Which **two** of the following statements identify possible
reasons for the exploding loss shown in Figure 22?

The input data contains one or more NaNs—for example, a value
caused by a division by zero.

This is more common than you might expect.

The input data contains a burst of outliers.

Sometimes, due to improper shuffling of batches, a batch might
contain a lot of outliers.

The learning rate is too low.

A very low learning rate might increase training time, but it is
not the cause of the strange loss curve.

The regularization rate is too high.

True, a very high regularization could prevent a model from
converging; however, it won't cause the strange loss curve
shown in Figure 22.

## Exercise 3. Test loss diverges from training loss

![IMAGE: Figure 23. The training loss curve appears to converge, but the validation loss begins to rise after a certain number of training steps.](/static/chapter2/overfitting/loss-curves/metric-curve-ex01.svg)

**Figure 23.** Sharp rise in validation loss.

Which **one** of the following statements best identifies the
reason for this difference between the loss curves of the training
and test sets?

The model is overfitting the training set.

Yes, it probably is. Possible solutions:

* Make the model simpler, possibly by reducing the number
  of features.
* Increase the regularization rate.
* Ensure that the training set and test set are statistically
  equivalent.

The learning rate is too high.

If the learning rate were too high, the loss curve for the training set
would likely not have behaved as it did.

## Exercise 4. Loss curve gets stuck

![IMAGE: Figure 24. A plot of a loss curve showing the loss beginning to converge with training but then displaying repeated patterns that look like a rectangular wave.](/static/chapter2/overfitting/loss-curves/metric-curve-ex05.svg)

**Figure 24.** Chaotic loss after a certain number of steps.

Which **one** of the following statements is the most likely
explanation for the erratic loss curve shown in Figure 24?

The training set is not shuffled well.

This is a possibility. For example, a training set that contains 100
images of dogs followed by 100 images of cats may cause loss
to oscillate as the model trains. Ensure that you shuffle
examples sufficiently.

The regularization rate is too high.

This is unlikely to be the cause.

The training set contains too many features.

This is unlikely to be the cause.

**Key terms:**

* [Batch](https://developers.google.com/machine-learning/glossary#batch)
* [Example](https://developers.google.com/machine-learning/glossary#example)
* [Feature](https://developers.google.com/machine-learning/glossary#feature)
* [Learning rate](https://developers.google.com/machine-learning/glossary#learning-rate)
* [Loss curve](https://developers.google.com/machine-learning/glossary#loss_curve)
* [Outliers](https://developers.google.com/machine-learning/glossary#outliers)
* [Overfitting](https://developers.google.com/machine-learning/glossary#overfitting)
* [Regularization](https://developers.google.com/machine-learning/glossary#regularization)
* [Regularization rate](https://developers.google.com/machine-learning/glossary#regularization-rate)
* [Test set](https://developers.google.com/machine-learning/glossary#test-set)
* [Training set](https://developers.google.com/machine-learning/glossary#training-set)
* [Validation set](https://developers.google.com/machine-learning/glossary#validation_set)
