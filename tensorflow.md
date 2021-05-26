# tensorflow

## Datasets

### Interleaving multiple Datasets

```python
ds0 = tf.data.Dataset.range(0, 10, 2)
ds1 = tf.data.Dataset.range(1, 10, 2)

# Zip combines an element from each input into a single element, and flat_map
# enables you to map the combined element into two elements, then flattens the
# result.
dataset = tf.data.Dataset.zip((ds0, ds1)).flat_map(
    lambda x0, x1: tf.data.Dataset.from_tensors(x0).concatenate(
        tf.data.Dataset.from_tensors(x1)))
```

Source. https://stackoverflow.com/a/47344405
