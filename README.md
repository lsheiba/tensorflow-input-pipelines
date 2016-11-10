# TensorFlow Input Pipelines

Use these TensorFlow(v0.11) pipelines to automatically download and easily fetch batches of data and labels from some of the most used datasets in Deep Learning. The implementations are threaded, efficient, can be randomized and also include large datasets such as imagenet. 

# Current datasets are supported
- MNIST
- CIFAR-10
- CIFAR-100
- SVHN
- Stanford Cars 196
- imagenet (no automatic data download, but a shell script is provided in utils/imagenet_download/)

(more datasets will be added soon ...)

# Usage Example
```python
import tensorflow as tf
sess = tf.Session()

with tf.device('/cpu:0'):
  from datasets.svhn import svhn_data
  d = svhn_data(batch_size=256, sess=sess)
  image_batch_tensor, target_batch_tensor = d.build_train_data_tensor()

image_batch, target_batch = sess.run([image_batch_tensor, target_batch_tensor])
print(image_batch.shape)
print(target_batch.shape)
```

A CNN training script template is provided with the following features:
- easy switchin of datasets
- separate training and testing streams
- continous console log 
- test-set evaluation after every epoch
- automatically saves the best performing model parameters
- automatically decreases the learning rate after if there is no improvement in accuracy
- evaluate top 1 and top n accuracies
- easy parameter loading from a previous save point to continue training
- prints a confusion matrix in your console
