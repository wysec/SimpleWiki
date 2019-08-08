
## 简介

首先，需要明白 TensorFlow：

- 使用图 (graph) 来表示计算任务。
- 在被称之为 会话 (Session) 的上下文 (context) 中执行图。
- 使用 tensor 表示数据。tensor是由一系列任意维度的矩阵构成。例如

```
3 # 这是一个维度为0的tensor，这是一个标量，它的大小是[]。
[1. ,2., 3.] # 这是一个维度为1的tensor，这是一个矢量，它的大小是[3]
[[1., 2., 3.], [4., 5., 6.]] # 这是一个维度为2的tensor。这是一个矩阵，它的大小是[2, 3]
[[[1., 2., 3.]], [[7., 8., 9.]]] # 这是一个维度为3的tensor，它的大小是[2, 1, 3]
```

- 通过 变量 (Variable) 维护状态。
- 使用 feed 和 fetch 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据。

TensorFlow 是一个编程系统，使用图来表示计算任务。 图中的节点被称之为 op (operation 的缩写)。一个 op 获得 0 个或多个 Tensor，执行计算，产生 0 个或多个 Tensor。每个 Tensor 是一个类型化的多维数组。例如，你可以将一小组图像集表示为一个四维浮点数数组，这四个维度分别是 [batch, height, width, channels]。

一个 TensorFlow 图描述了计算的过程。为了进行计算，图必须在 会话 里被启动。会话 将图的 op 分发到诸如 CPU 或 GPU 之类的 设备 上， 同时提供执行 op 的方法。这些方法执行后，将产生的 tensor 返回。 在 Python 语言中，返回的 tensor 是 numpy ndarray 对象；在 C 和 C++ 语言中， 返回的 tensor 是 tensorflow::Tensor 实例。

## 基础

Tensorflow程序通常被组织成一个构建阶段和一个执行阶段。在构建阶段，op的执行步骤被描述成一个图。在执行阶段，使用会话执行图中的op。

### 构建图

构建图的第一步, 是创建源 op (source op)。源 op 不需要任何输入。例如：常量 (Constant)。 源 op 的输出被传递给其它 op 做运算。

Python 库中，op 构造器的返回值代表被构造出的 op 的输出。 这些返回值可以传递给其它 op 构造器作为输入。

TensorFlow Python 库有一个默认图 (default graph)。op 构造器可以为其增加节点。 这个默认图对 许多程序来说已经足够用了。

```python
import tensorflow as tf

# 创建一个常量和两个变量op并被作为三个节点加到默认图中
const = tf.constant(2.0, name="const")
b = tf.Variable(2.0, name="b")
c = tf.Variable(1.0, dtype= tf.float32, name="c")

# 创建操作符
d = tf.add(b, c, name = "d")
e = tf.add(c, const, name = "e")
a = tf.multiply(d, e, name = "a")

# 如果定义了变量，那么需要对变量进行初始化
init_op = tf.global_variables_initializer()
```

### 计算图

构造阶段完成后，才能在会话中启动图。启动图的第一步是创建一个Session对象。如果没有任何参数，会话构造器将启动默认图。

```python
# 启动默认图时要创建Session
# Session对象在使用完成或需要关闭以释放资源。除了显示调用close外，也可以使用“with”代码块来自动完成关闭动作。
with tf.Session() as sess:
    # 执行变量初始化
    sess.run(init_op)
    # 执行op进行计算
    a_out = sess.run(a)
    print("Variable a is {}".format(a_out))
```

## 问题
执行上面程序是出现这样的问题提示。

> Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2

在程序文件前面加上`os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'`。


## 参考资料
[TensorFlow基本用法](http://www.tensorfly.cn/tfdoc/get_started/basic_usage.html)

[TensorFlow入门教程](https://www.jianshu.com/p/69ca199052da)

[TensorFlow 教程 - 新手入门笔记](https://blog.csdn.net/Toormi/article/details/53609245)