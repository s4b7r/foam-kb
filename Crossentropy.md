# Crossentropy

Loss term for machine learning / neural nets.

$-\frac{1}{N} \sum_{i=1}^{N} y_i\ log(p(y_i)) + (1-y_i)\ log(1-p(y_i))$

## "from logits"

Tensorflow asks for `from_logits` on [Binary Crossentropy](https://www.tensorflow.org/versions/r2.0/api_docs/python/tf/keras/losses/BinaryCrossentropy). The documentation states:

> Whether to interpret y_pred as a tensor of logit values. By default, we assume that y_pred contains probabilities (i.e., values in [0, 1]). Note: Using from_logits=True may be more numerically stable.

If the input to Binary Crossentropy is not passed through e.g. Sigmoid or Softmax, it is *from logits*. This means, the "raw" output values of the model.

In oposition, after Sigmoid activation or Softmax (and maybe some others) the values represent actual probabilities, meaning they sum up to $1$. That values are *not from logits*.

This can sometimes be a bit confusing, when Sigmoid activation is seen as a functional part of the last layer and not as a scaling / normalizing function for the purpose of getting probabilities which sum up to $1$.

[This article explains](https://towardsdatascience.com/sigmoid-activation-and-binary-crossentropy-a-less-than-perfect-match-b801e130e31):

> In Deep Learning, logits usually and unfortunately means the ‘raw’ outputs of the last layer of a classification network, that is, the output of the layer before it is passed to an activation/normalization function, e.g. the sigmoid. Raw outputs may take on any value. 

[Some](https://stackoverflow.com/questions/41455101/what-is-the-meaning-of-the-word-logits-in-tensorflow) [more](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a) [infor-](https://stackoverflow.com/a/53418478)[mation](https://stackoverflow.com/questions/52125924/why-does-sigmoid-crossentropy-of-keras-tensorflow-have-low-precision)

### Technical detail

Because of the underlying calculations there can be numerical instabilities in the combination of Sigmoid and Binary Crossentropy, if done wrong. Thus, Tensorflow will actually ignore Sigmoid activation in the last layer and combine the calculation of Sigmoid and Binary Crossentropy internally.

https://github.com/tensorflow/tensorflow/blob/v2.0.0/tensorflow/python/keras/losses.py#L348-L406

https://github.com/tensorflow/tensorflow/blob/64c3d382cadf7bbe8e7e99884bede8284ff67f56/tensorflow/python/keras/losses.py#L180

https://github.com/tensorflow/tensorflow/blob/64c3d382cadf7bbe8e7e99884bede8284ff67f56/tensorflow/python/keras/losses.py#L983

https://github.com/tensorflow/tensorflow/blob/64c3d382cadf7bbe8e7e99884bede8284ff67f56/tensorflow/python/keras/backend.py#L4559

https://github.com/tensorflow/tensorflow/blob/64c3d382cadf7bbe8e7e99884bede8284ff67f56/tensorflow/python/ops/nn_impl.py#L112
