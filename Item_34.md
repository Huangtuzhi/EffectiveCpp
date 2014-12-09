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
    {defaultFlay(destination); }
    ...
};

class ModelB: public Airplane{
public:
    virtual void fly(const Airport & destination){defaultFly(destination); }
    ...
}

```
