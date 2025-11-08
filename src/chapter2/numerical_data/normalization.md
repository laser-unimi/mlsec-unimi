# Numerical data: Normalization

After examining your data through statistical and visualization techniques,
you should transform your data in ways that will help your model train more
effectively. The goal of
[**normalization**](https://developers.google.com/machine-learning/glossary#normalization) is to transform
features to be on a similar scale. For example, consider the following two
features:

* Feature `X` spans the range 154 to 24,917,482.
* Feature `Y` spans the range 5 to 22.

These two features span very different ranges. Normalization might manipulate
`X` and `Y` so that they span a similar range, perhaps 0 to 1.

Normalization provides the following benefits:

* Helps models *converge more quickly* during training.
  When different features have different ranges, gradient descent can
  "bounce" and slow convergence. That said, more advanced optimizers like
  [Adagrad](https://developers.google.com/machine-learning/glossary#adagrad)
  and [Adam](https://arxiv.org/abs/1412.6980) protect against this problem by
  changing the effective learning rate over time.
* Helps models *infer better predictions*.
  When different features have different ranges, the resulting
  model might make somewhat less useful predictions.
* Helps *avoid the "NaN trap"* when feature values are very high.
  [NaN](https://wikipedia.org/wiki/NaN) is an abbreviation for
  *not a number*. When a value in a model exceeds the
  floating-point precision limit, the system sets the value to `NaN` instead
  of a number. When one number in the model becomes a NaN, other numbers in
  the model also eventually become a NaN.
* Helps the model *learn appropriate weights* for each feature.
  Without feature scaling, the model pays too much attention
  to features with wide ranges and not enough attention to features with
  narrow ranges.

We recommend normalizing numeric features covering distinctly
different ranges (for example, age and income).
We also recommend normalizing a single numeric feature that covers a wide range,
such as `city population.`

Warning: If you normalize a feature during training, you must also normalize
that feature when making predictions.

Consider the following two features:

* Feature `A`'s lowest value is -0.5 and highest is +0.5.
* Feature `B`'s lowest value is -5.0 and highest is +5.0.

Feature `A` and Feature `B` have relatively narrow spans. However, Feature `B`'s
span is 10 times wider than Feature `A`'s span. Therefore:

* At the start of training, the model assumes that Feature `B` is ten times
  more "important" than Feature `A`.
* Training will take longer than it should.
* The resulting model may be suboptimal.

The overall damage due to not normalizing will be relatively small; however,
we still recommend normalizing Feature A and Feature B to the same scale,
perhaps -1.0 to +1.0.

Now consider two features with a greater disparity of ranges:

* Feature `C`'s lowest value is -1 and highest is +1.
* Feature `D`'s lowest value is +5000 and highest is +1,000,000,000.

If you don't normalize Feature `C` and Feature `D`, your model will likely
be suboptimal. Furthermore, training will take much longer to
converge or even fail to converge entirely!

This section covers three popular normalization methods:

* linear scaling
* Z-score scaling
* log scaling

This section additionally covers
[**clipping**](https://developers.google.com/machine-learning/glossary#clipping). Although not a true
normalization technique, clipping does tame unruly numerical features into
ranges that produce better models.

## Linear scaling

**[Linear scaling](https://developers.google.com/machine-learning/glossary#scaling)** (more commonly
shortened to just **scaling**) means converting floating-point values from
their natural range into a standard range—usually 0 to 1 or
-1 to +1.

#### Click the icon to see the math.

Use the following formula to scale to the standard range
0 to 1, inclusive:

\\[ x' = (x - x\_{min}) / (x\_{max} - x\_{min}) \\]

where:

* \\(x'\\) is the scaled value.
* \\(x\\) is the original value.
* \\(x\_{min}\\) is the lowest value in the dataset of this feature.
* \\(x\_{max}\\) is the highest value in the dataset of this feature.

For example, consider a feature named `quantity` whose natural
range spans 100 to 900. Suppose the natural value of `quantity` in a
particular example is 300. Therefore, you can calculate the normalized value
of 300 as follows:

* \\(x\\) = 300
* \\(x\_{min}\\) = 100
* \\(x\_{max}\\) = 900

```
x' = (300 - 100) / (900 - 100)
x' = 200 / 800
x' = 0.25
```

---

Linear scaling is a good choice when all of the following conditions are met:

* The lower and upper bounds of your data don't change much over time.
* The feature contains few or no outliers, and those outliers aren't
  extreme.
* The feature is approximately uniformly distributed across its range.
  That is, a histogram would show roughly even bars for most values.

Suppose human `age` is a feature. Linear scaling is a good normalization
technique for `age` because:

* The approximate lower and upper bounds are 0 to 100.
* `age` contains a relatively small percentage of outliers. Only about 0.3% of
  the population is over 100.
* Although certain ages are somewhat better represented than others, a large
  dataset should contain sufficient examples of all ages.

**Note:** Most real-world features do not meet all of the criteria for linear
scaling. Z-score scaling is typically a better normalization choice than
linear scaling.

### Exercise: Check your understanding

Suppose your model has a feature named `net_worth` that holds the net
worth of different people. Would linear scaling be a good normalization
technique for `net_worth`? Why or why not?

<details>
<summary>Click to see the answer</summary>
**Answer:** Linear scaling would be a poor choice for normalizing
`net_worth`. This feature contains many outliers, and the values
are not uniformly distributed across its primary range. Most people would
be squeezed within a very narrow band of the overall range.
</details>

---

## Z-score scaling

A **Z-score** is the number of standard deviations a value is from the mean.
For example, a value that is 2 standard deviations *greater* than the mean
has a Z-score of +2.0. A value that is 1.5 standard deviations *less* than
the mean has a Z-score of -1.5.

Representing a feature with **Z-score scaling** means storing that feature's
Z-score in the feature vector. For example, the following figure shows two
histograms:

* On the left, a classic normal distribution.
* On the right, the same distribution normalized by Z-score scaling.

![IMAGE: Figure 4. Two histograms: both showing normal distributions with the identical distribution. The first histogram, which contains raw data, has a mean of 200 and a standard deviation of 30. The second histogram, which contains a Z-score version of the first distribution, has a mean of 0 and a standard deviation of 1.]()

**Figure 4.** Raw data (left) versus Z-score (right) for a normal
distribution.

Z-score scaling is also a good choice for data like that shown in
the following figure, which has only a vaguely normal distribution.

![IMAGE: Figure 5. Two histograms of identical shape, each showing a steep rise to a plateau and then a relatively quick descent followed by gradual decay. One histogram illustrates the distribution of the raw data; the other histogram illustrates the distribution of the raw data when normalized by Z-score scaling. The values on the X-axis of the two histograms are very different. The raw data histogram spans the domain 0 to 29,000, while the Z-score scaled histogram ranges from -1 to about +4.8]()

**Figure 5.** Raw data (left) versus Z-score scaling (right) for a
non-classic normal distribution.

Use the following formula to normalize a value, \\(x\\), to
its Z-score:

\\[ x' = (x - μ) / σ \\]

where:

* \\(x'\\) is the Z-score.
* \\(x\\) is the raw value; that is, \\(x\\) is the value you are normalizing.
* \\(μ\\) is the mean.
* \\(σ\\) is the standard deviation.

For example, suppose:

* mean = 100
* standard deviation = 20
* original value = 130

Therefore:

```
  Z-score = (130 - 100) / 20
  Z-score = 30 / 20
  Z-score = +1.5
```

---

<details>
<summary>Click here to learn more about normal distributions.</summary>
In a classic normal distribution:

* At least 68.27% of data has a Z-score between -1.0 and +1.0.
* At least 95.45% of data has a Z-score between -2.0 and +2.0.
* At least 99.73% of data has a Z-score between -3.0 and +3.0.
* At least 99.994% of data has a Z-score between -4.0 and +4.0.

So, data points with a Z-score less than -4.0 or more than +4.0
are rare, but are they truly outliers? Since *outliers* is a concept
without a strict definition, no one can say for sure.
Note that a dataset with a sufficiently large number of examples will
almost certainly contain at least a few of these "rare" examples.
For example, a feature with one billion examples conforming to a
classic normal distribution could have as many as 60,000 examples
with a score outside the range -4.0 to +4.0.
</details>

Z-score is a good choice when the data follows a normal distribution or
a distribution somewhat like a normal distribution.

Note that some distributions might be normal within the bulk of their
range, but still contain extreme outliers. For example, nearly all of the
points in a `net_worth` feature might fit neatly into 3 standard deviations,
but a few examples of this feature could be hundreds of standard deviations
away from the mean. In these situations, you can combine Z-score scaling with
another form of normalization (usually clipping) to handle this situation.

### Exercise: Check your understanding

Suppose your model trains on a feature named `height` that holds the adult
heights of ten million women. Would Z-score scaling be a good normalization
technique for `height`? Why or why not?

<details>
<summary>Click to see the answer</summary>
**Answer:** Z-score scaling would be a good normalization technique
for `height` because this feature conforms to a normal distribution.
Ten million examples implies a lot of outliers—probably enough outliers for
the model to learn patterns on very high or very low Z-scores.
</details>

---

## Log scaling

Log scaling computes the logarithm of the raw value. In theory, the
logarithm could be any base; in practice, log scaling usually calculates
the natural logarithm (ln).

Use the following formula to normalize a value, \\(x\\), to
its log:

\\[ x' = ln(x) \\]

where:

* \\(x'\\) is the natural logarithm of \\(x\\).
* original value = 54.598

Therefore, the log of the original value is about 4.0:

```
  4.0 = ln(54.598)
```

---

Log scaling is helpful when the data conforms to a *power law* distribution.
Casually speaking, a power law distribution looks as follows:

* Low values of `X` have very high values of `Y`.
* As the values of `X` increase, the values of `Y` quickly decrease.
  Consequently, high values of `X` have very low values of `Y`.

Movie ratings are a good example of a power law distribution. In the following
figure, notice:

* A few movies have lots of user ratings. (Low values of `X` have high
  values of `Y`.)
* Most movies have very few user ratings. (High values of `X` have low
  values of `Y`.)

Log scaling changes the distribution, which helps train a model that will
make better predictions.

![IMAGE: Figure 6. Two graphs comparing raw data versus the log of raw data. The raw data graph shows a lot of user ratings in the head, followed by a long tail. The log graph has a more even distribution.]()

**Figure 6.** Comparing a raw distribution to its log.

As a second example, book sales conform to a power law distribution because:

* Most published books sell a tiny number of copies, maybe one or two hundred.
* Some books sell a moderate number of copies, in the thousands.
* Only a few *bestsellers* will sell more than a million copies.

Suppose you are training a linear model to find the relationship
of, say, book covers to book sales. A linear model training on raw values would
have to find something about book covers on books that sell a million copies
that is 10,000 more powerful than book covers that sell only 100 copies.
However, log scaling all the sales figures makes the task far more feasible.
For example, the log of 100 is:

```
  ~4.6 = ln(100)
```

while the log of 1,000,000 is:

```
  ~13.8 = ln(1,000,000)
```

So, the log of 1,000,000 is only about three times larger than the log of 100.
You probably *could* imagine a bestseller book cover being about three times
more powerful (in some way) than a tiny-selling book cover.

## Clipping

[**Clipping**](https://developers.google.com/machine-learning/glossary#clipping) is a technique to
minimize the influence of extreme outliers. In brief, clipping usually caps
(reduces) the value of outliers to a specific maximum value. Clipping is a
strange idea, and yet, it can be very effective.

For example, imagine a dataset containing a feature named `roomsPerPerson`,
which represents the number of rooms (total rooms divided
by number of occupants) for various houses. The following plot shows that over
99% of the feature values conform to a normal distribution (roughly, a mean of
1.8 and a standard deviation of 0.7). However, the feature contains
a few outliers, some of them extreme:

![IMAGE: Figure 7. A plot of roomsPerPerson in which nearly all the values are clustered between 0 and 4, but there's a verrrrry long tail reaching all the way out to 17 rooms per person]()

**Figure 7.** Mainly normal, but not completely normal.

How can you minimize the influence of those extreme outliers? Well, the
histogram is not an even distribution, a normal distribution, or a power law
distribution. What if you simply *cap* or *clip* the maximum value of
`roomsPerPerson` at an arbitrary value, say 4.0?

![IMAGE: A plot of roomsPerPerson in which all values lie between 0 and
4.0. The plot is bell-shaped, but there's an anomalous hill at 4.0]()

**Figure 8.** Clipping feature values at 4.0.

Clipping the feature value at 4.0 doesn't mean that your model ignores all
values greater than 4.0. Rather, it means that all values that were greater
than 4.0 now become 4.0. This explains the peculiar hill at 4.0. Despite
that hill, the scaled feature set is now more useful than the original data.

Wait a second! Can you really reduce every outlier value to some arbitrary upper
threshold? When training a model, yes.

You can also clip values after applying other forms of normalization.
For example, suppose you use Z-score scaling, but a few outliers have
absolute values far greater than 3. In this case, you could:

* Clip Z-scores greater than 3 to become exactly 3.
* Clip Z-scores less than -3 to become exactly -3.

Clipping prevents your model from overindexing on unimportant data. However,
some outliers are actually important, so clip values carefully.

## Summary of normalization techniques

The best normalization technique is one that
works well in practice, so try new ideas if you think they'll work well on
your feature distribution.

| Normalization technique | Formula | When to use |
| --- | --- | --- |
| Linear scaling | \\[ x' = \frac{x - x\_{min}}{x\_{max} - x\_{min}} \\] | When the feature is mostly uniformly distributed across range. **Flat-shaped** |
| Z-score scaling | \\[ x' = \frac{x - μ}{σ}\\] | When the feature is normally distributed (peak close to mean). **Bell-shaped** |
| Log scaling | \\[ x' = log(x)\\] | When the feature distribution is heavy skewed on at least either side of tail. **Heavy Tail-shaped** |
| Clipping | If \\(x > max\\), set \\(x' = max\\)  If \\(x < min\\), set \\(x' = min\\) | When the feature contains extreme outliers. |

## Exercise: Test your knowledge

Which technique would be most suitable for normalizing a feature with
the following distribution?

![IMAGE: A histogram showing a cluster of data with values in the range 0 to 200,000. The number of data points gradually increases for the range from 0 to 100,000 and then gradually decreases from 100,000 to 200,000.]()

Z-score scaling

The data points generally conform to a normal distribution, so Z-score
scaling will force them into the range –3 to +3.

Linear scaling

Review the discussions of the normalization techniques on this page,
and try again.

Log scaling

Review the discussions of the normalization techniques on this page,
and try again.

Clipping

Review the discussions of the normalization techniques on this page,
and try again.

Suppose you are developing a model that predicts a data center's
productivity based on the temperature measured inside the data center.
Almost all of the `temperature` values in your dataset fall
between 15 and 30 (Celsius), with the following exceptions:

* Once or twice per year, on extremely hot days, a few values between
  31 and 45 are recorded in `temperature`.
* Every 1,000th point in `temperature` is set to 1,000
  rather than the actual temperature.

Which would be a reasonable normalization technique for
`temperature`?

Clip the outlier values between 31 and 45, but delete the outliers with
a value of 1,000

The values of 1,000 are mistakes, and should be deleted rather than
clipped.

The values between 31 and 45 are legitimate data points.
Clipping would probably be a good idea for these values, assuming the
dataset doesn't contain enough examples in this temperature range to
train the model to make good predictions. However, during inference,
note that the clipped model would therefore make the same prediction for
a temperature of 45 as for a temperature of 35.

Clip all the outliers

Review the discussions of the normalization techniques on this page,
and try again.

Delete all the outliers

Review the discussions of the normalization techniques on this page,
and try again.

Delete the outlier values between 31 and 45, but clip the
outliers with a value of 1,000.

Review the discussions of the normalization techniques on this page,
and try again.

**Key terms:**

* [Clipping](https://developers.google.com/machine-learning/glossary#clipping)
* [NaN trap](https://developers.google.com/machine-learning/glossary#NaN_trap)
* [Normalization](https://developers.google.com/machine-learning/glossary#normalization)
* [Scaling](https://developers.google.com/machine-learning/glossary#scaling)
* [Z-score normalization](https://developers.google.com/machine-learning/glossary#Z-score-normalization)
