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
