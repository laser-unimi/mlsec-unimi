# Datasets: Labels

This section focuses on [**labels**](https://developers.google.com/machine-learning/glossary#label).

## Direct versus proxy labels

Consider two different kinds of labels:

* **Direct labels**, which are labels identical to the prediction your model
  is trying to make. That is, the prediction your model is trying to make is
  exactly present as a column in your dataset.
  For example, a column named `bicycle owner` would be a direct label for a
  binary classification model that predicts whether or not a person owns
  a bicycle.
* **Proxy labels**, which are labels that are similar—but
  not identical—to the prediction your model is trying to make.
  For example, a person subscribing to Bicycle Bizarre magazine
  probably—but not definitely—owns a bicycle.

Direct labels are generally better than proxy labels. If your dataset
provides a possible direct label, you should probably use it.
Oftentimes though, direct labels aren't available.

Proxy labels are always a compromise—an imperfect approximation of
a direct label. However, some proxy labels are close enough approximations
to be useful. Models that use proxy labels are only as useful as the
connection between the proxy label and the prediction.

Recall that every label must be represented as a floating-point number
in the [**feature vector**](https://developers.google.com/machine-learning/glossary#feature-vector)
(because machine learning is fundamentally just a huge amalgam of mathematical
operations). Sometimes, a direct label exists but can't be easily represented as
a floating-point number in the feature vector. In this case, use a proxy label.

### Exercise: Check your understanding

Your company wants to do the following:

> Mail coupons ("Get 15% off a new bicycle
> helmet") to bicycle owners.

So, your model must do the following:

> Predict which people own a bicycle.

Unfortunately, the dataset doesn't contain a column named `bike owner`.
However, the dataset does contain a column named `recently bought a bicycle`.

Would `recently bought a bicycle` be a good proxy label
or a poor proxy label for this model?

Good proxy label

The column `recently bought a bicycle` is a
relatively good proxy label. After all, most of the people
who buy bicycles now own bicycles. Nevertheless, like all
proxy labels, even very good ones, `recently bought a
bicycle` is imperfect. After all, the person buying
an item isn't always the person using (or owning) that item.
For example, people sometimes buy bicycles as a gift.

Poor proxy label

Like all proxy labels, `recently bought a bicycle`
is imperfect (some bicycles are bought as gifts and given to
others). However, `recently bought a bicycle` is
still a relatively good indicator that someone owns a
bicycle.

## Human-generated data

Some data is **human-generated**; that is, one or more humans examine some
information and provide a value, usually for the label. For example,
one or more meteorologists could examine pictures of the sky and identify
cloud types.

Alternatively, some data is **automatically-generated**. That is, software
(possibly, another machine learning model) determines the value. For example, a
machine learning model could examine sky pictures and automatically identify
cloud types.

This section explores the advantages and disadvantages of human-generated data.

Advantages

* Human raters can perform a wide range of tasks that even sophisticated
  machine learning models may find difficult.
* The process forces the owner of the dataset to develop clear and
  consistent criteria.

Disadvantages

* You typically pay human raters, so human-generated data can be expensive.
* To err is human. Therefore, multiple human raters might have to evaluate the
  same data.

Think through these questions to determine your needs:

* How skilled must your raters be? (For example, must the raters
  know a specific language? Do you need linguists for dialogue or NLP
  applications?)
* How many labeled examples do you need? How soon do you need them?
* What's your budget?

**Always double-check your human raters**. For example, label 1000 examples
yourself, and see how your results match other raters' results.
If discrepancies surface, don't assume your ratings are the correct ones,
especially if a value judgment is involved. If human raters have introduced
errors, consider adding instructions to help them and try again.

#### Click the plus icon to learn more about human-generated data.

Looking at your data by hand is a good exercise regardless of how you
obtained your data. Andrej Karpathy did this on
[ImageNet
and wrote about the experience](http://karpathy.github.io/2014/09/02/what-i-learned-from-competing-against-a-convnet-on-imagenet).

Models can train on a mix of automated and human-generated labels. However,
for most models, an extra set of human-generated labels (which can become stale)
are generally not worth the extra complexity and maintenance.
That said, sometimes the human-generated labels can provide extra
information not available in the automated labels.

---

**Key terms:**

* [Label](https://developers.google.com/machine-learning/glossary#label)
* [Feature vector](https://developers.google.com/machine-learning/glossary#feature-vector)
