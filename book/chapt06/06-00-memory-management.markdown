# 第六章 内存管理

内存是计算机非常关键的部件之一，是暂时存储程序以及数据的空间，CPU只有有限的寄存器可以用于
存储计算数据，而大部分的数据都是存储在内存中的，程序运行都是在内存中进行的。和CPU计算能力一样，
内存也是决定计算效率的一个关键部分。

计算中的资源中主要包含：CPU计算能力，内存资源以及I/O。现代计算机为了充分利用资源，
而出现了多任务操作系统，通过进程调度来共享CPU计算资源，通过虚拟存储来分享内存存储能力。
本章的内存管理中不会介绍操作系统级别的虚拟存储技术，而是关注在应用层面：
如何高效的利用有限的内存资源。

目前除了使用C/C++等这类的低层编程语言以外，很多编程语言都将内存管理移到了语言之后，
例如Java, 各种脚本语言:PHP/Python/Ruby等等，程序手动维护内存的成本非常大，
而这些脚本语言或新型语言都专注于特定领域，这样能将程序员从内存管理中解放出来专注于业务的实现。
虽然程序员不需要手动维护内存，而在程序运行过程中内存的使用还是要进行管理的，
内存管理的工作也就编程语言实现程序员的工作了。

内存管理的主要工作是尽可能**高效的利用内存**。

内存的使用操作包括申请内存，销毁内存，修改内存的大小等。
如果申请了内存在使用完后没有及时释放则可能会造成内存泄露，如果这种情况出现在常驻程序中，
久而久之，程序会把机器的内存耗光。所以对于类似于PHP这样没有低层内存管理的语言来说，
内存管理是其至关重要的一个模块，它在很大程度上决定了程序的执行效率。

在PHP层面来看，定义的变量、类、函数等实体在运行过程中都会涉及到内存的申请和释放，
例如变量可能会在超出作用域后会进行销毁，在计算过程中会产生的临时数据等都会有内存操作，
像类对象，函数定义等数据则会在请求结束之后才会被释放。在这过程中何时申请内存及释放内存就比较关键了。
PHP从开始就有一套属于自己的内存管理机制，在5.3之前使用的是经典的引用计数技术，
但引用计数存在一定的技术缺陷，在PHP5.3之后，引入了新的垃圾回收机制，至此，PHP的内存管理机制更加完善。

本章将介绍PHP语言实现中的内存管理技术实现。
