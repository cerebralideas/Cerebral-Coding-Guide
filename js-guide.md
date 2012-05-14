# Cerebral Code Style for JavaScript
###### (Forked from the "Idiomatic Style Manifesto")

## I. Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!

2. If you are starting a project, and you have a choice, **USE TABS**.

	*For readability, I always recommend setting your editor's tab size to four characters. This will help align multi-line declarations and conditions.*

3. Never leave whitespace at line ends.

4. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:

	- Enforced consistency
	- Eliminating end of line whitespace
	- Eliminating blank line whitespace
	- Commits and diffs that are easier to read


## II. Beautiful Syntax

### A. Parens, Braces, Linebreaks

if/else/for/while/try always have spaces, braces and span multiple lines this encourages readability. 

Don't do this:

	if(condition) doSomething();

	while(condition) iterating++;

	for(var i=0;i<100;i++) someIterativeFn();


Do this, and use whitespace to promote readability

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


### B. Assignments, Declarations

When declaring variables, combine the declaration with the comma syntax. Make sure to use a tab before each successive declaration. Using only one `var` per scope (function) promotes readability and keeps your declaration list free of clutter (also saves a few keystrokes)

Don't do this:

	var foo = "";
	var bar = "";
	var qux;

Do this instead:

	var foo = "bar",
		num = 1,
		undef;

	// Literal notations:
	var array = [],
		object = {};


`var` statements should always be in the beginning of their respective scope (function). Same goes for const and let from ECMAScript 6.

Don't do this:

	function foo() {

		// some statements here

		var bar = "",
			qux;
		}

Do this instead:

	function foo() {
		var bar = "",
			qux;

		// all statements after the variables declarations.
		}


### C. Function Declaration

	// Anonymous function
	function () {
		// statements
	}

	// Named Function Declaration
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


	// Function Expression
	var square = function (number) {
		// Return something valuable and relevant
		return number * number;
	};

	// Function Expression with Identifier
	// This preferred form has the added value of being
	// able to call itself and have an identity in stack traces:
	var factorial = function factorial(number) {
		if (number < 2) {
			return 1;
		}
		return number * factorial(number - 1);
	};


	// Constructor Declaration
	function FooBar(options) {
		this.options = options;
	}

	// Usage
	// One line if only one key/value pair
	var fooBar = new FooBar({ a: 'alpha' });

	fooBar.options;
	
	// Multi-line if multiple key/value pairs
	var fooBar = new FooBar({
		a: 'alpha',
		b: 'beta'
		)};

	// Functions with callbacks
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

### D. Quotes

Use single quotes if starting a new project, and you have a choice. If adopting a project, use whatever was the original developer used as there is no difference in how JavaScript parses them. 

My personal opinion is that a single quote is more exemplary of fist level and double quote is exemplary of second or nested level. But, that's just my opinion.

What **ABSOLUTELY MUST** be enforced is consistency. **Never mix quotes in the same project. Pick one style and stick with it.**

### E. End of Lines and Empty Lines

Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically.

### F. Type Checking (Courtesy jQuery Core Style Guidelines)

Actual Types

	String:

		typeof variable === "string"

	Number:

		typeof variable === "number"

	Boolean:

		typeof variable === "boolean"

	Object:

		typeof variable === "object"

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

			typeof variable === "undefined"

	Local Variables:

		variable === undefined

	Properties:

		object.prop === undefined
		object.hasOwnProperty( prop )
		"prop" in object

You can preempt issues by using smart coercion with unary + or - operators:

	foo = +document.getElementById("foo-input").value;
	//		^ unary + operator will convert its right side operand to a number

	typeof foo;	// "number"

	if (foo === 1) {
		importantTask();
	}

	// `importantTask()` will be called


Here are some common cases along with coercions:

		var number = 1,
			string = "1",
			bool = false;

		number; // 1

		number + ""; // "1"

		string; // "1"

		+string; // 1

		+string++; // 1

		string; // 2

		bool; // false

		+bool; // 0

		bool + ""; // "false"

Equality

		var number = 1,
			string = "1",
			bool = true;

		string === number; // false

		string === number + ""; // true

		+string === number; // true

		bool === number; // false

		+bool === number; // true

		bool === string; // false

		bool === !!string; // true

Arrays

		var array = [ "a", "b", "c" ];

		!!~array.indexOf("a"); // true

		!!~array.indexOf("b"); // true

		!!~array.indexOf("c"); // true

		!!~array.indexOf("d"); // false
		

Note that the above should be considered "unnecessarily clever". Prefer the obvious approach of comparing the returned value of indexOf, like:

		if ( array.indexOf( "a" ) >= 0 ) {
			// ...
		}


### Conditional Evaluation


When only evaluating that an array has length.

Don't do this:

		if (array.length > 0) ...

Do this instead:

		if ( array.length ) ...

When only evaluating that an array is empty, instead of this:

		if ( array.length === 0 ) ...

