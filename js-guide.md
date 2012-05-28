# Cerebral Code-Style for JavaScript
##### (Adapted from the "Idiomatic Style Manifesto")

1. ## Whitespace Rules

	1. Never mix spaces and tabs; this is the **law**!
	
	2. If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.
	
		For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.
	
	3. Never leave whitespace at line ends or within blank lines.
	
	4. Terminate statements with semicolons. Don't write code that depends on automatic semicolon insertion or ASI. ASI is not a syntactical feature but an error correction procedure (see [Brendan Eich's article](http://brendaneich.com/2012/04/the-infernal-semicolon/)).
	
	5. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	
		- Enforced consistency
		
		- Eliminating end of line whitespace
		
		- Eliminating blank line whitespace
		
		- Commits and diffs that are easier to read
		
		
	6. Insert line-breaks, `\n`, only *after* commas, semicolons, braces — e.g. `{}`, or comments. Again, don't use line-breaks for statement termination, use semicolons (see item D above).
	
	7. Double line-breaks can be used to separate blocks (denoted by braces), from one another for increased readability.

2. ## Beautiful Syntax

	1. ### Parens, Braces, Linebreaks
	
		1. #### Conditionals and Loops:
		
			if/else/for/while/try always have spaces, braces and span multiple lines this encourages readability. 
		
			Don't do this:
		
				if(condition) doSomething();
			
				while(condition)
					doSomething();
		
				for(var i=0;i<100;i++) someIterativeFn();
		
			
			Do this, and use whitespace to promote readability. Notice the space between the punctuation and the line-end after the open brace.
			
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
	
	2. ### Assignments, Declarations
	
		1. When **declaring variables**, combine the declaration with the comma syntax. Make sure to use a tab before each successive declaration. Using only one `var` per scope (function) promotes readability, encourages declaring all variables at the beginning of a function (see #2 below) and keeps your declaration list free of clutter (also saves a few keystrokes).
		
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
			
		
		2. `var` statements should always be in the beginning of their respective scope (function). Same goes for const and let from ECMAScript 6.
		
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
	
	
	3. ### Functions
	
		1. **Anonymous functions** should consist of a minimum of 3 lines — the function keyword, parens, opening brace
		
				function () {
					// statements
				}
		
		2. **Named Function Declarations**
		
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
		
		
		3. **Function Expressions**
		
				var square = function (number) {
					// Return something valuable and relevant
					return number * number;
				};
		
		4. **Function Expression with Identifier**. This preferred form has the added value of being able to call itself and have an identity in stack traces:
		
				var factorial = function factorial(number) {
					if (number < 2) {
						return 1;
					}
					return number * factorial(number - 1);
				};
		
		
		5. **Constructor Declaration**. Notice a critical piece of style is the Capitalization of the name. Because this is not an ordinary function, the only way to tell it apart from other functions is the capitalization which should communicate the need for the `new` keyword.
		
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
		
		6. Functions with callbacks
		
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
	
	4. ### Quotes
	
		Use single quotes if starting a new project, and you have a choice. If adopting a project, use whatever the original developer used as there is no real difference in how JavaScript parses them. 
		
		My personal opinion is that a single quote is more exemplary of fist level and double quote is exemplary of second or nested level. But, that's just my opinion.
		
		What **ABSOLUTELY MUST** be enforced is consistency. **Never mix quotes in the same project. Pick one style and stick with it.**
	
	5. ### End of Lines and Empty Lines
	
		Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically.
	
	6. ### Type Checking (Courtesy jQuery Core Style Guidelines)
	
		1. Actual Types
		
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
		
		2. You can preempt issues by using smart coercion with unary + or - operators:
		
				foo = +document.getElementById("foo-input").value;
				//		^ unary + operator will convert its right side operand to a number
			
				typeof foo;	// "number"
			
				if (foo === 1) {
					importantTask();
				}
			
				// `importantTask()` will be called
		
		
		3. Here are some common cases along with coercions:
		
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
		
		4. Equality
		
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
		
		5. Arrays
		
				var array = [ "a", "b", "c" ];
		
				!!~array.indexOf("a"); // true
		
				!!~array.indexOf("b"); // true
		
				!!~array.indexOf("c"); // true
		
				!!~array.indexOf("d"); // false
				
		
		6. Note that the above should be considered "unnecessarily clever". Prefer the obvious approach of comparing the returned value of indexOf, like:
		
				if ( array.indexOf( "a" ) >= 0 ) {
					// ...
				}
		
	
	7. ### Conditional Evaluation
	
	
		1. When only evaluating that an array has length.
		
			Don't do this:
		
				if (array.length > 0) ...
		
			Do this instead:
		
				if ( array.length ) ...
		
		2. When only evaluating that an array is empty,
		 
		 	Don't do this:
		
				if ( array.length === 0 ) ...
		
			Do this instead:
		
				if ( !array.length ) ...
		
		
		3. When only evaluating that a string is not empty
		
			Don't do this:
			
				if ( string !== "" ) ...
		
			Do this instead:
		 
				if ( string ) ...
		
		
		4. When only evaluating that a string _is_ empty
		
			Don't do this:
		
				if ( string === "" ) ...
		
			Do this instead:
		
				if ( !string ) ...
		
		5. When only evaluating that a reference is true.
		
			Don't do this:
		
				if ( foo === true ) ...
		
			Do this and take advantage of built in capabilities:
		
				if ( foo ) ...
		
		6. When evaluating that a reference is false
		
			Don't do this:
		
				if ( foo == false ) ...
		
			Use negation to coerce a true evaluation instead:
		
				if ( !foo ) ...
		
			Be careful, this will also match: 0, "", null, undefined, NaN. If you _MUST_ test for a boolean false, then use
		
				if ( foo === false ) ...
		
		
		7. When only evaluating a ref that might be null or undefined, but NOT false, "" or 0.
		
			Don't do this:
		
				if ( foo === null || foo === undefined ) ...
		
			Take advantage of == type coercion, like this:
		
				if ( foo == null ) ...
		
				// Remember, using == will match a `null` to BOTH `null` and `undefined`
				// but not `false`, "" or 0
				null == undefined
		
		
		8. ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.
		
		9. Type coercion and evaluation notes:
		
			- Prefer `===` over `==` (unless the case requires loose type evaluation)
		
			- `===` does not coerce type, which means that:
		
					"1" === 1; // false
		
			- == does coerce type, which means that:
		
					"1" == 1; // true
	
	8. ### Booleans, Truthies & Falsies
	
		1. Booleans:
		
				true, false
		
		2. Truthy:
		
				"foo", 1
		
		3. Falsy:
		
				"", 0, null, undefined, NaN, void 0


3. ## Practical Style

	1. ### Practical Module
	
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
	
			}(this));

	2. ### Practical Constructor

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
	
			}(this));


	3. ### Naming
	
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
			
		Don't use the dollar sign, `$`, or the underscore, `_`, unless it's meaning is obvious and well explained. An example would be when you cached DOM elements and you don't always use jQuery to select the element. The dollar sign could differentiate between jQuery elements and regular JS elements.
		
		Example:
		
			var $element = $('#myElement'),
				element = document.getElementById('myElement');
		
	
