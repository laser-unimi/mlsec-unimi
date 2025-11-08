# Classification: Multi-class classification

Multi-class classification can be treated as an extension of
**binary classification**
to more than two classes. If each example can only be
assigned to one class, then the classification problem can be handled as a
binary classification problem, where one class contains one of the multiple
classes, and the other class contains all the other classes put together.
The process can then be repeated for each of the original classes.

For example, in a three-class multi-class classification problem,
where you're classifying examples with the labels **A**, **B**, and
**C**, you could turn the problem into two separate binary classification
problems. First, you might create a binary classifier that categorizes examples
using the label **A+B** and the label **C**. Then, you could create a second
binary classifier that reclassifies the examples that are labeled **A+B**
using the label **A** and the label **B**.

An example of a multi-class problem is a handwriting classifier that takes
an image of a handwritten digit and decides which digit, 0-9, is represented.

If class membership isn't exclusive, which is to say, an example can be
assigned to multiple classes, this is known as a *multi-label* classification
problem.

**Key terms:**

* [Binary classification](https://developers.google.com/machine-learning/glossary#binary_classification)
