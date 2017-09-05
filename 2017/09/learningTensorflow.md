## Learning Tensorflow source code

### Overview
On the tensorflow website there are different sections for learning Tensorflow. 
It covers how to use Tensorflow to develop your code. But the section on [Extending](https://www.tensorflow.org/extend/adding_an_op) an Op in Tensorflow is brief. **Please refer the doc before proceeding**. 

#### My approach for understanding the code
1. After going through the white papers which were precisely the content of the docs. I infered the following:
- most of the computation intensive tasks are done in C++ and the wrappers are available in different languages and Python is preferred.
- Tensorflow is low level approach. Keras and Estimators are available to couple number of tasks based on the default values and hence, prototyping is fast but at the same time limits the use-cases where it can be applied. Tensorflow is more general.
- It needs to build the source using bazel which is a way to customize build based on the changes made and hence, build time can be reduced while developing software.
 If the wheel is not generated after the bazel-build step, then run ``` % bazel clean --expunge``` and restart process because bazel builds the executable even when some of the dependencies run into error during download. (Thank me later :P)

2. After skimming through the source code I could only make sense at the high level so to understand the steps involved in creating a new ops I started looking at the issues section of the project and their corresponding solutions so that I can understand the flow of thoughts while creating a new feature. (I am covering for CPU kernels now. I will do for GPU's as an when I will learn.) I am linking the steps from the tensorflow doc to the example issue that I found useful to understand:
	1. [Try solving in python first using the existing ops.](https://github.com/tensorflow/tensorflow/issues/12610)
		1. [Register the new op in a C++ file.](https://github.com/tensorflow/tensorflow/pull/12574)
		2. [Implement the op in C++.](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/core/kernels)
		3. [Create a Python wrapper (optional)](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/estimator/estimator.py).
		4. [Write a function to compute gradients for the op (optional).](https://github.com/tensorflow/tensorflow/issues/12686)
		5. [Test the op.](https://github.com/tensorflow/tensorflow/pull/12645)
