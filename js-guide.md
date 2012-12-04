# Cerebral Code-Style for JavaScript (JS)
(Adapted from the "Idiomatic Style Manifesto")


## Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!
	
1. If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.
	
	For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.
	
1. Never leave whitespace at line ends or within blank lines.

1. Set your maximum line length at 120 characters.

1. Terminate statements with semicolons. Don't write code that depends on automatic semicolon insertion or ASI. ASI is not a syntactical feature but an error correction procedure (see [Brendan Eich's article](http://brendaneich.com/2012/04/the-infernal-semicolon/)).
	
1. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	- Enforced consistency		
	- Eliminating end of line whitespace	
	- Eliminating blank line whitespace	
	- Commits and diffs that are easier to read
		
1. Insert line-breaks, `\n`, only *after* commas, semicolons, braces — e.g. `{}`, or comments. Again, don't use line-breaks for statement termination, use semicolons (see item D above).
	
1. Double line-breaks can be used to separate blocks (denoted by braces), from one another for increased readability.


## Beautiful Syntax

### Parens, Braces, Linebreaks
			
For block statements, e.g. if/else/for/while and functions, always use spaces, braces and new lines. This encourages readability. 
		
Don't do this:

	if(condition) doSomething();

	while(condition)
		doSomething();

	for(var i=0;i<100;i++) someIterativeFn();
	
And, don't do this:

	if (condition)
	{
		doSomething();
	}		

Do this: use whitespace between the keywords and syntax characters to promote readability. Notice the space between the parentheses and the open brace.

	if (condition) {
		// statements
	}

	while (condition) {
		// statements
	}

	for (var i = 0; i < 100; i++) {
		// statements
	}

	var prop;

	for (prop in object) {
		// statements
	}

	if (true) {
		// statements
	} else {
		// statements
	}	
	
### Assignments, Declarations
	
1. When **declaring variables**, combine the declaration with the comma syntax. Make sure to use a tab before each successive declaration. Using only one `var` per scope (function) promotes readability, encourages declaring all variables at the beginning of a function (see #2 below) and keeps your declaration list free of clutter (also saves a few keystrokes).
		
	Don't do this:
	
		var foo = '';
		var bar = '';
		var qux;
	
	Do this instead:
	
		var foo = 'bar',
			num = 1,
			undef;
	
		// Literal notations:
		var array = [],
			object = {};
	

1. `var` statements should always be in the beginning of their respective scope (function). This is because of variable hoisting, see [JavaScript Hoisting Explained](http://net.tutsplus.com/tutorials/javascript-ajax/quick-tip-javascript-hoisting-explained/). Same goes for const and let from ECMAScript 6.

	Don't do this:
	
		function foo() {
	
			// some statements here
	
			var bar = '',
				qux;
			}
	
	Do this instead:
	
		function foo() {
			var bar = '',
				qux;
	
			// all statements after the variables declarations.
			}

	
### Functions
	
1. **Anonymous functions** should consist of a minimum of 3 lines — the function keyword, parens, opening brace

		function () {
			// statements
		}

1. **Named Function Declarations**

		function square(number) {
			// statements
		}
	
		// Usage
		square(10);
	
		// Really contrived continuation passing style
		function square(number, callback) {
			callback(number * number);
		}
	
		square( 10, function(square) {
			// callback statements
		});


1. **Function Expressions**

		var square = function (number) {
			// Return something valuable and relevant
			return number * number;
		};

1. **Function Expression with Identifier**. This preferred form has the added value of being able to call itself and have an identity in stack traces:

		var factorial = function factorial(number) {
			if (number < 2) {
				return 1;
			}
			return number * factorial(number - 1);
		};


1. **Constructor Declaration**. Notice a critical piece of style is the Capitalization of the name. Because this is not an ordinary function, the only way to tell it apart from other functions is the capitalization which should communicate the need for the `new` keyword.

		function FooBar(options) {
			this.options = options;
		}
	
	Now call the constructor function. The capitalization of the function should help remind devs to use the `new` keyword.
	
		// One line if only one key/value pair
		var fooBar = new FooBar({ a: 'alpha' });
	
		fooBar.options;
	
		// Multi-line if multiple key/value pairs
		var fooBar = new FooBar({
			a: 'alpha',
			b: 'beta'
		)};

1. Functions with callbacks

		foo(function () {
			// Note there is no extra space between the first paren
			// of the executing function call and the word "function"
		});
	
		// Function accepting an array, no space
		foo([ 'alpha', 'beta' ]);
	
		// Function accepting an object, no space
		foo({
			a: 'alpha',
			b: 'beta'
		});
	
		// Single argument string literal, no space
		foo('bar');
	
		// Inner grouping parens, no space
		if (!('foo' in obj)) {
	
		}
		
1. Declare functions, especially if you prefer the function expression style at the top of the respective scope. This is due to function and variable hoisting mentioned above in variable declarations.
	
### Quotes
	
Use single quotes if starting a new project, and you have a choice. If adopting a project, use whatever the original developer used as there is no real difference in how JavaScript parses them. 

My personal opinion is that a single quote is more exemplary of fist level and double quote is exemplary of second or nested level. But, that's just my opinion.

Please note: The JSON syntax requires double quotes around both the key and the value.

What **ABSOLUTELY MUST** be enforced is consistency. **Never mix quotes in the same project. Pick one style and stick with it.**
	
### End of Lines and Empty Lines
	
Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically or set your IDE to take care of it for you at save.
	
### Type Checking (Courtesy jQuery Core Style Guidelines)
	
1. Actual Types

	String:

		typeof variable === 'string'

	Number:

		typeof variable === 'number'

	Boolean:

		typeof variable === 'boolean'

	Object:

		typeof variable === 'object'

	Array:

		Array.isArray( arrayLikeObject )
		(wherever possible)

	Node:

		elem.nodeType === 1

	null:

		variable === null

	null or undefined:

		variable == null

	undefined:

		Global Variables:

			typeof variable === 'undefined'

	Local Variables:

		variable === undefined

	Properties:

		object.prop === undefined
		object.hasOwnProperty( prop )
		'prop' in object

1. You can preempt issues by using smart coercion with unary + or - operators:

		foo = +document.getElementById('foo-input').value;
		//		^ unary + operator will convert its right side operand to a number
	
		typeof foo;	// 'number'
	
		if (foo === 1) {
			importantTask();
		}
	
		// `importantTask()` will be called


1. Here are some common cases along with coercions:

		var number = 1,
			string = '1',
			bool = false;

		number; // 1

		number + ''; // '1'

		string; // '1'

		+string; // 1

		+string++; // 1

		string; // 2

		bool; // false

		+bool; // 0

		bool + ''; // 'false'

1. Equality

		var number = 1,
			string = '1',
			bool = true;

		string === number; // false

		string === number + ''; // true

		+string === number; // true

		bool === number; // false

		+bool === number; // true

		bool === string; // false

		bool === !!string; // true

1. Arrays

		var array = [ 'a', 'b', 'c' ];

		!!~array.indexOf('a'); // true

		!!~array.indexOf('b'); // true

		!!~array.indexOf('c'); // true

		!!~array.indexOf('d'); // false
		

1. Note that the above should be considered "unnecessarily clever". Prefer the obvious approach of comparing the returned value of indexOf, like:

		if ( array.indexOf( 'a' ) >= 0 ) {
			// ...
		}
	
### Conditional Evaluation
	
	
1. When only evaluating that an array has length.

	Don't do this:

		if (array.length > 0) ...

	Do this instead:

		if ( array.length ) ...

1. When only evaluating that an array is empty,
 
 	Don't do this:

		if ( array.length === 0 ) ...

	Do this instead:

		if ( !array.length ) ...


1. When only evaluating that a string is not empty

	Don't do this:
	
		if ( string !== '' ) ...

	Do this instead:
 
		if ( string ) ...


1. When only evaluating that a string _is_ empty

	Don't do this:

		if ( string === '' ) ...

	Do this instead:

		if ( !string ) ...

1. When only evaluating that a reference is true.

	Don't do this:

		if ( foo === true ) ...

	Do this and take advantage of built in capabilities:

		if ( foo ) ...

1. When evaluating that a reference is false

	Don't do this:

		if ( foo == false ) ...

	Use negation to coerce a true evaluation instead:

		if ( !foo ) ...

	Be careful, this will also match: 0, '', null, undefined, NaN. If you _MUST_ test for a boolean false, then use

		if ( foo === false ) ...


1. When only evaluating a ref that might be null or undefined, but NOT false, '' or 0.

	Don't do this:

		if ( foo === null || foo === undefined ) ...

	Take advantage of == type coercion, like this:

		if ( foo == null ) ...

		// Remember, using == will match a `null` to BOTH `null` and `undefined`
		// but not `false`, '' or 0
		null == undefined


1. ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

1. Type coercion and evaluation notes:

	* Prefer `===` over `==` (unless the case requires loose type evaluation)

	* `===` does not coerce type, which means that:

			'1' === 1; // false

	* == does coerce type, which means that:

			'1' == 1; // true
	
### Booleans, Truthies & Falsies
	
1. Booleans:

		true, false

1. Truthy:

		'foo', 1

1. Falsy:

		'', 0, null, undefined, NaN, void 0


## Practical Patterns

### For Single (or Few) Instances
	
For the most basic object creation patterns, you have a couple of patterns at your disposal. We'll stick to the Singleton and Module pattern (for more patterns and far more details, see [Addy Osmani's Book of JS Patterns](http://addyosmani.com/resources/essentialjsdesignpatterns/book/)). They are quick to create, easy to understand and utilize the prototypal nature (objects inheriting from other objects) of JavaScript. The one downside is each object contains it's own properties and methods, so when multiple objects are used on a single page, memory and performance is sacrificed (for multiple instance patterns, see section 3.2 below).
	
1. **Singleton Method**
		
	This is a very basic and common method used for object creation in JavaScript. Although, it's not highly recommended, it is good to know.
	
		var primate = {
		
			kingdom: 'Animalia',
			phylum: 'Chordata',
			class: 'Mammalia',
			order: 'Primates',
			
			useThumbs: function () {
				
				console.log('grab object');
			}
		};
		
		var human = primate;
	
		human.species = 'Homo sapiens';
		human.makeFire = function () {
		
			console.log('rub sticks together');
		}
		
		// Inherited properties
		human.kingdom; // Animalia
		human.useThumbs; // writes 'grab object' to console
		
		// Special properties
		human.species; // Homo sapiens
		human.makeFire; // writes 'rub sticks together' to console
		
	With this pattern, everything is passed by reference; good for functions, bad for values.

1. **Module Method**
		
	This is the more recommended pattern for single (or few) object creation. It takes advantage of the closure pattern, allowing for private data and privileged functions. Because of all of this, it is slightly more complex.
	
		(function(global) {
			var Module = (function() {
	
				var data = 'secret';
	
				return {
					getData: function() {
						// get the current value of `data`
						return data;
					},
					setData: function(value) {
						// set the value of `data` and return it
						return (data = value);
					}
				};
			})();
	
			// Other things might happen here
	
			// expose our module to the global object
			global.Module = Module;
	
		}(this));
		
	With this pattern, everything is passed by value, which is not the most performant if many of these objects are created on the same page.

### For Multiple Instances
	
1. **Constructor/Prototype Pattern ("Classical" Inheritance)**
		
	JavaScript can not perfectly replicate the classical style inheritance like Java, C languages and others. As said above, JS has prototypal inheritance, so building classes in JS is not quite as straight-forward as many classical programmers would like. This makes JS loved and hated by many, but an object's ability to inherit from other objects using JS's more relaxed inheritance makes developing in JS very easy.
			
	But, if you are having to instantiate multiple objects onto a single page, using a more "classical" style can be much more beneficial. For this, we take advantage of the Constructor/Prototype pattern. It's much faster and more memory conservative. It takes a bit more advanced logic, has some bad side-effects if written poorly, but it can pay off in dividends if done right.
			
	Example of basic Constructor/Prototype pattern with side effect:

		// Create constructor (Always capitalize the constructor function!)
		function User(name){
			this.name = name;
		}
		User.prototype = {
		
			constructor: User
			getName: function () {
				return this.name;
			}
		};
	
		// Using the *new* keyword, everything's gravy
		var newUser = new User('John Doe');
		
		newUser.getName(); // 'John Doe​​​'
		
		// But, what if we forget the *new* keyword?
		var anotherUser = User('Jane Doe');
		
		anotherUser.getName(); // Error: Cannot call method 'getName' of undefined

	To fix this issue and follow best practices for maintainability, we can use a slight variation of the above. To avoid the unfortunate side-effect of a missing `new` operator, we can test for it. If it wasn't used, we'll fix it, but write a warning to the console (this is important as we want to encourage proper coding practices). Let's also wrap the Constructor/Prototype in a self-invoking function to make into a nice neat package for readability.
	
		(function (global) {
	 
			// Now, create our Constructor function
			function User(name) {
				
				// We first test to see if the newly created object
				// is an instance of this Constructor. In other words,
				// test if the *new* keyword was used.
				if (!(this instanceof User)) {
			
					// If it isn't, then we write a warning out to
					// the console …
					console.log('Warning: Constructor function "User" should be used with the "new" operator.');
			
					// … and fix the issue
					return new User(name);
				}
				
				// assign the argument to the *this* keyword
				this.name = name;
				
				return this;
			};
			
			// Create our prototype as usual
			User.prototype = {
			
				constructor: User,
				getName: function () {
					return this.name;
				}
			};
			
			global.User = User;
	
		}(this));
	
		// Create a *new* object inheriting from our class as usual
		var newUser = new User('John Doe');
		
		console.log(newUser.getName()); // 'John Doe'
		
		// If the *new* keyword is not used, it works, but you get
		// a warning written out to the console.
		var anotherUser = User('Jane Doe');
		
		console.log(anotherUser.getName()); // 'Jane Doe'​ | 'Warning: Constructor function "User" should be used with the "new" operator.'
		
This pattern takes advantage of passing unique data by value, functions and global data by reference.

1. **Resig's Class Maker**
		
	This is a slight variation to the above Constructor/Prototype pattern offered by John Resig. He goes into detail about it on his article, [Simple “Class” Instantiation](http://ejohn.org/blog/simple-class-instantiation/). He mentions how jQuery uses this pattern, and avoids the necessary `new` operator when creating new jQuery objects — `jQuery('div')` and `new jQuery('div')` are virtually the same, although slightly different under the hood.

		// makeClass - By John Resig (MIT Licensed)
		function makeClass(){
		
			return function(args){
			
				if ( this instanceof arguments.callee ) {
				
					if ( typeof this.init == "function" ) {
					
						this.init.apply( this, args.callee ? args : arguments );
					}
					
				} else {
				
					return new arguments.callee( arguments );
				}
			};
		}
		
		var User = makeClass();
		
		User.prototype.init = function(first, last){
		
			this.name = first + " " + last;
		};
		
		var user = User("John", "Resig");
		
		user.name // => "John Resig" 

### Naming
	
You are not a human code compiler/compressor, so don't try to be one. Here are a few general rules:

1. Primitives should be singular nouns

		var quote = 'I am what I am.';

1. Objects should be singular nouns

		var myValue = {
		
			my: value					
		};

1. Arrays and NodeLists should be plural nouns

		var favColors = [blue, red, purple];
		
		var listItems = document.getElementsByTagName('li');		
1. Functions should be verbs

		function sayHi() {
		
			return 'Hi';
		}
		
		var sayHi = function () {
		
			return 'Hi';
		}
		
1. Use real words				

	Example of code with poor names

		function q(s) {
			return document.querySelectorAll(s);
		}
		var i,a=[],els=q('#foo');
		for(i=0;i<els.length;i++){a.push(els[i]);}


	Here's the same piece of logic, but with kinder, more thoughtful naming (and a readable structure):
	

		function query(selector) {
			return document.querySelectorAll( selector );
		}

		var elements = [],
			fooNodes = query('#fo'),
			length = fooNodes.length,
			iter;

		for (iter = 0 ; iter < length; iter++ ) {
		
			elements.push( matches[ iter ] );
		}

1. Use Case to Communicate:

		// Naming basic functions, objects, instances, etc

		camelCase; function and var declarations
		

		// Naming constructors, prototypes, etc.

		PascalCase; constructor function


		// Naming regular expressions

		rDesc = //;
	
	
	From the Google Closure Library Style Guide
	
		functionNamesLikeThis;
		
		variableNamesLikeThis;
		
		ConstructorNamesLikeThis;
		
		EnumNamesLikeThis;
		
		methodNamesLikeThis;
		
		SYMBOLIC_CONSTANTS_LIKE_THIS;
	
1. KISS

	Avoid the use of special characters when possible. Prefixing names with the dollar sign, `$`, or the underscore, `_`, can mean many different things to many different people.
	
	If you feel the need to communicate a real difference between named objects/elements, make sure its meaning is obvious, well explained and communicates a real difference. An example would be when you have raw JS objects and jQuery object mixed together. For example, the dollar sign could differentiate between jQuery objects containing DOM elements from regular JS NodeLists.

	But, if you use this technique, explain it in a comment at the top of the JS file, so everyone is aware of this convention.
	
	Example:
	
		/**********************************
		* DOM SELECTOR THING FOR XYZ *
		
		* NOTE: Prefixing a name with the $ 
		  communicates a jQuery object. *
		***********************************/

		var $listItems = $('li');
		
		// JavaScript NodeLists aren't
		var listItems = document.getElementByTagName('li');
		
	This prevents people from wrapping jQuery objects with another jQuery object. Example:
	
		var listItems = $('li');
		
		// This calls the jQuery object on a jQuery object
		// Not performant :(
		$(listItems).addClass('oops');
		
		
		// If instead you use the $ prefix on vars
		// This tells other devs that this is already wrapped
		var $listItems = $('li');
		
		// Better :)
		$listItems.addClass('ahhh');

## Performance Suggestions

### Repainting the Screen is Expensive
	
If you are manipulating the DOM, do it all at once. One of the most expensive operations for the browser is having to repaint the screen after DOM manipulation. So, copy what you want to manipulate from the DOM, rework the elements, then reinsert when done. That forces just one repainting.
		
### Searching the DOM is Expensive
	
JS libraries are great for DOM selection and manipulation, but they can also have a large impact on performance. One of those factors is searching the DOM. Here are some suggestions using jQuery:

1. Cache anything you use more than once.

		var cachedEl = $('#myElement');
		
1. Use ID's as much as you can. Searching for classes, or special selectors is not performant.

1. Use context and avoid relying on CSS selectors. This helps avoid having to search the whole DOM over and over.

	Don't do this:
	
		$('.classElement > li');
		
	Do this instead:
	
		$('.classElement).find('li');
		
	Or even better:
	
		var classElement = $('.classElement');
		
		classElement.find('li');


### Use context

Use a cached elements to find children. If you already have a parent element cached, use it to grab its children. That way, your note searching the whole DOM.
		
Example:

	var parentEl = document.getElementById('myList');
	
	// Now that we have the parent, use it to find it's children.
	var childEl = parentEl.getElementsByTagName('li'); 

If you are using jQuery, use the `.find()` method as it's the fastest method for finding children with jQuery.

### Use native Javascript when appropriate
	
Only call the jQuery library when native JS won't cut it. Everytime you call the `$` or use `.each()`, `.map()`, `css()` and/or `.attr()` on jQuery objects, you are forcing the browser to run through the whole jQuery library. If this is done hundreds of times, it can affect performance.
	
### When Binding Events to Many Elements use Delegation
	
Say you have a unordered list that contains 100 list items, and you want to attach a click handler to each item in the list. The best way is to delegate the event, rather than directly binding to each item.
		
Don't do this:

	$('li').click(function () … );
	
Do this instead:

	$('ul').on('click', 'li', function () … )

## Misc Suggestions

This section will serve to illustrate ideas and concepts that should not be considered dogma, but instead exists to encourage questioning practices in an attempt to find better ways to do common JavaScript programming tasks.

### Using `switch` should be used with caution 

An example switch statement

	switch (foo) {
		case 'alpha':
			alpha();
			break;
		case 'beta':
			beta();
			break;
		default:
			// something to default to
			break;
	}

A better approach would be to use an object literal or even a module:

	var switchObj = {
		alpha: function() {
			// statements
			// a return
		},
		beta: function() {
			// statements
			// a return
		},
		default: function() {
			// statements
			// a return
		}
	};

	var switchModule = (function () {
		return {
			alpha: function() {
				// statements
				// a return
			},
			beta: function() {
				// statements
				// a return
			},
			default: function() {
				// statements
				// a return
			}
		};
	}());
	

### Early returns promote code readability with negligible performance difference

Don't do this:

	function returnLate(foo) {
	
		var ret;

		if ( foo ) {
			ret = 'foo';
		} else {
			ret = 'quux';
		}
		return ret;
		}

Do this instead:

	function returnEarly(foo) {

		if (foo) {
			return 'foo'; // Exits function here.
		}
		return 'quux'; // Exits here if cond fails
	}
	
### Save time and effort and use the literal notation — `{}` or `[]`

Don't do this:

	var myObject = new Object(),
		myArray = new Array();
	
Do this instead:

	var myObject = {},
		myArray = [];
			
		
## Comments

### Default commenting
	
Default style should be a the single line comment above the code that is subject with no space between the comment and the next line of code.
	
	// This is a comment
	function () …
	 
### Commenting a Section
	
Multi-line comments should be used for separating unrelated blocks of code; text should be ALL-CAPS with a blank line between the comment and the next line of code.
		
	/**********************************
	* THIS STARTS A NEW SECTION *
	***********************************/
	
	function () …
	 
### End of Line Comments
	
These are allowed if very short (~5 words)!

	calc(h, w); // Adds height and width
			

## Handling Content with AJAX

Carefully evaluate your need for dynamically loading content via AJAX. Completely relying on JS for content, state and routing should only be used in certain types of projects. Most projects benefit from a balanced architecture, rather than all or none approach. There's more information about this topic on Twitter's Engineering blog: [Improving performance on twitter.com](http://engineering.twitter.com/2012/05/improving-performance-on-twittercom.html).

1. **Load the Core Data & Templating (HTML) Statically**
	
	* Don't rely solely on JS to load all data and HTML. If JS fails or is slow, you don't want the user staring at a blank page that looks like it finished loading. 
	* Don't rely on JavaScript or the browser to crunch lots of data; it will fail.
			
1. **Load Subsequent & Extraneous Data Content with JS**
		
	* Perceived page load is faster due to core content displayed on screen without dependencies.
	* The use of "lazy loading" or loading content after user action spares having to load undesired content on page load.
		
1. **If You Are Going to Control State & Routing with JS**
	
	* Have static fallback		
	* Use a proven framework
	
1. **Take advantage of JSON for data transmission**

	* Don't import XML or HMTL partials, use JSON to pass data back and forth from the server.
	
	
		
## JavaScript Resources

* [http://es5.github.com/](http://es5.github.com/)
* [Baseline For Front End Developers](http://rmurphey.com/blog/2012/04/12/a-baseline-for-front-end-developers/)
* [Eloquent JavaScript](http://eloquentjavascript.net/)
* [JavaScript, JavaScript](http://javascriptweblog.wordpress.com/)
* [Adventures in JavaScript Development](http://rmurphey.com/)
* [Perfection Kills](http://perfectionkills.com/)
* [Douglas Crockford's Wrrrld Wide Web](http://www.crockford.com)
* [JS Assessment](https://github.com/rmurphey/js-assessment)
* [Leveraging Code Quality Tools by Anton Kovalyov](http://anton.kovalyov.net/slides/gothamjs/)

 
## Build & Deployment Process

Projects should always attempt to include some generic means by which source can be linted, tested and compressed in preparation for production use. [Grunt](https://github.com/cowboy/grunt) by Ben Alman is second to none and has officially replaced the "kits/" directory of this repo.

## Tests

Projects _must_ include some form of unit, reference, implementation or functional testing. Use case demos DO NOT QUALIFY as "tests". The following is a list of test frameworks, none of which are endorsed more than the other.
	
* [QUnit](http://github.com/jquery/qunit)
* [Jasmine](https://github.com/pivotal/jasmine)
* [Vows](https://github.com/cloudhead/vows)
* [Mocha](https://github.com/visionmedia/mocha)
* [Hiro](http://hirojs.com/)
* [JsTestDriver](https://code.google.com/p/js-test-driver/)
* [Buster.js](http://busterjs.org/)
	