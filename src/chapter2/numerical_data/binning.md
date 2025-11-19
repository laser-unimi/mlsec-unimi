# Numerical data: Binning
**Binning** (also called **bucketing**) is a
[**feature engineering**](https://developers.google.com/machine-learning/glossary#feature_engineering)
technique that groups different numerical subranges into *bins* or
[***buckets***](https://developers.google.com/machine-learning/glossary#bucketing).
In many cases, binning turns numerical data into categorical data.
For example, consider a [**feature**](https://developers.google.com/machine-learning/glossary#feature)
named `X` whose lowest value is 15 and
highest value is 425. Using binning, you could represent `X` with the
following five bins:

* Bin 1: 15 to 34
* Bin 2: 35 to 117
* Bin 3: 118 to 279
* Bin 4: 280 to 392
* Bin 5: 393 to 425

Bin 1 spans the range 15 to 34, so every value of `X` between 15 and 34
ends up in Bin 1. A model trained on these bins will react no differently
to `X` values of 17 and 29 since both values are in Bin 1.

The [**feature vector**](https://developers.google.com/machine-learning/glossary#feature_vector) represents
the five bins as follows:

| Bin number | Range | Feature vector |
| --- | --- | --- |
| 1 | 15-34 | [1.0, 0.0, 0.0, 0.0, 0.0] |
| 2 | 35-117 | [0.0, 1.0, 0.0, 0.0, 0.0] |
| 3 | 118-279 | [0.0, 0.0, 1.0, 0.0, 0.0] |
| 4 | 280-392 | [0.0, 0.0, 0.0, 1.0, 0.0] |
| 5 | 393-425 | [0.0, 0.0, 0.0, 0.0, 1.0] |

Even though `X` is a single column in the dataset, binning causes a model
to treat `X` as *five* separate features. Therefore, the model learns
separate weights for each bin.

Binning is a good alternative to [**scaling**](https://developers.google.com/machine-learning/glossary#scaling)
or [**clipping**](https://developers.google.com/machine-learning/glossary#clipping) when either of the
following conditions is met:

* The overall *linear* relationship between the feature and the
  [**label**](https://developers.google.com/machine-learning/glossary#label) is weak or nonexistent.
* When the feature values are clustered.

Binning can feel counterintuitive, given that the model in the
previous example treats the values 37 and 115 identically. But when
a feature appears more *clumpy* than linear, binning is a much better way to
represent the data.

## Binning example: number of shoppers versus temperature

Suppose you are creating a model that predicts the number of
shoppers by the outside temperature for that day. Here's a plot of the
temperature versus the number of shoppers:

![IMAGE: Figure 9. A scatter plot of 45 points. The 45 points naturally cluster into three groups. ](/static/chapter2/numerical/binning/binning_temperature_vs_shoppers.png)

**Figure 9.** A scatter plot of 45 points.

The plot shows, not surprisingly, that the number of shoppers was highest when
the temperature was most comfortable.

You could represent the feature as raw values: a temperature of 35.0 in the
dataset would be 35.0 in the feature vector. Is that the best idea?

During training, a linear regression model learns a single weight for each
feature. Therefore, if temperature is represented as a single feature, then a
temperature of 35.0 would have five times the influence (or one-fifth the
influence) in a prediction as a temperature of 7.0. However, the plot doesn't
really show any sort of linear relationship between the label and the
feature value.

The graph suggests three clusters in the following subranges:

* Bin 1 is the temperature range 4-11.
* Bin 2 is the temperature range 12-26.
* Bin 3 is the temperature range 27-36.

![IMAGE: Figure 10. The same scatter plot of 45 points as in the previous figure, but with vertical lines to make the bins more obvious.](/static/chapter2/numerical/binning/binning_temperature_vs_shoppers_divided_into_3_bins.png)

**Figure 10.** The scatter plot divided into three bins.

The model learns separate weights for each bin.

While it's possible to create more than three bins, even a separate bin for
each temperature reading, this is often a bad idea for the following reasons:

* A model can only learn the association between a bin and a label if there
  are enough examples in that bin. In the given example, each of the 3 bins
  contains at least 10 examples, which *might* be sufficient for training.
  With 33 separate bins,
  none of the bins would contain enough examples for the model to train on.
* A separate bin for each temperature results in
  33 separate temperature features. However, you typically should *minimize*
  the number of features in a model.

### Exercise: Check your understanding

The following plot shows the median home price for each 0.2 degrees of
latitude for the mythical country of Freedonia:

![IMAGE: Figure 11. A plot of home values per latitude. The lowest house value is about 327 and the highest is 712. The latitudes span 41.0 to 44.8, with a dot representing the median house value for every 0.2 degrees of latitude. The pattern is highly irregular, but with two distinct clusters (one cluster between latitude 41.0 and 41.8, and another cluster between latitude 42.6 and 43.4).](/static/chapter2/numerical/binning/MedianHouseValueByLatitude.png)

**Figure 11.** Median home value per 0.2 degrees latitude.

The graphic shows a nonlinear pattern between home value and latitude,
so representing latitude as its floating-point value is unlikely to help
a model make good predictions. Perhaps bucketing latitudes would be a better
idea?

What would be the best bucketing strategy?

Don't bucket.

Given the randomness of most of the plot, this is probably the
best strategy.

Create four buckets:

* 41.0 to 41.8
* 42.0 to 42.6
* 42.8 to 43.4
* 43.6 to 44.8

It would be hard for a model to find a single predictive weight for
all the homes in the second bin or the fourth bin, which contain
few examples.

Make each data point its own bucket.

This would only be helpful if the training set contains enough
examples for each 0.2 degrees of latitude. In general, homes
tend to cluster near cities and be relatively scarce in other
places.

## Quantile Bucketing

**Quantile bucketing** creates bucketing boundaries such that the number
of examples in each bucket is exactly or nearly equal. Quantile bucketing
mostly hides the outliers.

To illustrate the problem that quantile bucketing solves, consider the
equally spaced buckets shown in the following figure, where each
of the ten buckets represents a span of exactly 10,000 dollars.
Notice that the bucket from 0 to 10,000 contains dozens of examples
but the bucket from 50,000 to 60,000 contains only 5 examples.
Consequently, the model has enough examples to train on the 0 to 10,000
bucket but not enough examples to train on for the 50,000 to 60,000 bucket.

![IMAGE: Figure 13. A plot of car price versus the number of cars sold at that price. The number of cars sold peaks at a price of 6,000. Above a price of 6,000, the number of cars sold generally decreases, with very few cars sold between a price of 40,000 to 60,000. The plot is divided into 6 equally-sized buckets, each with a range of 10,000. So, the first bucket contains all the cars sold between a price of 0 and a price of 10,000, the second bucket contains all the cars sold between a price of 10,001 and 20,000, and so on. The first bucket contain many examples; each subsequent bucket contains fewer examples.](/static/chapter2/numerical/binning/NeedsQuantileBucketing.png)

**Figure 13.** Some buckets contain a lot of cars; other buckets contain
very few cars.

In contrast, the following figure uses quantile bucketing to divide car prices
into bins with approximately the same number of examples in each bucket.
Notice that some of the bins encompass a narrow price span while others
encompass a very wide price span.

![IMAGE: Figure 14. Same as previous figure, except with quantile buckets. That is, the buckets now have different sizes. The first bucket contains the cars sold from 0 to 4,000, the second bucket contains the cars sold from 4,001 to 6,000. The sixth bucket contains the cars sold from 25,001 to 60,000. The number of cars in each bucket is now about the same.](/static/chapter2/numerical/binning/QuantileBucketing.png)

**Figure 14.** Quantile bucketing gives each bucket about the same
number of cars.

Bucketing with equal intervals works for many data
distributions. For skewed data,
however, try quantile bucketing. Equal intervals give extra
information space to the long tail while compacting the large torso
into a single bucket. Quantile buckets give extra information space to the
large torso while compacting the long tail into a single bucket.
**Key terms:**

* [Binning](https://developers.google.com/machine-learning/glossary#binning)
* [Bucketing](https://developers.google.com/machine-learning/glossary#bucketing)
* [Clipping](https://developers.google.com/machine-learning/glossary#clipping)
* [Feature](https://developers.google.com/machine-learning/glossary#feature)
* [Feature engineering](https://developers.google.com/machine-learning/glossary#feature_engineering)
* [Feature vector](https://developers.google.com/machine-learning/glossary#feature_vector)
* [Label](https://developers.google.com/machine-learning/glossary#label)
* [Scaling](https://developers.google.com/machine-learning/glossary#scaling)
