Item31：Minimize compilation dependencies between files.

-----------------------------------------------------------------------------------

##Code##

`
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
`

##Reference##

[1].http://blog.csdn.net/ozwarld/article/details/7101974
