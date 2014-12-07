Item 32：Make sure public inheritance models "is-a."
-----------------------------------------------

举例：

class Rectangle{
	public:
	virtual void setHeight(int newHeight);
	virtual void setWidth(int newWidth);
	virtual int height() const;
	virtual int width() const;
};

void makeBigger(Rectangle & r)
{
	int oldHeight=r.height();
	r.setWidth(r.width+10);
	assert(r.height()==oldHeight);
}

class Square: public Rectangle{};
Square s;
assert(s.width()==s.height());
makeBigger(s);
assert(s.width()==s.height());

makeBigger用来改变矩形的长度。而继承后的正方形调用makeBigger后，宽和高不一样，因为断言函数
abort。这里就不能用public继承。

-------------------------------------------

##Reference##

[1].http://www.tuicool.com/articles/6j2yy2z

[2].http://blog.csdn.net/segen_jaa/article/details/8080167
