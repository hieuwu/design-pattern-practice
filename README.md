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
- Use Interface
