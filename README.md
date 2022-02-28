# design-pattern-practice
Practice notes for problems and solutions learned from Head First Design Pattern book


# Strategy Pattern:

**Get started:** Write a program to display a Duck and other kinds of duck. Basic action that a duck can perform is swim, quack and display

**Naive approach:** Use OO basics like Inheritance, create a Duck then other kinds of duck inherits attributes, method and override it if needed.

The class diagram looks like:

```mermaid

classDiagram
    Duck <|-- OtherKindsOfDuck
    Duck <|-- MallardDuck
    Duck <|-- RedheadDuck

    class Duck{
      +swim()
      +quack()
      +display()
    }
    class OtherKindsOfDuck{
        +display()
    }
    class MallardDuck{
        +display()
    }
    class RedheadDuck{
        +display()
    }

```


**What if ..? :**
- The customer wants to add a Rubber Duck.  It's ok, just override all the methods then leave it empty
- The customer wants to add new action to a duck, like fly. We can add fly method to Duck class, and we forget to override this method in 33 subclass of Duck that can not fly. Big problem here!
- The customer wants different duck to quack differently, We have to override quack in every Duck subclass?

**Another approach:**
- Use Interface `Quackable` and `Flyable`. Which type of duck can flly or quack can implement from theese interfaces but this is still not a good approach.
- This approach looks good at first, but not good for mantainance. When we need to modify a behavior, we need to track and change it in all subclasses, this can lead to new bug.

```mermaid
classDiagram
    Duck <|-- RubberDuck
    Duck <|-- MallardDuck
    Duck <|-- RedheadDuck
        Quackable <.. RedheadDuck
    Quackable <.. MallardDuck

    class Duck{
      +swim()
      +quack()
      +display()
    }
    class RubberDuck{
        +display()
    }
    class MallardDuck{
        +display()
        +quack()
    }
    class RedheadDuck{
        +display()
        +fly()
        +quack()
    }

    class Quackable{
        <<interface>>
        +quack()
    }

    Flyable <.. RedheadDuck
    class Flyable{
        <<interface>>
        +fly()
    }


```

