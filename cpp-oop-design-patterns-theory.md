# Object-Oriented Programming and Design Patterns in C++

## OOP Principles

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data and code. The four main principles of OOP are Encapsulation, Inheritance, Polymorphism, and Abstraction.

### 1. Encapsulation

Encapsulation is the bundling of data and the methods that operate on that data within a single unit (object). It restricts direct access to some of an object's components, which is a means of preventing accidental interference and misuse of the methods and data.

Key concepts:
- Data hiding
- Access specifiers (public, private, protected)
- Getter and setter methods

Example in C++:

```cpp
class BankAccount {
private:
    double balance;

public:
    BankAccount(double initialBalance) : balance(initialBalance) {}

    bool deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return true;
        }
        return false;
    }

    bool withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }

    double getBalance() const {
        return balance;
    }
};
```

In this example, `balance` is a private member, encapsulated within the `BankAccount` class. It can only be accessed or modified through the public methods, ensuring controlled access to the account balance.

### 2. Inheritance

Inheritance is a mechanism where you can derive a class from another class for a hierarchy of classes that share a set of attributes and methods. It promotes code reusability and establishes a relationship between a more general base class and a more specialized derived class.

Key concepts:
- Base class (parent) and derived class (child)
- `protected` access specifier
- Method overriding

Example in C++:

```cpp
class Animal {
protected:
    std::string name;

public:
    Animal(const std::string& name) : name(name) {}
    virtual void speak() const {
        std::cout << name << " makes a sound." << std::endl;
    }
};

class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {}
    void speak() const override {
        std::cout << name << " barks." << std::endl;
    }
};
```

Here, `Dog` inherits from `Animal`, reusing the `name` attribute and overriding the `speak` method.

### 3. Polymorphism

Polymorphism allows objects of different classes to be treated as objects of a common base class. It enables you to work with objects of derived classes through base class pointers or references.

Key concepts:
- Virtual functions
- Runtime polymorphism (dynamic binding)
- Override keyword (C++11 and later)

Example in C++:

```cpp
class Shape {
public:
    virtual double area() const = 0;
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}
    double area() const override {
        return M_PI * radius * radius;
    }
};

class Rectangle : public Shape {
private:
    double width, height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}
    double area() const override {
        return width * height;
    }
};

// Usage
void printArea(const Shape& shape) {
    std::cout << "Area: " << shape.area() << std::endl;
}

int main() {
    Circle circle(5);
    Rectangle rectangle(4, 5);

    printArea(circle);     // Calls Circle::area()
    printArea(rectangle);  // Calls Rectangle::area()
}
```

This example demonstrates polymorphism through the use of the virtual `area()` function, which is overridden in derived classes.

### 4. Abstraction

Abstraction is the process of hiding complex implementation details and showing only the necessary features of an object. It helps in reducing programming complexity and effort.

Key concepts:
- Abstract classes
- Pure virtual functions
- Interfaces (implemented using abstract classes in C++)

Example in C++:

```cpp
class AbstractDatabaseConnector {
public:
    virtual void connect() = 0;
    virtual void disconnect() = 0;
    virtual void executeQuery(const std::string& query) = 0;
};

class MySQLConnector : public AbstractDatabaseConnector {
public:
    void connect() override {
        std::cout << "Connecting to MySQL database..." << std::endl;
    }

    void disconnect() override {
        std::cout << "Disconnecting from MySQL database..." << std::endl;
    }

    void executeQuery(const std::string& query) override {
        std::cout << "Executing MySQL query: " << query << std::endl;
    }
};
```

Here, `AbstractDatabaseConnector` provides an abstraction for database operations, which `MySQLConnector` implements.

## Design Patterns

Design patterns are typical solutions to common problems in software design. They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

### Creational Patterns

Creational patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.

#### 1. Singleton

The Singleton pattern ensures a class has only one instance and provides a global point of access to it.

Key concepts:
- Private constructor
- Static instance
- Lazy initialization

Example in C++:

```cpp
class DatabaseConnection {
private:
    static DatabaseConnection* instance;
    std::string connection;

    DatabaseConnection() : connection("") {}

public:
    static DatabaseConnection* getInstance() {
        if (instance == nullptr) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    void connect() {
        if (connection.empty()) {
            std::cout << "Connecting to database..." << std::endl;
            connection = "Connected";
        }
    }
};

DatabaseConnection* DatabaseConnection::instance = nullptr;
```

#### 2. Factory

The Factory pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate.

Key concepts:
- Factory method
- Product interface
- Concrete products

Example in C++:

```cpp
class Vehicle {
public:
    virtual void drive() = 0;
};

class Car : public Vehicle {
public:
    void drive() override {
        std::cout << "Driving a car" << std::endl;
    }
};

class Bike : public Vehicle {
public:
    void drive() override {
        std::cout << "Riding a bike" << std::endl;
    }
};

class VehicleFactory {
public:
    static Vehicle* createVehicle(const std::string& type) {
        if (type == "car") {
            return new Car();
        } else if (type == "bike") {
            return new Bike();
        }
        return nullptr;
    }
};
```

#### 3. Builder

