Model "has-a" or “is-implemented-in-terms-of" through composition.

----------------------------------
以下就是复合类型中的has-a关系，Person包含了预先定义的类。

```
class Address{...}
class PhoneNumber{...}
class Person{
    public:
        //...
    private:
        std::string name;
        Address address;
        PhoneNumber voiceNumber;
        PhoneNumber faxNumber;
};
```

下面是is-implemented-in-terms-of关系,Set根据List实现。

```
template <class T>
class Set{
    public:
        bool member(const T& item) const;
        void insert(const T& item);
        void remove(const T& item);
        std::size_t size() const;
    private:
        std::List<T> rep;
};

template<typename T>
bool Set<T>::member(const T& item) const
{
    return std::find(rep.begin(), rep.end(), item) != rep.end();
}

template<typename T>
void Set<T>::insert(const T& item)
{
    if(!member(item)) rep.push_back(item);
}

template<typename T>
void Set<T>::remove(const T& item)
{
    typename std::List<T>::iterator it = std::find(rep.begin(), rep.end(). item);
    if(it !=rep.end()) rep.erash(it);
}

template<typename T>
std::size_t Set<T>::size() const
{
    return rep.size();
}
```


-----------------------------------------

##Reference##
[1].http://blog.csdn.net/hbhhww/article/details/4157799
