# TensorFlow

通常会配合 `numpy` 以及 `pandas` 还有 `matplotlib` 一起使用。

``` py
import pandas as pd
import numpy as np
import tensorflow as tf
from matplotlib import pyplot as plt
```

关于 TensorFlow 层级结构的[直观的理解](https://developers.google.com/machine-learning/crash-course/first-steps-with-tensorflow/toolkit)。

---

直到现在的版本 `tensorflow==2.4` 时，使用和安装 tf （的原生 GPU 支持）仍然是一件麻烦的事情。

## 安装

使用 docker 或原生安装。最好设置原生 GPU 支持。

在[使用 GPU](https://www.tensorflow.org/guide/gpu) 时，通常需要设定 Memory Growth 选项，以免出现内存问题。

``` py
# Set memory growth option, see <https://www.tensorflow.org/guide/gpu>
gpus = tf.config.experimental.list_physical_devices('GPU')
if gpus:
  try:
    for gpu in gpus:
      tf.config.experimental.set_memory_growth(gpu, True)
    logical_gpus = tf.config.experimental.list_logical_devices('GPU')
    print(len(gpus), "Physical GPUs,", len(logical_gpus), "Logical GPUs")
  except RuntimeError as e:
    print(e)
```

### docker 安装

docker 安装的参考文章：

- <https://josehoras.github.io/tensorflow-with-gpu-using-docker-and-pycharm/>

### 典型安装

典型安装非常麻烦，但是装上总是有好处的。如果经常使用还是选择典型安装较好。

[典型安装](https://www.tensorflow.org/install/gpu)时，务必遵照[版本需求](https://www.tensorflow.org/install/source#tested_build_configurations)。

可能需要 `apt` hold 住特定的软件版本防止升级。

``` sh
apt list --installed | grep cudnn
sudo apt-mark hold libcudnn8 libcudnn8-dev

sudo apt-mark showhold
sudo apt-mark unhold <package-name>
```

### 测试安装

如果下面三个测试代码都能运行，那么 TensorFlow 的安装基本没有问题。

``` py
import tensorflow as tf

print('CPUs:', tf.config.list_physical_devices('CPU'))
print('GPUs:', tf.config.list_physical_devices('GPU'))
```

``` py
import tensorflow as tf

mnist = tf.keras.datasets.mnist

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation='softmax')
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=5)

model.evaluate(x_test,  y_test, verbose=2)
```

``` py
import tensorflow as tf

from tensorflow.keras.layers import Dense, Flatten, Conv2D
from tensorflow.keras import Model

# Set memory growth option, see <https://www.tensorflow.org/guide/gpu>
gpus = tf.config.experimental.list_physical_devices('GPU')
if gpus:
  try:
    for gpu in gpus:
      tf.config.experimental.set_memory_growth(gpu, True)
    logical_gpus = tf.config.experimental.list_logical_devices('GPU')
    print(len(gpus), "Physical GPUs,", len(logical_gpus), "Logical GPUs")
  except RuntimeError as e:
    print(e)


mnist = tf.keras.datasets.mnist

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

# Add a channels dimension
x_train = x_train[..., tf.newaxis]
x_test = x_test[..., tf.newaxis]

train_ds = tf.data.Dataset.from_tensor_slices(
    (x_train, y_train)).shuffle(10000).batch(32)
test_ds = tf.data.Dataset.from_tensor_slices((x_test, y_test)).batch(32)

class MyModel(Model):
  def __init__(self):
    super(MyModel, self).__init__()
    self.conv1 = Conv2D(32, 3, activation='relu')
    self.flatten = Flatten()
    self.d1 = Dense(128, activation='relu')
    self.d2 = Dense(10, activation='softmax')

  def call(self, x):
    x = self.conv1(x)
    x = self.flatten(x)
    x = self.d1(x)
    return self.d2(x)

model = MyModel()

loss_object = tf.keras.losses.SparseCategoricalCrossentropy()

optimizer = tf.keras.optimizers.Adam()

train_loss = tf.keras.metrics.Mean(name='train_loss')
train_accuracy = tf.keras.metrics.SparseCategoricalAccuracy(name='train_accuracy')

test_loss = tf.keras.metrics.Mean(name='test_loss')
test_accuracy = tf.keras.metrics.SparseCategoricalAccuracy(name='test_accuracy')

@tf.function
def train_step(images, labels):
  with tf.GradientTape() as tape:
    predictions = model(images)
    loss = loss_object(labels, predictions)
  gradients = tape.gradient(loss, model.trainable_variables)
  optimizer.apply_gradients(zip(gradients, model.trainable_variables))

  train_loss(loss)
  train_accuracy(labels, predictions)

@tf.function
def test_step(images, labels):
  predictions = model(images)
  t_loss = loss_object(labels, predictions)

  test_loss(t_loss)
  test_accuracy(labels, predictions)

EPOCHS = 5

for epoch in range(EPOCHS):
  train_loss.reset_states()
  train_accuracy.reset_states()
  test_loss.reset_states()
  test_accuracy.reset_states()

  for images, labels in train_ds:
    train_step(images, labels)

  for test_images, test_labels in test_ds:
    test_step(test_images, test_labels)

  template = 'Epoch {}, Loss: {}, Accuracy: {}, Test Loss: {}, Test Accuracy: {}'
  print (template.format(epoch+1,
                         train_loss.result(),
                         train_accuracy.result()*100,
                         test_loss.result(),
                         test_accuracy.result()*100))
```
