# Datasets: Dividing the original dataset

All good software engineering projects devote considerable energy to
*testing* their apps. Similarly, we strongly recommend testing your
ML model to determine the correctness of its predictions.

## Training, validation, and test sets

You should test a model against a *different* set of examples than those
used to train the model. As you'll learn
[a little later](#additional_problems_with_test_sets), testing
on different examples is stronger proof of your model's fitness than testing
on the same set of examples.
Where do you get those different examples? Traditionally in machine learning,
you get those different examples by splitting the original dataset. You might
assume, therefore, that you should split the original dataset into two subsets:

* A [**training set**](https://developers.google.com/machine-learning/glossary#training-set)
  that the model trains on.
* A [**test set**](https://developers.google.com/machine-learning/glossary#test-set) for evaluation of the
  trained model.

![IMAGE: Figure 8. A horizontal bar divided into two pieces: ~80% of which is the training set and ~20% is the test set.](/static/chapter2/overfitting/dividing-datasets/PartitionTwoSets.png)

**Figure 8.** Not an optimal split.

### Exercise: Check your intuition

Suppose you train on the training set and evaluate on the test set
over multiple rounds. In each round, you use the test set results
to guide how to update hyperparameters and the feature set. Can you
see anything wrong with this approach? Pick only one answer.

Doing many rounds of this procedure might cause the model
to implicitly fit the peculiarities of the test set.

Yes! The more often you use the same test set,
the more likely the model closely fits the test set.
Like a teacher "teaching to the test," the model inadvertently
fits the test set, which might make it harder for the model
to fit real-world data.

This approach is fine. After all, you're training on the
training set and evaluating on a separate test set.

Actually, there's a subtle issue here. Think about what might
gradually go wrong.

This approach is computationally inefficient. Don't change
hyperparameters or feature sets after each round of testing.

Frequent testing is expensive but critical. However, frequent
testing is far less expensive than additional training. Optimizing
hyperparameters and the feature set can dramatically improve
model quality, so always budget time and computational resources
to work on these.

Dividing the dataset into two sets is a decent idea, but
a better approach is to divide the dataset into *three* subsets.
In addition to the training set and the test set, the third subset is:

* A [**validation set**](https://developers.google.com/machine-learning/glossary#validation-set)
  performs the initial testing on the model as it is being trained.

![IMAGE: Figure 9. A horizontal bar divided into three pieces: 70% of which is the training set, 15% the validation set, and 15% the test set](/static/chapter2/overfitting/dividing-datasets/PartitionThreeSets.png)

**Figure 9.** A much better split.

Use the **validation set** to evaluate results from the training set.
After repeated use of the validation set suggests that your model is
making good predictions, use the test set to double-check your model.

The following figure suggests this workflow.
In the figure, "Tweak model" means adjusting anything about the model
—from changing the learning rate, to adding or removing
features, to designing a completely new model from scratch.

![IMAGE: Figure 10. A workflow diagram](/static/chapter2/overfitting/dividing-datasets/workflow_with_validation_set.svg)

**Figure 10.** A good workflow for development and testing.

**Note:** When you transform a feature in your training set, you must make the
*same* transformation in the validation set, test set, and real-world dataset.

The workflow shown in Figure 10 is optimal, but even with that workflow,
test sets and validation sets still "wear out" with repeated use.
That is, the more you use the same data to make decisions about
hyperparameter settings or other model improvements, the less confidence
that the model will make good predictions on new data.
For this reason, it's a good idea to collect more data to "refresh" the test
set and validation set. Starting anew is a great reset.

### Exercise: Check your intuition

You shuffled all the examples in the dataset and divided
the shuffled examples into training, validation, and test
sets. However, the loss value on your test set is so staggeringly low
that you suspect a mistake. What might have gone wrong?

Many of the examples in the test set are duplicates of examples
in the training set.

Yes. This can be a problem in a dataset with a lot of redundant
examples. We strongly recommend deleting duplicate examples from
the test set before testing.

Training and testing are nondeterministic. Sometimes, by chance,
your test loss is incredibly low. Rerun the test to confirm the
result.

Although loss does vary a little on each run, it shouldn't vary so
much that you think you won the machine learning lottery.

By chance, the test set just happened to contain examples that the
model performed well on.

The examples were well shuffled, so this is extremely unlikely.

## Additional problems with test sets

As the previous question illustrates, duplicate examples can affect model evaluation.
After splitting a dataset into training, validation, and test sets,
delete any examples in the validation set or test set that are duplicates of
examples in the training set. The only fair test of a model is against
new examples, not duplicates.

For example, consider a model that predicts whether an email is spam, using
the subject line, email body, and sender's email address as features.
Suppose you divide the data into training and test sets, with an 80-20 split.
After training, the model achieves 99% precision on both the training set and
the test set. You'd probably expect a lower precision on the test set, so you
take another look at the data and discover that many of the examples in the test
set are duplicates of examples in the training set. The problem is that you
neglected to scrub duplicate entries for the same spam email from your input
database before splitting the data. You've inadvertently trained on some of
your test data.

In summary, a good test set or validation set meets all of the
following criteria:

* Large enough to yield statistically significant testing results.
* Representative of the dataset as a whole. In other words, don't pick
  a test set with different characteristics than the training set.
* Representative of the real-world data that the model will encounter
  as part of its business purpose.
* Zero examples duplicated in the training set.

### Exercises: Check your understanding

Given a single dataset with a fixed number of examples,
which of the following statements is true?

Every example used in testing the model is one less example used
in training the model.

Dividing examples into train/test/validation sets is a zero-sum game.
This is the central trade-off.

The number of examples in the test set must be greater than
the number of examples in the validation set.

In theory, the validation set and test test should contain the same
number of examples or nearly so.

The number of examples in the test set must be greater than
the number of examples in the validation set or training set.

The number of examples in the training set is usually greater than
the number of examples in the validation set or test set; however,
there are no percentage requirements for the different sets.

Suppose your test set contains enough examples to perform a
statistically significant test. Furthermore, testing against
the test set yields low loss. However, the model performed
poorly in the real world. What should you do?

Determine how the original dataset differs from real-life data.

Yes. Even the best datasets are only a snapshot of real-life data;
the underlying
[ground truth](https://developers.google.com/machine-learning/glossary#ground-truth)
tends to change over time. Although your test set matched your
training set well enough to suggest good model quality, your
dataset probably doesn't adequately match real-world data.
You might have to retrain and retest against a new dataset.

Retest on the same test set. The test results might have
been an anomaly.

Although retesting might yield slightly different results,
this tactic probably isn't very helpful.

How many examples should the test set contain?

Enough examples to yield a statistically significant test.

Yes. How many examples is that? You'll need to experiment.

At least 15% of the original dataset.

15% may or may not be enough examples.

**Key terms:**

* [Test set](https://developers.google.com/machine-learning/glossary#test-set)
* [Training set](https://developers.google.com/machine-learning/glossary#training-set)
* [Validation set](https://developers.google.com/machine-learning/glossary#validation_set)
