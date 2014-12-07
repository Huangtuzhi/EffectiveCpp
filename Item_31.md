Item31：Minimize compilation dependencies between files.

-----------------------------------------------------------------------------------
一句话总结就是数据从Base类下放到Derived类，调用时由Derived类返回Base类。

##方法一##
把Person分为两个classes，一个class A只提供接口，一个class B负责实现。B在A中private中有个指针定义用来关联实现和接口。
参数由A的构造函数传到B的构造函数里实现赋值。


``` 
#include <string>
#include <memory>
class PersonImpl;
class Date;
class Address;

class Person{
public:
	Person(const std::string &name,const Date& birthday,const Address &addr);
	std::string name() const;
	std::string birthDate() const;
	std::string address() const;

private:
	std::tr1::shared_ptr<PersonImpl> pImpl;
}

Person::Person(const std::string &name,const Date& birthday,const Address &addr):
plmpl(new PersonImpl(name,birthday,addr))
{
	//把Person的成员theName,theBirthday放到PersonImpl中。初始化的时候用PersonImpl来实现，把用户传进来的参数
	//传到PersonImpl类中。
}

std::string Person::name() const
{
	return pImpl->name();
}

class PersonImpl{
	public：
		PersonImpl(const std::string &name,const Date& birthday,const Address &addr):
	theName(name),theBirthDay(birthday),theAddress(addr);
	std::string name() const;
	private：
		std::string theName;
		Data theBirthDay;
		Address theAddress;
}

std::string PersonImpl::name() const
{
	return theName;
}
``` 

---------------------------------

##方法二##
令Person成为抽象基类（Interface Class）。具体的实现定义在继承类RealPerson中。

``` 
class Person{
public:
	virtual ~person();
	virtual std::string name() const=0;
	static std::str1::shared_ptr<Person> create(const std::string &name);
};

class RealPerson:public Person{
public:
	RealPerson(const std::string &name):theName(name){};
	virtual ~RealPerson() const;
private:
	std::string theName；
}；

std::str1::shared_ptr<Person> Person::create(const std::string &name)
{
		return std:tr1:shared_ptr<Person>(new RealPerson(name);
}

void main()
{
	std::string name;
	std::tr1::shared_ptr<Person> pp(Person::create(name));
	std::cout<<pp->name;
}

``` 

##shared_ptr##

先回顾一下智能指针shared_ptr的用法：

由于 C++ 语言没有自动内存回收机制，程序员每次 new 出来的内存都要手动 delete，比如流程太复杂，最终导致没有 delete，异常导致程序过早退出，没有执行 delete 的情况并不罕见，并造成内存泄露。如此c++引入智能指针 ，智能指针即是C++ RAII的一种应用，可用于动态资源管理，资源即对象的管理策略。

类似vector，智能指针也是模板。boost::shared_ptr的管理机制其实并不复杂，就是对所管理的对象进行了引用计数，当新增一个boost::shared_ptr对该对象进行管理时，就将该对象的引用计数加一；减少一个boost::shared_ptr对该对象进行管理时，就将该对象的引用计数减一，如果该对象的引用计数为0的时候，说明没有任何指针对其管理，才调用delete释放其所占的内存。

这样就可以共享资源。


##Reference##

[1].http://blog.csdn.net/ozwarld/article/details/7101974

[2].http://blog.csdn.net/Eric_Jo/article/details/4138548

[3].http://www.cnblogs.com/TianFang/archive/2008/09/19/1294521.html
