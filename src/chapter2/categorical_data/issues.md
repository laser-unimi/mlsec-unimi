# Categorical data: Common issues  |  Machine Learning  |  Google for Developers

Source: https://developers.google.com/machine-learning/crash-course/categorical-data/issues

* [Home](https://developers.google.com/)
* [Products](https://developers.google.com/products)
* [Machine Learning](https://developers.google.com/machine-learning)
* [ML Concepts](https://developers.google.com/machine-learning/crash-course)
* [Crash Course](https://developers.google.com/machine-learning/crash-course/prereqs-and-prework)

Send feedback

# Categorical data: Common issues Stay organized with collections Save and categorize content based on your preferences.



![IMAGE: Spark icon]()

## AI-generated Key Takeaways

outlined\_flag

* Categorical data quality hinges on how categories are defined and labeled, impacting data reliability.
* Human-labeled data, known as "gold labels," is generally preferred for training due to its higher quality, but it's essential to check for human errors and biases.
* Machine-labeled data, or "silver labels," can introduce biases or inaccuracies, necessitating careful quality checks and awareness of potential common-sense violations.
* High-dimensionality in categorical data increases training complexity and costs, leading to techniques like embeddings for dimensionality reduction.

Numerical data is often recorded by scientific instruments or
automated measurements. Categorical data, on the other hand, is often
categorized by human beings or by machine learning (ML) models. *Who* decides
on categories and labels, and *how* they make those decisions, affects the
reliability and usefulness of that data.

## Human raters

Data manually labeled by human beings is often referred to as *gold labels*,
and is considered more desirable than machine-labeled data for training models,
due to relatively better data quality.

This doesn't necessarily mean that any set of human-labeled data is of high
quality. Human errors, bias, and malice can be introduced at the point
of data collection or during data cleaning and processing. Check for them
before training.

Any two human beings may label the same example differently. The difference
between human raters' decisions is called
[**inter-rater
agreement**](https://developers.google.com/machine-learning/glossary#inter-rater-agreement).
You can get a sense of the variance in raters' opinions by using
multiple raters per example and measuring inter-rater agreement.

**Click to learn about inter-rater agreement metrics**

The following are ways to measure inter-rater agreement:

* Cohen's kappa and variants
* Intra-class correlation (ICC)
* Krippendorff's alpha

For details on Cohen's kappa and intra-class correlation, see
[Hallgren
2012](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3402032/). For details on Krippendorff's alpha, see
[Krippendorff 2011](https://www.asc.upenn.edu/sites/default/files/2021-03/Computing%20Krippendorff%27s%20Alpha-Reliability.pdf).

## Machine raters

Machine-labeled data, where categories are automatically determined by one or
more classification models, is often referred to as *silver labels*.
Machine-labeled data can vary widely in quality. Check it not only for accuracy
and biases but also for violations of common sense, reality, and intention. For
example, if a computer-vision model mislabels a photo of a
[chihuahua as a muffin](https://www.freecodecamp.org/news/chihuahua-or-muffin-my-search-for-the-best-computer-vision-api-cbda4d6b425d/),
or a photo of a muffin as a chihuahua, models trained on that labeled data will
be of lower quality.

Similarly, a sentiment analyzer that scores neutral words as -0.25, when 0.0 is
the neutral value, might be scoring all words with an additional negative bias
that is not actually present in the data. An oversensitive toxicity detector
may falsely flag many neutral statements as toxic. Try to get a sense of the
quality and biases of machine labels and annotations in your data before
training on it.

## High dimensionality

Categorical data tends to produce high-dimensional feature vectors; that is,
feature vectors having a large number of elements.
High dimensionality increases training costs and makes training more
difficult. For these reasons, ML experts often seek ways to reduce the number
of dimensions prior to training.

For natural-language data, the main method of reducing dimensionality is
to convert feature vectors to embedding vectors. This is discussed in the
[Embeddings module](/machine-learning/crash-course/embeddings) later in
this course.

**Key terms:**

* [Inter-rater agreement](https://developers.google.com/machine-learning/glossary#inter-rater-agreement)

[Help Center](https://support.google.com/machinelearningeducation)

[Previous

arrow\_back

Vocabulary and one-hot encoding (10 min)](/machine-learning/crash-course/categorical-data/one-hot-encoding)

[Next

Feature crosses (5 min)

arrow\_forward](/machine-learning/crash-course/categorical-data/feature-crosses)






Send feedback

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-08-25 UTC.




Need to tell us more?

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2025-08-25 UTC."],[],[]]