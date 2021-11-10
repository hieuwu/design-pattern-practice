# design-pattern-practice
Practice notes for problems and solutions learned from Head First Design Pattern book


# Strategy Pattern:


**Get started:** Write a program to display a Duck and other kinds of duck. Basic action that a duck can perform is swim, quack and display

**Naive approach:** Use OO basics like Inheritance, create a Duck then other kinds of duck inherits attributes, method and override it if needed.

The class diagram looks like:

[![](https://mermaid.ink/img/eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIE90aGVyS2luZHNPZkR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBPdGhlcktpbmRzT2ZEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfSIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/edit/#eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIE90aGVyS2luZHNPZkR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBPdGhlcktpbmRzT2ZEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfSIsIm1lcm1haWQiOiJ7XG4gIFwidGhlbWVcIjogXCJkZWZhdWx0XCJcbn0iLCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)

**What if ..? :**
- The customer wants to add a Rubber Duck.  It's ok, just override all the methods then leave it empty
- The customer wants to add new action to a duck, like fly. We can add fly method to Duck class, and we forget to override this method in 33 subclass of Duck that can not fly. Big problem here!
- The customer wants different duck to quack differently, We have to override quack in every Duck subclass?

**Another approach:**
- Use Interface `Quackable` and `Flyable`. Which type of duck can flly or quack can implement from theese interfaces but this is still not a good approach.
- This approach looks good at first, but not good for mantainance. When we need to modify a behavior, we need to track and change it in all subclasses, this can lead to new bug.

[![](https://mermaid.ink/img/eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcbiAgICAgICAgUXVhY2thYmxlIDwuLiBSZWRoZWFkRHVja1xuICAgIFF1YWNrYWJsZSA8Li4gTWFsbGFyZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBSdWJiZXJEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtxdWFjaygpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtmbHkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNrYWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIEZseWFibGUgPC4uIFJlZGhlYWREdWNrXG4gICAgY2xhc3MgRmx5YWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArZmx5KClcbiAgICB9XG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](https://mermaid-js.github.io/mermaid-live-editor/edit/#eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcbiAgICAgICAgUXVhY2thYmxlIDwuLiBSZWRoZWFkRHVja1xuICAgIFF1YWNrYWJsZSA8Li4gTWFsbGFyZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBSdWJiZXJEdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgfVxuICAgIGNsYXNzIE1hbGxhcmREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtxdWFjaygpXG4gICAgfVxuICAgIGNsYXNzIFJlZGhlYWREdWNre1xuICAgICAgICArZGlzcGxheSgpXG4gICAgICAgICtmbHkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNrYWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIEZseWFibGUgPC4uIFJlZGhlYWREdWNrXG4gICAgY2xhc3MgRmx5YWJsZXtcbiAgICAgICAgPDxpbnRlcmZhY2U-PlxuICAgICAgICArZmx5KClcbiAgICB9XG4iLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)

**Efficient approach:**
- We will delegate our Duck methods to another class, and interface so that our program would be less code reuse but, more flexible and maintainable (Following some Design Principles noted at the end of this section)
- Create interfaces for behaviors like FlyBehavior, QuackBehavior. Then for each specific behavior, we create a class that implements the interface. Next, add a reference of each behavior inside a kind of Duck.
- Our final result:

[![](https://mermaid.ink/img/eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICAgIC1GbHlCZWhhdmlvciBmbHlCZWhhdmlvclxuICAgICAgICAtUXVhY2tCZWhhdmlvciBxdWFja0JlaGF2aW9yXG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgICAgK3NldEZseUJlaGF2aW9yKClcbiAgICAgICtzZXRRdWFja0JlaGF2aW9yKClcbiAgICB9XG4gICAgY2xhc3MgUnViYmVyRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBNYWxsYXJkRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cbiAgICBjbGFzcyBSZWRoZWFkRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgICAgICArZmx5KClcbiAgICAgICAgK3F1YWNrKClcbiAgICB9XG5cblxuICAgIEZseUJlaGF2aW9yIDwuLiBGbHlXaXRoV2luZ3NcbiAgICBGbHlCZWhhdmlvciA8Li4gRmx5Tm9XYXlcblxuICAgIGNsYXNzIEZseUJlaGF2aW9ye1xuICAgICAgICA8PGludGVyZmFjZT4-XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIGNsYXNzIEZseVdpdGhXaW5nc3tcbiAgICAgICAgK2ZseSgpXG4gICAgfVxuXG4gICAgY2xhc3MgRmx5Tm9XYXl7XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIFxuICAgIFF1YWNrQmVoYXZpb3IgPC4uIFF1YWNrXG4gICAgUXVhY2tCZWhhdmlvciA8Li4gU3F1ZWFrXG5cbiAgICBjbGFzcyBRdWFja0JlaGF2aW9ye1xuICAgICAgICA8PGludGVyZmFjZT4-XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNre1xuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFNxdWVha3tcbiAgICAgICAgK3F1YWNrKClcbiAgICB9IiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid-js.github.io/mermaid-live-editor/edit/#eyJjb2RlIjoiY2xhc3NEaWFncmFtXG4gICAgRHVjayA8fC0tIFJ1YmJlckR1Y2tcbiAgICBEdWNrIDx8LS0gTWFsbGFyZER1Y2tcbiAgICBEdWNrIDx8LS0gUmVkaGVhZER1Y2tcblxuICAgIGNsYXNzIER1Y2t7XG4gICAgICAgIC1GbHlCZWhhdmlvciBmbHlCZWhhdmlvclxuICAgICAgICAtUXVhY2tCZWhhdmlvciBxdWFja0JlaGF2aW9yXG4gICAgICArc3dpbSgpXG4gICAgICArcXVhY2soKVxuICAgICAgK2Rpc3BsYXkoKVxuICAgICAgK3NldEZseUJlaGF2aW9yKClcbiAgICAgICtzZXRRdWFja0JlaGF2aW9yKClcbiAgICB9XG4gICAgY2xhc3MgUnViYmVyRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgIH1cbiAgICBjbGFzcyBNYWxsYXJkRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgICAgICArcXVhY2soKVxuICAgIH1cbiAgICBjbGFzcyBSZWRoZWFkRHVja3tcbiAgICAgICAgK2Rpc3BsYXkoKVxuICAgICAgICArZmx5KClcbiAgICAgICAgK3F1YWNrKClcbiAgICB9XG5cblxuICAgIEZseUJlaGF2aW9yIDwuLiBGbHlXaXRoV2luZ3NcbiAgICBGbHlCZWhhdmlvciA8Li4gRmx5Tm9XYXlcblxuICAgIGNsYXNzIEZseUJlaGF2aW9ye1xuICAgICAgICA8PGludGVyZmFjZT4-XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIGNsYXNzIEZseVdpdGhXaW5nc3tcbiAgICAgICAgK2ZseSgpXG4gICAgfVxuXG4gICAgY2xhc3MgRmx5Tm9XYXl7XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIFxuICAgIFF1YWNrQmVoYXZpb3IgPC4uIFF1YWNrXG4gICAgUXVhY2tCZWhhdmlvciA8Li4gU3F1ZWFrXG5cbiAgICBjbGFzcyBRdWFja0JlaGF2aW9ye1xuICAgICAgICA8PGludGVyZmFjZT4-XG4gICAgICAgICtmbHkoKVxuICAgIH1cblxuICAgIGNsYXNzIFF1YWNre1xuICAgICAgICArcXVhY2soKVxuICAgIH1cblxuICAgIGNsYXNzIFNxdWVha3tcbiAgICAgICAgK3F1YWNrKClcbiAgICB9IiwibWVybWFpZCI6IntcbiAgXCJ0aGVtZVwiOiBcImRlZmF1bHRcIlxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)

**Conclusion:**
- **The Strategy Pattern** defines a family of algorithms,encapsulates each one, and makes them interchangeable.Strategy lets the algorithm vary independently from clients that use it

# Observer Pattern:
**Get started:** 

**Naive approach:** 

The class diagram looks like:

**What if ..? :**
**Another approach:**

**Efficient approach:**

- Our final result:


**Conclusion:**
- **The Observer Pattern** 



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




