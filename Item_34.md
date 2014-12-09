Item 34: Differentiate between inheritance of interface and inheritance of implementation.

--------------------------------------------

```
class Airport {...}
class Airplane{
public:
virtual void fly(const Airport & destination = 0);
...
protected:
    void defaultFly(const Airport & destination);
};

void Airplane::defaultFly(const Airport & destination)
{
     //Fly to default destination
}

class ModelA: public Airplane{
public:
    virtual void fly(const Airport & destination)
    {defaultFly(destination); }
    ...
};

class ModelB: public Airplane{
public:
    virtual void fly(const Airport & destination)
    {defaultFly(destination); }
    ...
}
```

上面的代码中纯虚函数`virtual void fly(const Airport & destination = 0)`就是接口，Airplane类不能用来实例化对象。而`defaultFly(const Airport & destination)`提供了一个默认的实现，也可以在继承类中定义自己的实现。

class ModelA中以内联的形式调用`defaultFly(destination)`.
