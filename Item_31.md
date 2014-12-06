Item31：Minimize compilation dependencies between files.

-----------------------------------------------------------------------------------

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


##Reference##

[1].http://blog.csdn.net/ozwarld/article/details/7101974

[2].http://blog.csdn.net/Eric_Jo/article/details/4138548
