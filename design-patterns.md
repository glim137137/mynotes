# Design Pattrens

[TOC]

设计模式是软件设计中常见问题的**可重用解决方案**，是前辈程序员经验的总结。它们不是代码，而是解决问题的**模板和指导思想**。

**设计模式的三大分类（GoF 23种）**

根据目的（模式是用来做什么的），设计模式分为三类：

1. **创建型模式 (Creational Patterns)**：关注对象的**创建过程**，将对象的创建与使用分离。
2. **结构型模式 (Structural Patterns)**：关注如何将类或对象**组合成更大的结构**。
3. **行为型模式 (Behavioral Patterns)**：关注对象之间的**职责分配和通信**。



# 创建型模式 (5种)



## 单例模式 (Singleton Pattern)
**目的**：确保一个类**只有一个实例**，并提供一个全局访问点。
**场景**：配置文件读取、线程池、数据库连接池、日志对象等。
**关键点**：构造函数私有化，静态方法获取实例。

```java
public class Singleton {
    // 1. 静态私有实例，volatile防止指令重排
    private static volatile Singleton instance;
    
    // 2. 私有构造函数，防止外部new
    private Singleton() {}
    
    // 3. 公共静态方法获取实例
    public static Singleton getInstance() {
        if (instance == null) { // 第一次检查
            synchronized (Singleton.class) { // 加锁
                if (instance == null) { // 第二次检查（双重检查锁定）
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
    
    // 其他方法...
}
```

## 工厂方法模式 (Factory Method Pattern)

**目的**：定义一个创建对象的接口，但让子类决定实例化哪一个类。工厂方法使一个类的实例化延迟到其子类。
**场景**：需要创建对象，但不希望指定具体的类。

```java
// 1. 产品接口
interface Product {
    void use();
}

// 2. 具体产品
class ConcreteProductA implements Product {
    @Override
    public void use() { System.out.println("Using Product A"); }
}

class ConcreteProductB implements Product {
    @Override
    public void use() { System.out.println("Using Product B"); }
}

// 3. 创建者抽象类
abstract class Creator {
    public abstract Product createProduct(); // 工厂方法
    
    public void someOperation() {
        Product product = createProduct();
        product.use();
    }
}

// 4. 具体创建者
class ConcreteCreatorA extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProductA();
    }
}

class ConcreteCreatorB extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProductB();
    }
}
```

## 抽象工厂模式 (Abstract Factory Pattern)

**目的**：提供一个接口，用于创建**相关或依赖对象**的家族，而不需要指定具体类。
**场景**：需要创建一系列相关的产品。

```java
// 抽象产品族
interface Button {
    void render();
}

interface Checkbox {
    void check();
}

// 具体产品 - Windows风格
class WindowsButton implements Button {
    @Override
    public void render() { System.out.println("Rendering Windows button"); }
}

class WindowsCheckbox implements Checkbox {
    @Override
    public void check() { System.out.println("Windows checkbox checked"); }
}

// 具体产品 - Mac风格
class MacButton implements Button {
    @Override
    public void render() { System.out.println("Rendering Mac button"); }
}

class MacCheckbox implements Checkbox {
    @Override
    public void check() { System.out.println("Mac checkbox checked"); }
}

// 抽象工厂
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// 具体工厂
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() { return new WindowsButton(); }
    
    @Override
    public Checkbox createCheckbox() { return new WindowsCheckbox(); }
}

class MacFactory implements GUIFactory {
    @Override
    public Button createButton() { return new MacButton(); }
    
    @Override
    public Checkbox createCheckbox() { return new MacCheckbox(); }
}
```

## 建造者模式 (Builder Pattern)
**目的**：将一个复杂对象的构建与其表示分离，使得同样的构建过程可以创建不同的表示。
**场景**：创建复杂对象，对象有很多可选参数。

```java
public class Computer {
    // 必需参数
    private final String cpu;
    private final String ram;
    // 可选参数
    private final String storage;
    private final String graphicsCard;
    
    private Computer(Builder builder) {
        this.cpu = builder.cpu;
        this.ram = builder.ram;
        this.storage = builder.storage;
        this.graphicsCard = builder.graphicsCard;
    }
    
    public static class Builder {
        private final String cpu;
        private final String ram;
        private String storage = "256GB SSD";
        private String graphicsCard = "Integrated";
        
        public Builder(String cpu, String ram) {
            this.cpu = cpu;
            this.ram = ram;
        }
        
        public Builder storage(String storage) {
            this.storage = storage;
            return this;
        }
        
        public Builder graphicsCard(String graphicsCard) {
            this.graphicsCard = graphicsCard;
            return this;
        }
        
        public Computer build() {
            return new Computer(this);
        }
    }
}

// 使用
Computer computer = new Computer.Builder("Intel i7", "16GB")
                        .storage("512GB SSD")
                        .graphicsCard("NVIDIA RTX 3080")
                        .build();
```

## 原型模式 (Prototype Pattern)
**目的**：用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。
**场景**：创建对象成本较高，或者希望避免重复的初始化过程。

