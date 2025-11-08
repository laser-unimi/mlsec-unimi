# Overfitting: Model complexity  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/overfitting/model-complexity

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Overfitting: Model complexity Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Simpler models often generalize better to new data than complex models, even if they perform slightly worse on training data.
* Occam's Razor favors simpler explanations and models, prioritizing them over more complex ones.
* Regularization techniques help prevent overfitting by penalizing model complexity during training.
* Model training aims to minimize both loss (errors on training data) and complexity for optimal performance on new data.
* Model complexity can be quantified using functions of model weights, like L1 and L2 regularization.

The previous unit introduced the following model, which miscategorized a lot
of trees in the test set:

![IMAGE: Figure 16. The same image as Figure 13. This is a complex shape that
miscategorizes many trees.]()

**Figure 16.** The misbehaving complex model from the previous unit.

The preceding model contains a lot of complex shapes. Would a simpler
model handle new data better? Suppose you replace the complex model with
a ridiculously simple model--a straight line.

![IMAGE: Figure 17. A straight line model that does an excellent job
separating the sick trees from the healthy trees.]()

**Figure 17.** A much simpler model.

The simple model generalizes better than the complex model on new data. That is,
the simple model made better predictions on the test set than the complex model.

Simplicity has been beating complexity for a long time. In fact, the
preference for simplicity dates back to ancient Greece. Centuries later,
a fourteenth-century friar named William of Occam formalized the preference
for simplicity in a philosophy known as [Occam's
razor](https://wikipedia.org/wiki/Occam%27s_razor). This philosophy
remains an essential underlying principle of many sciences, including
machine learning.

**Note:** Complex models typically outperform simple models on the training set.
However, simple models typically outperform complex models on the test set
(which is more important).

### Exercises: Check your understanding

You are developing a physics equation. Which of the following formulas
conform more closely to Occam's Razor?

A formula with three variables.

Three variables is more Occam-friendly than twelve variables.

A formula with twelve variables.

Twelve variables seems overly complicated, doesn't it?
The two most famous physics formulas of all time (F=ma and
E=mc2) each involve only three variables.

You're on a brand-new machine learning project, about to select your
first features. How many features should you pick?

Pick 1–3 features that seem to have strong predictive power.

It's best for your data collection pipeline to start with only one or
two features. This will help you confirm that the ML model works as intended.
Also, when you build a baseline from a couple of features,
you'll feel like you're making progress!

Pick 4–6 features that seem to have strong predictive power.

You might eventually use this many features, but it's still better to
start with fewer. Fewer features usually means fewer unnecessary
complications.

Pick as many features as you can, so you can start observing which
features have the strongest predictive power.

Start smaller. Every new feature adds a new dimension to your training
dataset. When the dimensionality increases, the volume of the space
increases so fast that the available training data become sparse. The
sparser your data, the harder it is for a model to learn the relationship
between the features that actually matter and the label. This phenomenon
is called "the curse of dimensionality."

## Regularization

Machine learning models must simultaneously meet two conflicting goals:

* Fit data well.
* Fit data as simply as possible.

One approach to keeping a model simple is to penalize complex models; that is,
to force the model to become simpler during training. Penalizing complex
models is one form of **regularization**.

**A regularization analogy:**
Suppose every student in a lecture hall had a little buzzer that emitted
a sound that annoyed the professor.
Students would press the buzzer whenever the professor's lecture became too
complicated. Annoyed, the professor would be forced to simplify the lecture.
The professor would complain, "When I simplify, I'm not being precise enough."
The students would counter with, "The only goal is to explain it simply
enough that I understand it." Gradually, the buzzers would train the professor
to give an appropriately simple lecture, even if the simpler lecture isn't as
sufficiently precise.

### Loss and complexity

So far, this course has suggested that the only goal when training was to
minimize loss; that is:

\\[\text{minimize(loss)}\\]

As you've seen, models focused solely on minimizing loss tend to overfit.
A better training optimization algorithm minimizes some combination of
loss and complexity:

\\[\text{minimize(loss + complexity)}\\]

Unfortunately, loss and complexity are typically inversely related. As
complexity increases, loss decreases. As complexity decreases, loss increases.
You should find a reasonable middle ground where the model makes good
predictions on both the training data and real-world data.
That is, your model should find a reasonable compromise
between loss and complexity.

## What is complexity?

You've already seen a few different ways of quantifying loss. How would
you quantify complexity? Start your exploration through the following exercise:

### Exercise: Check your intuition

So far, we've been pretty vague about what *complexity* actually
is. Which of the following ideas do you think would be reasonable
complexity metrics?

Complexity is a function of the model's weights.

Yes, this is one way to measure some models' complexity.
This metric is called
[**L1 regularization.**](https://developers.google.com/machine-learning/glossary#L1_regularization)

Complexity is a function of the square of the model's weights.

Yes, you can measure some models' complexity this way. This metric
is called
[**L2 regularization**](https://developers.google.com/machine-learning/glossary#L2_regularization).

Complexity is a function of the biases of all the features in the
model.

Bias doesn't measure complexity.

**Key terms:**

* [L1 regularization](https://developers.google.com/machine-learning/glossary#L1_regularization)
* [L2 regularization](https://developers.google.com/machine-learning/glossary#L2_regularization)
* [Regularization](https://developers.google.com/machine-learning/glossary#regularization)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Overfitting (10 min)](/machine-learning/crash-course/overfitting/overfitting)

[Next

L2 regularization (10 min)

arrow\_forward](/machine-learning/crash-course/overfitting/regularization)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]