<!-- [![](https://mermaid.ink/img/eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcbiAgICAgICAgUXVhY2thYmxlIDwuLiBSZWRoZWFkRHVja1xuICAgIFF1YWNrYWJsZSA8Li4gTWFsbGFyZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBSdWJiZXJEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtxdWFjaygpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtmbHkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNrYWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIEZseWFibGUgPC4uIFJlZGhlYWREdWNrXG4gICAgY2xhc3MgRmx5YWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArZmx5KClcbiAgICB9XG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](https://mermaid-js.github.io/mermaid-live-editor/edit/#eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcbiAgICAgICAgUXVhY2thYmxlIDwuLiBSZWRoZWFkRHVja1xuICAgIFF1YWNrYWJsZSA8Li4gTWFsbGFyZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBSdWJiZXJEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtxdWFjaygpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtmbHkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNrYWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIEZseWFibGUgPC4uIFJlZGhlYWREdWNrXG4gICAgY2xhc3MgRmx5YWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArZmx5KClcbiAgICB9XG4iLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ) -->

**Efficient approach:**
- We will delegate our Duck methods to another class, and interface so that our program would be less code reuse but, more flexible and maintainable (Following some Design Principles noted at the end of this section)
- Create interfaces for behaviors like FlyBehavior, QuackBehavior. Then for each specific behavior, we create a class that implements the interface. Next, add a reference of each behavior inside a kind of Duck.
- Our final result:

```mermaid

classDiagram
    Duck <|-- RubberDuck
    Duck <|-- MallardDuck
    Duck <|-- RedheadDuck

    class Duck{
        -FlyBehavior flyBehavior
        -QuackBehavior quackBehavior
      +swim()
      +quack()
      +display()
      +setFlyBehavior()
      +setQuackBehavior()
    }
    
    class RubberDuck{
        +display()
    }
    
    class MallardDuck{
        +display()
        +quack()
    }
    
    class RedheadDuck{
        +display()
        +fly()
        +quack()
    }
    FlyBehavior <.. FlyWithWings
    FlyBehavior <.. FlyNoWay

    class FlyBehavior{
        <<interface>>
        +fly()
    }

    class FlyWithWings{
        +fly()
    }

    class FlyNoWay{
        +fly()
    }

    
    QuackBehavior <.. Quack
    QuackBehavior <.. Squeak

    class QuackBehavior{
        <<interface>>
        +fly()
    }

    class Quack{
        +quack()
    }

    class Squeak{
        +quack()
    }

```


**Conclusion:**
- **The Strategy Pattern** defines a family of algorithms,encapsulates each one, and makes them interchangeable.Strategy lets the algorithm vary independently from clients that use it

# Observer Pattern:
**Get started:** Given that we need to write a Weather monitor application. In this application, we have to get data from a provider. The important thing is that, we need to notify to all users whenver the forecase measurement data is updated. And also we need to display it with in multiple forms.

**Naive approach:** So first of all, we need a class contains the data and some methods to get and display data to the user. The class would look like:

```mermaid
classDiagram

    class WeatherData{
        -CurrentConditionDisplay currentConditionDisplay
        -StatisticsDisplay statisticsDisplay
        -ForecastDisplay forecastDisplay
      +getTemprature()
      +getHumidity()
      +getPressure()
      +measurementsDataChanged()
    }
```

And our `measurementsDataChanged` method would look something like:

```java
public void measurementsDataChanged() {
    float temp = getTemperature()
    float humidity = getHumidity()
    float pressure = getPressure()
    
    currentConditionDisplay.update(temp, humidity, pressure)
    statisticsDisplay.update(temp, humidity, pressure)
    forecastDisplay.update(temp, humidity, pressure)
}
```


**What if ..? :** 
- We need to add more display or remove one. Because the `measurementsDataChanged()` method is implemented in concrete way, we can not add or remove display withou making changes to the program

**Efficient approach:** We use Observer Pattern for this case. In this pattern, we will have a `Subject` which is our `WeatherData` class, where we get data from. The next one is `Observers`, all the thing that consume the data which is our displays
- First, we need to define all the interface needed for `Observers`, `Subjects` along with shared behavior of each observer:
```mermaid
classDiagram
    class Subject{
        <<interface>>
        +registerObserver(Observer o)
        +removeObserver(Observer o)
        +notifyObservers()
    }

    class Observer{
        <<interface>>
        +update(float temp, float humidity, float pressure)
    }

    class DisplayElement{
        <<interface>>
        +display()
    }

```
- Next, refactor our `WeatherData` class:
```java
public class WeatherData implements Subject {
    private ArrayList observers;
    private float temperature;
    private float humidity;
    private float pressure;
    
    public WeatherData() {
        observers = new ArrayList();
    }
    
    public void registerObserver(Observer o) {
        observers.add(o);
    }
    
    public void removeObserver(Observer o) {
        int i = observers.indexOf(o);
        if (i >= 0) {
            observers.remove(i);
        }
    }
    
    public void notifyObservers() {
        for (int i = 0; i < observers.size(); i++) {
            Observer observer = (Observer) observers.get(i);
            observer.update(temperature, humidity, pressure);
        }
    }
    
    public void measurementsChanged() {
        notifyObservers();
    }
    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }
}
```


- Our final result:

```mermaid
classDiagram
    WeatherData <|-- Subject
    class WeatherData{
        -CurrentConditionDisplay currentConditionDisplay
        -StatisticsDisplay statisticsDisplay
        -ForecastDisplay forecastDisplay
      +getTemprature()
      +getHumidity()
      +getPressure()
      +measurementsDataChanged()
      +registerObserver(Observer o)
      +removeObserver(Observer o)
      +notifyObservers()
    }
    class Subject{
        <<interface>>
        +registerObserver(Observer o)
        +removeObserver(Observer o)
        +notifyObservers()
    }

    class Observer{
        <<interface>>
        +update(float temp, float humidity, float pressure)
    }

    class DisplayElement{
        <<interface>>
        +display()
    }

    CurrentConditionDisplay <|-- Observer
    CurrentConditionDisplay <|-- DisplayElement
    class CurrentConditionDisplay {
       +update(float temp, float humidity, float pressure)
       +display()
    }

    StatisticsDisplay <|-- Observer
    StatisticsDisplay <|-- DisplayElement
    class StatisticsDisplay {
       +update(float temp, float humidity, float pressure)
       +display()
    }

    ForecastDisplay <|-- Observer
    ForecastDisplay <|-- DisplayElement
    class ForecastDisplay {
       +update(float temp, float humidity, float pressure)
       +display()
    }
```
**Conclusion:**
- **The Observer Pattern** defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically

# Decorator Pattern:
**Get started:** Write a program to for a coffee shop to create order with many beverages, of course, many toppings and other properties.

**Naive approach:** Create an abstract class called Beverage, and other kind will extends this class. Then just override methods like cost() to calculate the price for each kind of beverage.

The class diagram looks like:


**What if ..? :**
- We want to add some condiments like milk, chocolate, then we just need to create more class for this kind of "new" beverage. Maybe for current Coffe, we would have new classes such as CoffeeWithMilk, CoffeeWithSoy,..uh oh Class Explosion
- We calculate the price for each beverage, with different condiments, size

**Another approach:** 
- Put all the condiments inside the abstract Beverage class, then for each subclass, we have to override all the checking condiments method as below. This is still not a good approach

**Efficient approach:**

# Factory Pattern:
- Simple Factory
- Factory Method
- Abstract Factory
**Get started:** 

**Naive approach:** 

The class diagram looks like:

**What if ..? :**
**Another approach:**

**Efficient approach:**

- Our final result:


**Conclusion:**
- **The Factory Pattern** 

# Builder Pattern:
**Get started:** 

**Naive approach:** 

The class diagram looks like:

**What if ..? :**
**Another approach:**

**Efficient approach:**

- Our final result:


**Conclusion:**
- **The Builder Pattern** 