```java
interface Prototype extends Cloneable {
    Prototype clone() throws CloneNotSupportedException;
}

class ConcretePrototype implements Prototype {
    private String field;
    
    public ConcretePrototype(String field) {
        this.field = field;
    }
    
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (ConcretePrototype) super.clone(); // 浅拷贝
    }
    
    public String getField() { return field; }
}
```



# 结构型模式 (7种)



## 适配器模式 (Adapter Pattern)
**目的**：将一个类的接口转换成客户期望的另一个接口。

```java
// 目标接口
interface Target {
    void request();
}

// 需要适配的类
class Adaptee {
    public void specificRequest() {
        System.out.println("Specific request");
    }
}

// 适配器
class Adapter implements Target {
    private Adaptee adaptee;
    
    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }
    
    @Override
    public void request() {
        adaptee.specificRequest(); // 转换调用
    }
}
```

## 装饰器模式 (Decorator Pattern)
**目的**：动态地给一个对象添加一些额外的职责。

```java
interface Coffee {
    double getCost();
    String getDescription();
}

class SimpleCoffee implements Coffee {
    @Override
    public double getCost() { return 2.0; }
    @Override
    public String getDescription() { return "Simple coffee"; }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;
    
    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }
    
    public double getCost() {
        return decoratedCoffee.getCost();
    }
    
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }
}

class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }
    
    @Override
    public double getCost() {
        return super.getCost() + 0.5;
    }
    
    @Override
    public String getDescription() {
        return super.getDescription() + ", with milk";
    }
}
```

## 代理模式 (Proxy Pattern)
**目的**：为其他对象提供一种代理以控制对这个对象的访问。

```java
interface Image {
    void display();
}

class RealImage implements Image {
    private String filename;
    
    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }
    
    private void loadFromDisk() {
        System.out.println("Loading " + filename);
    }
    
    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;
    
    public ProxyImage(String filename) {
        this.filename = filename;
    }
    
    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename); // 延迟加载
        }
        realImage.display();
    }
}
```

## 外观模式 (Facade Pattern)
**目的**：为子系统中的一组接口提供一个一致的界面。

```java
class CPU {
    void start() { System.out.println("CPU start"); }
}

class Memory {
    void load() { System.out.println("Memory load"); }
}

class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    
    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
    }
    
    public void start() {
        cpu.start();
        memory.load();
        System.out.println("Computer started");
    }
}
```

## 桥接模式 (Bridge Pattern)
**目的**：将抽象部分与实现部分分离，使它们都可以独立地变化。

```java
interface Color {
    void applyColor();
}

class Red implements Color {
    @Override
    public void applyColor() { System.out.println("Red"); }
}

abstract class Shape {
    protected Color color;
    
    public Shape(Color color) {
        this.color = color;
    }
    
    abstract void draw();
}

class Circle extends Shape {
    public Circle(Color color) {
        super(color);
    }
    
    @Override
    void draw() {
        System.out.print("Circle filled with ");
        color.applyColor();
    }
}
```

# 行为型模式 (11种)

## 策略模式 (Strategy Pattern)
**目的**：定义一系列的算法，把它们一个个封装起来，并且使它们可相互替换。

```java
interface PaymentStrategy {
    void pay(int amount);
}

class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPalPayment implements PaymentStrategy {
    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

class ShoppingCart {
    private PaymentStrategy paymentStrategy;
    
    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.paymentStrategy = strategy;
    }
    
    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}
```

## 观察者模式 (Observer Pattern)
**目的**：定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

interface Subject {
    void registerObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}

class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;
    
    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }
    
    @Override
    public void removeObserver(Observer o) {
        observers.remove(o);
    }
    
    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(news);
        }
    }
    
    public void setNews(String news) {
        this.news = news;
        notifyObservers();
    }
}

class NewsChannel implements Observer {
    private String news;
    
    @Override
    public void update(String news) {
        this.news = news;
        System.out.println("News updated: " + news);
    }
}
```

## 模板方法模式 (Template Method Pattern)
**目的**：定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。

```java
abstract class Game {
    // 模板方法
    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
    
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();
}

class Cricket extends Game {
    @Override
    void initialize() { System.out.println("Cricket Game Initialized"); }
    @Override
    void startPlay() { System.out.println("Cricket Game Started"); }
    @Override
    void endPlay() { System.out.println("Cricket Game Finished"); }
}
```

## 其他重要模式：
- **责任链模式 (Chain of Responsibility)**：让多个对象都有机会处理请求
- **命令模式 (Command)**：将请求封装为对象
- **状态模式 (State)**：允许对象在内部状态改变时改变它的行为
- **访问者模式 (Visitor)**：在不修改类的前提下定义新的操作

# 设计模式选择指南

| 场景             | 推荐模式         |
| :--------------- | :--------------- |
| 需要全局唯一实例 | **单例模式**     |
| 创建复杂对象     | **建造者模式**   |
| 创建相关对象家族 | **抽象工厂模式** |
| 需要扩展对象功能 | **装饰器模式**   |
| 控制对象访问     | **代理模式**     |
| 算法可互换       | **策略模式**     |
| 对象状态变化通知 | **观察者模式**   |
| 定义算法骨架     | **模板方法模式** |

**重要原则**：不要为了用模式而用模式。模式是解决特定问题的工具，而不是必须遵守的教条。优先考虑代码的**简洁性**和**可读性**。