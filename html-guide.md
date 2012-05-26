# Cerebral Code-Style for HTML


## I. Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!

2. If you are starting a project, and you have a choice, **USE TABS**.

	*For readability, I always recommend setting your editor's tab size to four characters. This will help align multi-line declarations and conditions.*

3. Never leave whitespace at line ends.

4. Terminate statements with semicolons. Don't write code that depends on automatic semicolon insertion or ASI. ASI is not a syntactical feature but an error correction procedure (see [Brendan Eich's article](http://brendaneich.com/2012/04/the-infernal-semicolon/)).

5. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:

	- Enforced consistency
	- Eliminating end of line whitespace
	- Eliminating blank line whitespace
	- Commits and diffs that are easier to read
	
6. Insert line-breaks, `\n`, only after commas, semicolons, open braces, or comments. Again, don't use line-break for statement termination, use semicolons (see #4).

7. Double line-break can be used to separate blocks from one another for increased readability.



## II. Beautiful Syntax

### A. 

if/else/for/while/try always have spaces, braces and span multiple lines this encourages readability. 

Don't do this:

	if(condition) doSomething();