The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create various representations.

Key concepts:
- Builder interface
- Concrete builders
- Director (optional)
- Product

Example in C++:

```cpp
class House {
public:
    int floors = 0;
    int walls = 0;
    bool roof = false;
};

class HouseBuilder {
private:
    House house;

public:
    HouseBuilder& addFloors(int floors) {
        house.floors = floors;
        return *this;
    }

    HouseBuilder& addWalls(int walls) {
        house.walls = walls;
        return *this;
    }

    HouseBuilder& addRoof() {
        house.roof = true;
        return *this;
    }

    House build() {
        return house;
    }
};

// Usage
House house = HouseBuilder()
    .addFloors(2)
    .addWalls(4)
    .addRoof()
    .build();
```

### Structural Patterns

Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

#### 1. Adapter

The Adapter pattern allows objects with incompatible interfaces to collaborate.

Key concepts:
- Target interface
- Adapter
- Adaptee

Example in C++:

```cpp
class OldPrinter {
public:
    void print(const std::string& text) {
        std::cout << "OldPrinter: " << text << std::endl;
    }
};

class NewPrinter {
public:
    void printDocument(const std::string& text) {
        std::cout << "NewPrinter: " << text << std::endl;
    }
};

class PrinterAdapter : public OldPrinter {
private:
    NewPrinter* newPrinter;

public:
    PrinterAdapter(NewPrinter* printer) : newPrinter(printer) {}

    void print(const std::string& text) override {
        newPrinter->printDocument(text);
    }
};
```

#### 2. Decorator

The Decorator pattern lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

Key concepts:
- Component interface
- Concrete component
- Base decorator
- Concrete decorators

Example in C++:

```cpp
class Coffee {
public:
    virtual double cost() = 0;
    virtual std::string description() = 0;
};

class SimpleCoffee : public Coffee {
public:
    double cost() override { return 1.0; }
    std::string description() override { return "Simple coffee"; }
};

class CoffeeDecorator : public Coffee {
protected:
    Coffee* coffee;
public:
    CoffeeDecorator(Coffee* c) : coffee(c) {}
    double cost() override { return coffee->cost(); }
    std::string description() override { return coffee->description(); }
};

class MilkDecorator : public CoffeeDecorator {
public:
    MilkDecorator(Coffee* c) : CoffeeDecorator(c) {}
    double cost() override { return CoffeeDecorator::cost() + 0.5; }
    std::string description() override { 
        return CoffeeDecorator::description() + ", milk"; 
    }
};

// Usage
Coffee* coffee = new SimpleCoffee();
coffee = new MilkDecorator(coffee);
std::cout << coffee->description() << " costs $" << coffee->cost() << std::endl;
```

### Behavioral Patterns

Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects.

#### 1. Observer

The Observer pattern lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they're observing.

Key concepts:
- Subject interface
- Concrete subject
- Observer interface
- Concrete observer

Example in C++:

```cpp
#include <vector>
#include <algorithm>

class Observer {
public:
    virtual void update(const std::string& message) = 0;
};

class Subject {
private:
    std::vector<Observer*> observers;
public:
    void attach(Observer* observer) {
        observers.push_back(observer);
    }
    void detach(Observer* observer) {
        observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
    }
    void notify(const std::string& message) {
        for (Observer* observer : observers) {
            observer->update(message);
        }
    }
};

class ConcreteObserver : public Observer {
private:
    std::string name;
public:
    ConcreteObserver(const std::string& n) : name(n) {}
    void update(const std::string& message) override {
        std::cout << name << " received message: " << message << std::endl;
    }
};

// Usage
Subject subject;
ConcreteObserver observer1("Observer 1");
ConcreteObserver observer2("Observer 2");

subject.attach(&observer1);
subject.attach(&observer2);
subject.notify("Hello Observers!");
```

#### 2. Strategy

The Strategy pattern lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.

Key concepts:
- Strategy interface
- Concrete strategies
- Context

Example in C++:

```cpp
class PaymentStrategy {
public:
    virtual void pay(int amount) = 0;
};

class CreditCardStrategy : public PaymentStrategy {
public:
    void pay(int amount) override {
        std::cout << "Paid " << amount << " using Credit Card" << std::endl;
    }
};

class PayPalStrategy : public PaymentStrategy {
public:
    void pay(int amount) override {
        std::cout << "Paid " << amount << " using PayPal" << std::endl;
    }
};

class ShoppingCart {
private:
    PaymentStrategy* paymentStrategy;
public:
    void setPaymentStrategy(PaymentStrategy* strategy) {
        paymentStrategy = strategy;
    }
    void checkout(int amount) {
        paymentStrategy->pay(amount);
    }
};

// Usage
ShoppingCart cart;
cart.setPaymentStrategy(new CreditCardStrategy());
cart.checkout(100);

cart.setPaymentStrategy(new PayPalStrategy());
cart.checkout(200);
```

This comprehensive guide covers the main OOP principles and several key design patterns, providing both theoretical explanations and C++ code examples. Remember that understanding these concepts deeply and knowing when to apply them is crucial for writing maintainable and efficient code.
