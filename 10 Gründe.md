10 Gründe warum CoffeeScript rockt wie Sau
==========================================

1. Erfahre die Schönheit sofort
-------------------------------

[Try CoffeeScript](http://coffeescript.org)


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

4. Classes for real™
--------------------

```coffeescript
class Dog
  dogName: 'fido'

  constructor: (@dogName) ->

  # Public
  doStuff: ->
    alert 'The dog is walking'

    return

  sayHi: ->
    sayHello.call @

    return

  # Private
  sayHello = ->
    alert "Hi! I'm #{@dogName}"

    return

ralph = new Dog 'ralph'
do ralph.doStuff
# do ralph.sayHello # Fail

bob = new Dog 'bob'
do bob.doStuff
do bob.sayHi

class @AwesomeModel extends Backbone.Model
  defaults: {
    # ...
  }

  clear: -> # Remove from collection
    do @.destroy

class @AwesomeCollection extends Backbone.Collection
  model: AwesomeModel

class @AwesomeView extends Backbone.View

```

5. Varargs
----------

```coffeescript
foo = (first, second, others...) ->
  alert "First entry: #{first}"
  alert "Second entry: #{second}"
  alert "Rest: #{other}" for other in others

foo 'Ted', 'Bob', 'Jim', 'Suzie', 'Blob'
```

compiles to

```javascript
var foo,
  __slice = [].slice;

foo = function() {
  var first, other, others, second, _i, _len, _results;
  first = arguments[0], second = arguments[1], others = 3 <= arguments.length ? __slice.call(arguments, 2) : [];
  alert("First entry: " + first);
  alert("Second entry: " + second);
  _results = [];
  for (_i = 0, _len = others.length; _i < _len; _i++) {
    other = others[_i];
    _results.push(alert("Rest: " + other));
  }
  return _results;
};

foo('Ted', 'Bob', 'Jim', 'Suzie', 'Blob');
```

6. Sexy loops with index and filterings
---------------------------------------

```coffeescript
alert bob for bob in ['Bob', 'Bobb', 'Bobby']

alert "I am bob ##{i}: #{bob}" for bob,i in ['Bob', 'Bobb', 'Bobby']

alert bob for bob in ['Bob', 'Bobb', 'Bobby'] when bob isnt 'Bobb'
```

compiles to

```javascript
var bob, i, _i, _j, _k, _len, _len1, _len2, _ref, _ref1, _ref2;

_ref = ['Bob', 'Bobb', 'Bobby'];
for (_i = 0, _len = _ref.length; _i < _len; _i++) {
  bob = _ref[_i];
  alert(bob);
}

_ref1 = ['Bob', 'Bobb', 'Bobby'];
for (i = _j = 0, _len1 = _ref1.length; _j < _len1; i = ++_j) {
  bob = _ref1[i];
  alert("I am bob #" + i + ": " + bob);
}

_ref2 = ['Bob', 'Bobb', 'Bobby'];
for (_k = 0, _len2 = _ref2.length; _k < _len2; _k++) {
  bob = _ref2[_k];
  if (bob !== 'Bobb') {
    alert(bob);
  }
}
```

7. String Concatenation
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

8. Multiline Strings and HTML
-----------------------------

```coffeescript
html = """
<div class="content">
  You have got <span class="sum">20</span> new emails
</div>
"""
```

compiles to

```javascript
var html;

html = "<div class=\"content\">\n  You have got <span class=\"sum\">20</span> new emails\n</div>";
```

9. “Automatic” return value
---------------------------

```coffeescript
bob = ->
  'Bob'

bob123 = ->
  123

speakBob = ->
  alert 'Hi, i am “Bob”'

  return
```

compiles to

```javascript
var bob, bob123, speakBob;

bob = function() {
  return 'Bob';
};

bob123 = function() {
  return 123;
};

speakBob = function() {
  alert('Hi, i am “Bob”');
};
```

10. The Fat Arrow Operator
---------------------------

```coffeescript
absinth =
  iAmDrunk: false
  drink: ->
    $('.bottle a').on 'click', =>
      @iAmDrunk = true
```

compiles to

```javascript
var absinth;

absinth = {
  iAmDrunk: false,
  drink: function() {
    var _this = this;
    return $('.bottle a').on('click', function() {
      return _this.iAmDrunk = true;
    });
  }
};
```