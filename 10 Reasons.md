10 Gründe warum CoffeeScript rockt wie Sau
==========================================

1. Erfahre die Schönheit sofort
-------------------------------

[Try CofeeScript](http://coffeescript.org)


2. Keine peinliche Klammern, Semikolons und “vars”
--------------------------------------------------

```coffeescript
# Objects and Arrays
math =
  root:   Math.sqrt
  square: square
  cube:   (x) -> x * square x

kids =
  brother:
    name: 'Max'
    age:  11
  sister:
    name: 'Ida'
    age:  9

bitlist = [
  1, 0, 1
  0, 0, 1
  1, 1, 0
]

# Functions
square = (x) -> x * x

alert 'Man, I really like Vegas.' if elvis?

do foobar
```

compiles to

```javascript
var bitlist, kids, math, square;

math = {
  root: Math.sqrt,
  square: square,
  cube: function(x) {
    return x * square(x);
  }
};

kids = {
  brother: {
    name: 'Max',
    age: 11
  },
  sister: {
    name: 'Ida',
    age: 9
  }
};

bitlist = [1, 0, 1, 0, 0, 1, 1, 1, 0];

square = function(x) {
  return x * x;
};

if (typeof elvis !== "undefined" && elvis !== null) {
  alert('Man, I really like Vegas.');
}

foobar();
```

3. Lexical Scoping and Variable Safety
--------------------------------------

```coffeescript
outer = 1

changeNumbers = ->
  inner = -1
  outer = 10

inner = changeNumbers()
```

compiles to

```javascript
var changeNumbers, inner, outer;

outer = 1;

changeNumbers = function() {
  var inner;
  inner = -1;
  return outer = 10;
};

inner = changeNumbers();
```

4. String Concatenation
-----------------------

```coffeescript
elvis = 'The King'
quote = 'Man, I really like Vegas.'

alert "#{elvis} says: #{quote}"
```

compiles to

```javascript
var elvis, quote;

elvis = 'The King';

quote = 'Man, I really like Vegas.';

alert("" + elvis + " says: " + quote);
```