Do this

		if ( !array.length ) ...


When only evaluating that a string is not empty, instead of this:

		if ( string !== "" ) ...

Do this:
 
		if ( string ) ...


When only evaluating that a string _is_ empty, instead of this:

		if ( string === "" ) ...

Do this:

		if ( !string ) ...

When only evaluating that a reference is true, instead of this:

		if ( foo === true ) ...

Do this and take advantage of built in capabilities:

		if ( foo ) ...

When evaluating that a reference is false, instead of this:

		if ( foo === false ) ...

Use negation to coerce a true evaluation

		if ( !foo ) ...

Be careful, this will also match: 0, "", null, undefined, NaN. If you _MUST_ test for a boolean false, then use

		if ( foo === false ) ...


When only evaluating a ref that might be null or undefined, but NOT false, "" or 0, instead of this:

		if ( foo === null || foo === undefined ) ...

Take advantage of == type coercion, like this:

		if ( foo == null ) ...

		// Remember, using == will match a `null` to BOTH `null` and `undefined`
		// but not `false`, "" or 0
		null == undefined


ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

Type coercion and evaluation notes:

- Prefer `===` over `==` (unless the case requires loose type evaluation)

- === does not coerce type, which means that:

		"1" === 1; // false

- == does coerce type, which means that:

		"1" == 1; // true

### Booleans, Truthies & Falsies

		// Booleans:
		true, false

		// Truthy:
		"foo", 1

		// Falsy:
		"", 0, null, undefined, NaN, void 0


## Practical Style

### A Practical Module

		(function( global ) {
			var Module = (function() {

				var data = "secret";

				return {
					// This is some boolean property
					bool: true,
					// Some string value
					string: "a string",
					// An array property
					array: [ 1, 2, 3, 4 ],
					// An object property
					object: {
						lang: "en-Us"
					},
					getData: function() {
						// get the current value of `data`
						return data;
					},
					setData: function( value ) {
						// set the value of `data` and return it
						return ( data = value );
					}
				};
			})();

			// Other things might happen here

			// expose our module to the global object
			global.Module = Module;

		})( this );

### A Practical Constructor

		(function( global ) {

			function Ctor( foo ) {

				this.foo = foo;

				return this;
			}

			Ctor.prototype.getFoo = function() {
				return this.foo;
			};

			Ctor.prototype.setFoo = function( val ) {
				return ( this.foo = val );
			};


			// To call constructor's without `new`, you might do this:
			var ctor = function( foo ) {
				return new Ctor( foo );
			};


			// expose our constructor to the global object
			global.ctor = ctor;

		})( this );


### Naming

You are not a human code compiler/compressor, so don't try to be one.

Example of code with poor names

		function q(s) {
			return document.querySelectorAll(s);
		}
		var i,a=[],els=q("#foo");
		for(i=0;i<els.length;i++){a.push(els[i]);}


Here's the same piece of logic, but with kinder, more thoughtful naming (and a readable structure):


		function query( selector ) {
			return document.querySelectorAll( selector );
		}

		var idx = 0,
			elements = [],
			matches = query("#foo"),
			length = matches.length;

		for( ; idx < length; idx++ ){
			elements.push( matches[ idx ] );
		}

A few additional naming pointers:

		// Naming strings

		`dog` is a string
		

		// Naming arrays

		`dogs` is an array of `dog` strings
		

		// Naming functions, objects, instances, etc

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


## Misc

This section will serve to illustrate ideas and concepts that should not be considered dogma, but instead exists to encourage questioning practices in an attempt to find better ways to do common JavaScript programming tasks.

### Using `switch` should be used with caution 

An example switch statement

		switch( foo ) {
			case "alpha":
				alpha();
				break;
			case "beta":
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
			_default: function() {
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
				_default: function() {
					// statements
					// a return
				}
			};
		})();


### Early returns promote code readability with negligible performance difference

Don't do this:

	function returnLate( foo ) {
	
		var ret;

		if ( foo ) {
			ret = "foo";
		} else {
			ret = "quux";
		}
		return ret;
		}

Do this instead:

	function returnEarly(foo) {

		if (foo) {
			return "foo"; // Exits function here.
		}
		return "quux"; // Exits here if cond fails
	}


## III. Comments

1. Default commenting style should be a the single line comment above the code that is subject with no space between the comment and the next line of code.

		// This is a comment
		function () …
 
2. Multi-line should be used for separating unrelated sections of code and text should be capitalized with a blank line between the comment and the next line of code.

		/**********************************
		* THIS STARTS A NEW SECTION *
		***********************************/
		
		function () …
 
3. End of line comments are allowed if very short (~4 words)!
 
 		calc(2, 8); // Adds arguments together
 		
4. JSDoc style is good, but requires a significant time investment

## IV. One Language Code

Programs should be written in one language, whatever that language may be, as dictated by the maintainer or maintainers.