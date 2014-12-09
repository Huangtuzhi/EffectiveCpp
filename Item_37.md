Item 37: Never redefine a function's inherited default parameter value.

------------------------------------------------------------------------------

```

class Shape{
public:
    enum ShapeColor {Red, Green, Blue};
    void draw(ShapeColor color = Red) const
    {
        doDraw(color); //调用一个virtual
    }
    ...
private:
    virtual void doDraw(ShapeColor color) const = 0;//真正的工作在此处完成
};

class Rectangle: public Shape{
public:
...
private:
    virtual void doDraw(ShapeColor color) const;
    ...
}

```

以上是所谓的NVI（non-virtual interface）方法。

virtual函数是动态绑定的（dynamically bound)，而缺省参数值却是静态绑定（statically bound)。