4. ## Performance Suggestions

	1. ### Repainting the Screen is Expensive
	
		If you are manipulating the DOM, do it all at once. One of the most expensive operations for the browser is having to repaint the screen after DOM manipulation. So, copy what you want to manipulate from the DOM, rework the elements, then reinsert when done. That forces just one repainting.
		
	2. ### Searching the DOM is Expensive
	
		JS libraries are great for DOM selection and manipulation, but they can also have a large impact on performance. One of those factors is searching the DOM. Here are some suggestions using jQuery:
		
		1. Cache anything you use more than once.
		
				var cachedEl = $('#myElement');
				
		2. Use ID's as much as you can. Searching for classes, or special selectors is not performant.
	
		3. Use context and avoid relying on CSS selectors. This helps avoid having to search the whole DOM over and over.

			Don't do this:
			
				$('.classElement > li');
				
			Do this instead:
			
				$('.classElement).find('li');
				
			Or even better:
			
				var classElement = $('.classElement');
				
				classElement.find('li');


	3. ### Use context

		Use a cached elements to find children. If you already have a parent element cached, use it to grab its children. That way, your note searching the whole DOM.
		
		Example:
		
			var parentEl = document.getElementById('myList');
			
			// Now that we have the parent, use it to find it's children.
			var childEl = parentEl.getElementsByTagName('li'); 

		If you are using jQuery, use the `.find()` method as it's the fastest method for finding children with jQuery.

	4. ### Use native Javascript when appropriate
	
		Only call the jQuery library when native JS won't cut it. Everytime you call the `$` or use `.each()`, `.map()`, `css()` and/or `.attr()` on jQuery objects, you are forcing the browser to run through the whole jQuery library. If this is done hundreds of times, it can affect performance.
	
	5. ### When Binding Events to Many Elements use Delegation
	
		Say you have a unordered list that contains 100 list items, and you want to attach a click handler to each item in the list. The best way is to delegate the event, rather than directly binding to each item.
		
		Don't do this:
		
			$('li').click(function () … );
			
		Do this instead:
		
			$('ul').on('click', 'li', function () … )

5. ## Misc Suggestions

	This section will serve to illustrate ideas and concepts that should not be considered dogma, but instead exists to encourage questioning practices in an attempt to find better ways to do common JavaScript programming tasks.

	1. ### Using `switch` should be used with caution 

		An example switch statement
		
			switch (foo) {
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
	

	2. ### Early returns promote code readability with negligible performance difference

		Don't do this:
		
			function returnLate(foo) {
			
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
			
	3. ### Save time and effort and use the literal notation — `{}` or `[]`
	
		Don't do this:
		
			var myObject = new Object(),
				myArray = new Array();
			
		Do this instead:
		
			var myObject = {},
				myArray = [];
			
		
6. ## Comments

	1. ### Default commenting
	
		Default style should be a the single line comment above the code that is subject with no space between the comment and the next line of code.
	
			// This is a comment
			function () …
	 
	2. ### Commenting a Section
	
		Multi-line comments should be used for separating unrelated sections of code and text should be ALL-CAPS with a blank line between the comment and the next line of code.
		
			/**********************************
			* THIS STARTS A NEW SECTION *
			***********************************/
			
			function () …
	 
	3. ### End of Line Comments
	
		These are allowed if very short (~4 words)!
	 
			calc(h, w); // Adds height and width
			
7. ## JavaScript Resources

	* [http://es5.github.com/](http://es5.github.com/)
	* [Baseline For Front End Developers](http://rmurphey.com/blog/2012/04/12/a-baseline-for-front-end-developers/)
	* [Eloquent JavaScript](http://eloquentjavascript.net/)
	* [JavaScript, JavaScript](http://javascriptweblog.wordpress.com/)
	* [Adventures in JavaScript Development](http://rmurphey.com/)
	* [Perfection Kills](http://perfectionkills.com/)
	* [Douglas Crockford's Wrrrld Wide Web](http://www.crockford.com)
	* [JS Assessment](https://github.com/rmurphey/js-assessment)
	* [Leveraging Code Quality Tools by Anton Kovalyov](http://anton.kovalyov.net/slides/gothamjs/)
	<p></p>
 
8. ## Build & Deployment Process

	Projects should always attempt to include some generic means by which source can be linted, tested and compressed in preparation for production use. [Grunt](https://github.com/cowboy/grunt) by Ben Alman is second to none and has officially replaced the "kits/" directory of this repo.

9. ## Test Facility

	Projects _must_ include some form of unit, reference, implementation or functional testing. Use case demos DO NOT QUALIFY as "tests". The following is a list of test frameworks, none of which are endorsed more than the other.
	
	* [QUnit](http://github.com/jquery/qunit)
	* [Jasmine](https://github.com/pivotal/jasmine)
	* [Vows](https://github.com/cloudhead/vows)
	* [Mocha](https://github.com/visionmedia/mocha)
	* [Hiro](http://hirojs.com/)
	* [JsTestDriver](https://code.google.com/p/js-test-driver/)
	* [Buster.js](http://busterjs.org/)