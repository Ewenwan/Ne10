# README

## What’s Ne10?
Ne10 is a library of common, useful functions that have been heavily optimised for ARM-based CPUs equipped with [NEON](https://www.arm.com/products/processors/technologies/neon.php) SIMD capabilities. It provides consistent, well-tested behaviour, allowing for painless integration into a wide variety of applications. The library currently focuses primarily around math, signal processing, image processing, and physics functions.

Ne10是一个单独的开源库，可以把它直接嵌入到工程里面去（目前支持linux，android，ios），直接调用里面的函数。Ne10已实现一些接口，可分为4个模块：dsp、math、imgproc、physics。比如dsp中目前就已封装了fft，fir，irr算法函数接口，用户直接调用这些接口函数就可以实现相应算法。Ne10中的所有接口函数既有基于neon实现又有基于c语言实现，这样保证了Ne10库的可移植性。当平台支持neon时，则调用neon函数，否则调用c函数。

Ne10 是由ARM主导开发的一个开源软件库。该库旨在提供一系列通用的，基于ARM NEON架构并且经过深度优化的函数集合。通过调用该库函数可以让软件开发人员免于编写重复的底层汇编代码，同时也能充分利用ARM NEON SIMD指令的并行运算能力。Ne10主要包含math, dsp以及新添的imgproc三个功能模块：

* l. math 数学模块：主要包含矢量/矩阵数学运算。
* 2. dsp 数字信号处理模块：主要包含FFT快速傅立叶变换，以及部分FIR/IIR滤波函数。
* 3. imgproc 图像处理模块：主要包含图像缩放，旋转等图像后处理函数。

Ne10主要侧重于矩阵和向量的数学运算；而math-neon主要侧重于三角函数、对数、指数等复杂运算。



## Building 编译 [![CircleCI](https://circleci.com/gh/projectNe10/Ne10.svg?style=svg)](https://circleci.com/gh/projectNe10/Ne10)
Out of the box, Ne10 supports the Linux, Android, and iOS platforms. For instructions on building Ne10 for these platforms, please consult the build instructions in 编译指导 [`building.md`](https://github.com/projectNe10/Ne10/tree/master/doc/building.md#building-ne10). It is possible to use the library on other platforms (or, indeed, “without a platform”), however you may have to fiddle with some of the build configuration files.

## 使用

在自己的项目中使用Ne10时，要在代码中include “NE10.h”。并把Ne10的inc目录中的几个.h文件添加到自己项目的头文件目录中(以保证软件编译通过)。使用动态库调用方式时，要先将libNE10.so.10软链接为libNE10.so，然后向makefile添加动态库的-L链接命令（以保证软件链接通过）。同时在嵌入式机器的文件系统的/usr/lib目录中加入动态库libNE10.so.10（以保证项目软件运行时能找到动态库）。在调用Ne10的接口函数之前一定要先调用ne10_init()来初始化Ne10的接口函数，在这里Ne10就会查询当前平台是否支持neon，从而选择初始化neon函数还是c函数。

Once Ne10 has been built, it can be linked against just like any other C library. To link C code against Ne10, for instance, the compiler must first be aware of Ne10's library and header files — those within `build/modules/` and `inc/`. To do this, these files can be copied to the standard directories used by compilation tools by running `make install`, or by installing Ne10 from a package manager. Following this, you can simply include `Ne10.h` in your C code, and ask the compiler to link against the `NE10` library (e.g. with `-lNE10`).

## Documentation 文档
Ne10’s official documentation is generated from [doxygen](https://www.stack.nl/~dimitri/doxygen/) annotations in the source code. As such, these documents can be generated locally from the codebase by running `doxygen` within the `doc` directory (producing results in `doc/html`), or viewed remotely as [hosted copies available over the Internet](http://projectne10.github.io/Ne10/doc/modules.html).

We also have a handful of carefully prepared sample code snippets in the [`samples/`](https://github.com/projectNe10/Ne10/tree/master/samples) directory that outline how Ne10 can be used to accomplish a number of common tasks. These include example programs to perform the [FFT](https://github.com/projectNe10/Ne10/tree/master/samples/NE10_sample_complex_fft.c), [FIR](https://github.com/projectNe10/Ne10/tree/master/samples/NE10_sample_fir.c), and [matrix multiply](https://github.com/projectNe10/Ne10/tree/master/samples/NE10_sample_matrix_multiply.c) operations.

## Contributing 贡献
Ne10 welcomes and encourages external contributions of any and all forms. If you’ve found a bug or have a suggestion, please don’t hesitate to detail these in the [official issue tracker](https://github.com/projectNe10/Ne10/issues). For those looking to get their hands dirty and contribute code (the best kind of contribution!), please see [`CONTRIBUTING.md`](https://github.com/projectNe10/Ne10/tree/master/CONTRIBUTING.md#contributing-to-project-ne10) for more details.

## Quick Links

- [Official website](http://projectne10.org/)
- [Source repository](https://github.com/projectNe10/Ne10)
- [Issue tracker](https://github.com/projectNe10/Ne10/issues)
- [Doxygen documentation](http://projectne10.github.io/Ne10/doc/modules.html)
- [Coding style guidelines](https://github.com/projectNe10/Ne10/wiki/Ne10-Coding-Style)

## Call for Use Cases

Find Project Ne10 useful? You can help us justify spending more engineering resources on the project! Please email us, outlining how you are using the project in your applications.

Want us to help cross-promote your product using Ne10 at developer events? We’re also looking for Ne10 use cases to show at conferences and meetups.

