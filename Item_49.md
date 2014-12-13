Item 49: Understand the behavior of the new-handler.
-------------------------------------

首先看一下typedef+函数指针的定义方式。

```
char (*PFun)(int) //定义一个函数指针，未对指针赋值
char glFun(int a){return;}
void main()
{
    PFun=glFun;//对函数指针进行赋值，glFun是函数，但函数名也是一个指针
}

```
上面的写法等同于

```
typedef char (*PFun)(int) //PFun成了一种新的定义，参数为int，返回值为char。
PFun glFun;
```

申明于<new>的一个标准函数库函数：

```
namespcae std{
typedef void (*new_handler)();
new_handler set_new_handler(new_handler p) throw;
}
```

`set_new_handler`用来设置用户使用new时异常调用的用户处理函数。

