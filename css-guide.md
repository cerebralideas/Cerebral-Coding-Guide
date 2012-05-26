# Cerebral Code-Style for CSS

1. ## Whitespace Rules

	A. Never mix spaces and tabs; this is the **law**!
	
	B. If you are starting a project, and you have a choice, **USE TABS**.
	
		*For readability and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces.*
	
	C. Never leave whitespace at line ends.
	
	D. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	
		- Enforced consistency
		
		- Eliminating end of line whitespace
		
		- Eliminating blank line whitespace
		
		- Commits and diffs that are easier to read
		
		
	F. Insert line-breaks, `\n`, after commas, semicolons, braces — e.g. `{}`, or comments.
	
	G. Double line-breaks can be used to separate sections, from one another for increased readability.

2. ## Beautiful Syntax

	A. ### CSS rules
	
		Don't do this:
		
			.listElement{color:#ffff00;background:#000;}
			
		Do this instead:
		
			.listElement {
				color: #ffff00;
				background: #000;
			}
			
	B. ### Use Shorthand when possible
	
		Don't do this:
		
			h1 {
				font-family: serif;
				font-size: 2em;
				font-weight: 700;
				font-height: 1.5em;
			}
			
		Do this instead:
		
			h1 {
				font: 700 2em/1.5em serif;
			}
			
	C. ### Use numeric version for values, not names
	
		Don't do this:
		
			blockquote {
				background: lightgray;
				color: darkred;
				font-weight: bolder;
			}
			
		Do this instead:
		
			blockquote {
				background: #ccc;
				color: #8D0A08;
				font-weight: 900;
			}
			
	D. ### Shorten colors values if possible
	
		Rather than this:
		
			p {
				color: #000000;
			}
			
		This is better:
		
			p {
				color: #000;
			}
			
	E. ### Wrap URL's with single quotes
	
		Don't do this:
		
			body {
				background: #333 url(/images/background.png);
			}
						
		Do this instead:
		
			body {
				background: #333 url('/images/background.png');
			}
			
	F. ### Use line-breaks after commas to improve readability
	
		Don't do this:
		
			.listEl, .anotherEl, .someQuote, #randomImg, .anotherThingy {
				font-family: serif;
			}
			
		Do this instead:
		
			.listEl,
			.anotherEl,
			.someQuote,
			#randomImg,
			.anotherThingy {
				font-family: serif;
			}
			
3. ## Comments

	A. ### Commenting a Main Section
	
		Use multi-line style separating unrelated sections of code and text should be ALL-CAPS with a double line-break afterwards. The next line of code should be nested after comment.
		
			/**********************************
			* THIS STARTS A NEW SECTION *
			***********************************/
			
				footer …
	 
	B. ### Commenting Subsections
	
		Default style should be a the single line comment above the code that is subject. Comments for subsections should be capitalized with a double line-break and indentation.
			
			/* This Is A Subsection */
					
				footer .someElement {
					color: #000;
				}
					
	C. ### Commenting for Communicaing Intent
	
		This comment should be all lowercase, single line and single line-break with no indentation.
			
			/* this is a comment */
			footer .someElement {
				color: #000;
			}
	 
	C. ### End of Line Comments (Very Rarely Needed)
	
		These are allowed if very short (~4 words)!
	 
			footer .someElement {
				line-height: 1.5em; /* 20px */
			}
			
4. ## Indentation

	A. ### Indent for every section and subsection
	
		To increase readability, it is recommended to indent each section and subsections nesting the code to designate relationships. Start the indentation after the comment, so that the comment "sticks out" to the left helping the eye catch the change.
		
		Example:
		
			/**********************************
			* NAVIGATION SECTION STYLING *
			***********************************/
			
				nav {
					background: #000;
				}
				nav ul {
					margin: 0;
				}
			
				/* Top Navigation Styling */
				
					nav.top {
						font-size: 1.2em;
					}
					nav.top li a {
						padding: 5px;
					}
			
			/**********************************
			* SIDEBAR SECTION STYLING *
			***********************************/
		
				aside …
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			