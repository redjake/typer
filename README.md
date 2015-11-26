# Typer.js
Typer.js is an easy to use, choc-full-of-options, robust automated typing solution. There are a number of methods with various options for you to impress your friends, have a parade thrown in your name, and officially obtain "that guy" status ("that gal" for the ladies).

Typer.js has *no library dependencies* so just slap it on your page and go.
(We still love you, [jQuery](https://cdnjs.com/libraries/jquery/).)

In short... Typer.js can type individual characters, unicode, whole words, half words, HTML elements, erase stuff, go fast, go slow, make new lines, fire events, listen to events, and make julienne fries in minutes.

## Installation

Simply include `typer.css` in the `<head>`...
```html
<head>
  ...
  <link rel="stylesheet" href="typer.css">
</head>
```

and include `typer.js` just above your closing `</body>` tag...
```html
<body>
  ...
  <script src="typer.js"></script>
</body>
```

## Usage

```javascript
typer(el, speed)
```

The Typer function itself takes two arguments:

*  `el` - a DOM element, such as `document.body` or `document.querySelector('.someClass')`.
*  `speed` - a number (milliseconds) representing how fast each character should be typed out. If no number is given, Typer will default to 70.

Now you begin calling Typer's various methods (below) via simple & sexy dot-notation...

## Simple Code Examples

#### Single line:

```javascript
typer(document.body)
  .line('Typer.js is awesome!');
```

#### Single line, correct mispelling with back:

```javascript
typer(document.body)
  .line('This function roolz.')
  .back(5)
  .continue('ules!');
```

#### Type a list of frameworks with the help of pause & back:

```javascript
typer(document.body)
  .line('Backbone')
  .pause(1000)
  .back(8)
  .continue('Angular')
  .pause(1000)
  .back(7)
  .continue('Ember');
```

#### Multi-line typing:

```javascript
typer(document.body)
  .line('How cool is this?')
  .line('So very cool.')
  .line('Agreed!');
```

* * *

# Methods

## CURSOR

```javascript
.cursor(false);
.cursor({block: true, blink: 'hard', color: 'red'});
```

The `.cursor` method takes a single argument: `false` _or_ `{an: object}`. You can specify the 3 options below within the object. `.cursor` can be omitted altogether which will result in the default styles mentioned below. Default options need not be given as they will take effect unless otherwise specified.

### No cursor

```javascript
.cursor(false)
```

### Options

#### block

```javascript
.cursor({block: true});
```

*   `false` - (default) The cursor will be a standard vertical line.
*   `true` - The cursor will be a block, inspired from older style terminals.

#### blink

```javascript
.cursor({blink: 'hard'});
```

*   `'soft'` - (default) Smooth blinking animation.
*   `'hard'` - Binary (on / off) blinking animation.

#### color

```javascript
.cursor({color: 'red'});
.cursor({color: '#ff0000'});
.cursor({color: 'rgb(255,0,0)'});
.cursor({color: 'rgba(255,0,0,0.7)'});
```

*   You can specify any css color you want via any method (i.e. name, rgb, #, etc.).
*   As a default, Typer will grab the color attribute of the parent element and use that for the cursor color to match the text with the cursor.

#### _all options at once_

```javascript
.cursor({block: true, blink: 'hard', color: 'red'});
```

* * *

## LINE

```javascript
.line('Typer.js is visual awesomeness!');
.line('Typer.js is visual <em>awesomeness!</em>', 100);
.line(['Type. ', 'Whole. ', '<span style="color: red;">Words.</span>'], 200);
.line(document.querySelector('.someClass'), 200, {html: false}); // Order of 2nd & 3rd arguments is irrelevant.
```

The `.line` method is the heart of Typer. As the name suggests, it types out a single line.  
You can feed it a `'single string'`, an `['array', 'of', 'strings']`, or a DOM element as it's only (necessary) argument. `.line` can take an additional two arguments in any particular order. `.line` defaults to parsing HTML, so you must explicitly tell it not to with the option below.

### Arguments

* Argument 1:
  * `string` - The message you want typed out, character by character (normal typing).
  * `array` - The message you want typed out, phrase by phrase / word by word.
  * DOM element - **SEO** in the house! If you give `.line` a DOM element, Typer will use the contents of that element to type with. For obvious reasons, it is best that the element is hidden (css - `display: none;`). This will let web crawlers index your content while still maintaining *JavaScript typing awesomeness*.
* Arguments 2 or 3:
  * `speed` - A number (milliseconds); Each line can optionally have its own typing speed. If no speed is given, it defaults to the number given to the `typer` function itself or Typer's internal default of 70.
  * `html` - `{html: false}`; specifies that the provided content is to be treated as non-html code. Characters will be typed out exactly as you provide them.

_* TIP: If you supply no arguments, you will create a blank line._

### HTML

_Go nuts_. You can include `<div>`'s, `<span>`'s, elements with styles (i.e. `<span style="color: red;">I'm red!</span>`), `<em>`'s, `<strong>`'s, etc. You also can include HTML void elements (self-closing tags) such as `<br>` and `<hr>`. It's even possible to go crazy and include elements such as `<textarea>` and `<input>`.

* * *

## CONTINUE

```javascript
.continue("I'm on the same line!");
.continue('Same line, emphasis on <em>sloooow</em>.', 500, {html: true});
```

The `.continue` method works just like `.line` in that it accepts the same arguments but it _continues_ typing on the same line, whereas `.line` creates new lines. In conjunction with the `.pause` and `.line` methods, you can create eloborate schemes.

### Arguments

Same as those for `.line` (above).

* * *

## PAUSE

```javascript
.pause();
.pause(1000);
```

Pause takes a single argument, a number in milliseconds. Typer will wait that long before proceeding to the next called method. If no argument is provided, the default is 500.

* * *

## EMIT

```javascript
.emit(document.querySelector('.someClass'), 'boom');
.emit('boom');
```

Emits an event on a specified DOM element or defaults to `document.body`. This is useful for setting up complex automation where multiple Typer functions (or other functions on your page) are time-dependant on eachother. DOM event explosions causing mass automated awesomeness. What could be better?

### Arguments

2 possible argument structures:

1. `(el, 'event')` - specify a DOM element that the `'event'` will be fired from.
2. `('event')` - the event name; Omitting a DOM element will default to the event firing off of `document.body`.

* * *

## LISTEN

```javascript
listen(document.querySelector('.someClass'), 'boom');
listen('boom');
```

Typer has the ability (super-power) to listen for events as well. The `.listen` method will stop Typer in its tracks until the specified event is fired. Once fired, Typer will proceed from where it last left off. More automation goodness.

### Arguments

2 possible argument structures:


1. `(el, 'event')` - specify a DOM element to listen to.
2. `('event')` - the event name we're listening for; Omitting a DOM element will default to listening to `document.body` for the event.

_* NOTE: Typer uses one-time event listeners. When the event is fired, the listener is triggered, then removed._

* * *

## BACK

```javascript
.back(5, 100);
.back('all');
```

Erase stuff!

### Arguments

The 1st argument is mandatory and has two options. The 2nd argument is optional. These arguments are order sensative.

*   Argument 1:
  * Number - number of characters to be erased / how many times you want to "hit" the "backspace button".
  * `'all'` - this will "backspace" the entire line. This saves you having to calculate how many characters (including spaces) there are in the whole line.
*   Argument 2 - Number (milliseconds); the speed at which the backspace will perform. If no number is specified, it will default to the user-supplied Typer speed or Typer's internal default of 70.

* * *

## EMPTY

```javascript
empty();
```

The `.empty` method empties the parent element (specified as an argument to `typer`) and starts over with a fresh line. The parent element could contain multiple lines and HTML elements, the likes of which cannot be undone with a simple `.back('all')`. Also, `.empty` will instantaneously empty the parent element as opposed to backspacing it into oblivion.

* * *

## RUN

```javascript
.run(function() { /* do stuff */ });
```

To round out our automation tools, the `.run` method will do just that: run a function before proceeding with any additional methods. Feed it a function and let it fly.

* * *

## END

```javascript
.end()
.end(function(){console.log('fin!')});
.end(function(){console.log('fin!')}, true);
```

### Arguments

The `.end` method always removes the cursor, can optionally execute a callback function, and optionally fire off the `typerFinished` event. The event can be used to trigger other things in your application. These arguments are completely optional. The order of the arguments is not strict but the callback will always be executed before firing the `typerFinished` event.

*   callback - A function you want executed when `typer` is finished.
*   `true` - Indicates you want the `typerFinished` event fired once Typer is finished. This event is fired from `document.body`. The default (if left unspecified) is false.

* * *