## Learning Tensorflow source code

### Overview
On the tensorflow website there are different sections for learning Tensorflow. 
It covers how to use Tensorflow to develop your code. But the section on [Extending](https://www.tensorflow.org/extend/adding_an_op) an Op in Tensorflow is brief. **Please refer the doc before proceeding**. 

#### My approach for understanding the code
1. After going through the white papers which were precisely the content of the docs. I understood:
- most of the computation intensive tasks are done in C++ and the wrappers are available in different languages and Python is preferred.
- Tensorflow is low level approach. Keras and Estimators are available to couple number of tasks based on the default values and hence, prototyping is fast but at the same time limits the use-cases where it can be applied. Tensorflow is much general.
- It needs to build the source using bazel which is a way to customize build based on the changes made and hence, build time can be reduced while developing software.



I am covering for CPU kernels now. I will do for GPU's as an when I will learn.

It covers the main steps:
1. Register the new op in a C++ file: