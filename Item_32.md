Item 32：Make sure public inheritance models "is-a."
-----------------------------------------------

先回顾一下智能指针shared_ptr的用法：

由于 C++ 语言没有自动内存回收机制，程序员每次 new 出来的内存都要手动 delete，比如流程太复杂，最终导致没有 delete，异常导致
程序过早退出，没有执行 delete 的情况并不罕见，并造成内存泄露。如此c++引入智能指针 ，智能指针即是C++ RAII的一种应用，
可用于动态资源管理，资源即对象的管理策略。



-------------------------------------------

##Reference##

[1].http://www.tuicool.com/articles/6j2yy2z

[2].http://blog.csdn.net/segen_jaa/article/details/8080167
