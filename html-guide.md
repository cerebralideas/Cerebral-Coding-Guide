# Cerebral Code-Style for CSS

1. ## Whitespace Rules

	1. Never mix spaces and tabs; this is the **law**!
	
	2. If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.
	
		For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.
	
	3. Never leave whitespace at line ends or within blank lines.
	
	4. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	
		- Enforced consistency
		
		- Eliminating end of line whitespace
		
		- Eliminating blank line whitespace
		
		- Commits and diffs that are easier to read
		
		
	5. Insert line-breaks, `\n`, after tag closures, `</>`.
	
	6. Double line-breaks should be used to separate same level elements from one another for increased readability.

2. ## Know Your Elements

	1. ### Block Elements
	
		Common block HTML4 elements:
	
		`<html>` `<body>` `<div>` `<ul>` `<li>` `<p>` `<blockquote>` <br/>
		
		`<h1> - <h6>` `<table>` `<form>` `<fieldset>`
		
		New block HTML5 elements:
		
		`<header>` `<section>` `<article>` `<footer>` `<aside>`
	
		Block-level elements represent a horizontal section of a document. These elements span the whole width of their container or parent element. Block-level elements can contain other block-level elements.
		
		Block level elements do not need a break tag, `<br/>`, afterward to ensure any element falls below.
		
		Don't do this:
		
			<div><!-- stuff --></div><br/>
			
		The break tag is not needed since block elements naturally take up the whole width of the container element.
		
	2. ### Inline Elements
	
		Common inline HTML4 elements:
		
		`<a>` `<span>` `<strong>` `<img>`
		
		Inline elements have no inherent width. These elements can be zero pixels wide to the full width of the container element. They get their width by whatever they are containing. So, if you have, say, an `<img>` element, it will just in herent the width of the actual image file it contains.
		
		Their height is also dictated by what they contain. Inline elements can't (and won't follow) any top or bottom margin and padding; you can't set any height either.
		
		Inline elements should not contain block elements.
		
	3. ### Inline-Block Elements
	
		There are no natural `inline-block` elements, but block elements are best to convert to `inline-block`. These elements are created by the `display: inline-block;` property in CSS. These elements have properties of both block elements and inline. `inline-block` elements can contain any kind of element — block or inline.
		
		`inline-block` elements take on the width of whatever they contain, unless specified otherwise. If an `inline-block` element contains a block element, then it will take up the full width of its container. If it contains an inline element, it is the width of whatever it contains.
		
3. ## Style (Block) Element

	Rarely, if ever, use the `<style>` block element. There are very few reasons to write css within style tags in HTML. Always use external stylesheets!
	
	*The one exception is if you need to declare IE specific styling with a conditional stylesheet.*
	
4. ## Script

	Including inline or in-page JavaScript should be avoided as much as possible. This again is going back to not mixing languages. JavaScript should be in .js files, CSS should be in .css files and HTML should be in .html files. So, if you have some page specific JavaScript that you don't want on your `site.js` file, create a separate `page.js` file and include it in just that page.
	
	Don't do this:
	
		<script type="text/javascript">
			
			// Bunch of JS functions and stuff in your .html file
			
		</script>
		
	Do this instead:
	
		<script type="text/javascript" src="/js/site.js"></script>
	
	But remember, cache anything that is used frequently throughout the site. If you are including different .js files throughout your site, find ways to write more reusable JavaScript so that you include it once and for all.

4. ## Attributes

	1. ### Classes
	
		1. Classes are traditionally used to add the hooks necessary for CSS styling. 
		
		2. Name classes with semantic names that describe either their content or their purpose. **Remember: use a naming convention that someone that is unfamiliar with the project could read and understand.** Use either camel case or underscores for complex names, but once you choose a convention, stick with it.
		
			Don't do this:
			
				<!-- Too ambigous -->
				<div class="b1">
				
				<!-- hyphens can be troublesome when double clicking to copy -->
				<div class="display-item">
				
			Do this instead:
			
				<div class="blogArticle">
				
				<button class="primary_action">
				
			But, if you adopt a project, continue using whatever convention that has already been established. Don't mix and match.
			
		3. Try to avoid using too many classes. You can do this by using parent-child relationships, [pseudo-classes](http://www.w3.org/wiki/CSS/Selectors#Pseudo-classes), [pseudo-elements](http://www.w3.org/wiki/CSS/Selectors#Pseudo-elements) and [pattern matching](http://www.w3.org/TR/CSS2/selector.html#pattern-matching). Whatever you do, don't rely on just a bunch of classes.
		
			Try to avoid this:
			
				<article class="blog article sticky first yellow">
				
			Do this instead:
			
				<div class="blog">
					<article class="stickyArticle">
				
			Now you can use `.blog .stickyArticle {}` in your CSS and then `.blog div:first-child {}` to style the first element in the list.
			
		4. Try to use classes for CSS and ID's for Javascript. Using classes, rather than ID's, for CSS prevents many specificity problems, and encourages code reuse.
		
	2. ### ID's
	
		ID's must be unique and not shared with any other element in the document, they should follow the same naming pattern as classes and you can only have one ID per element. ID's should be reserved for JavaScript when possible.
		
	3. ### Style
	
		Style attributes should never be used, ever! Use classes to style elements.
		
	4. ### Events
	
		Inline Events like `onclick=""` should be used very carefully, if at all. Try to avoid mixing languages. If you do use it, make sure you are calling a single function that's on an external .js file.
		
5. ## Comments

	1. Comments should be used anytime there is ambiguity or complexity. If you are using PHP `includes` then a comment explaining what is being included is always a good idea.
	
	2. Use comments for closing tags that could be far from there opening tag. This helps debug issues where finding a close tag for a div can be near impossible when there are 20 div's between it and it's opening tag.
	
		Example:
		
			<body>
				<div class="content">
				
					…
					
					…
					
					…
				</div><!-- .content -->
			</body>
			
6. ## Conventions

	1. ### Use unordered lists for more than just text lists.
	
		If you have repeating, related content, whether they are multiple articles, images, videos, links … use unordered lists as elements.
	
		Don't do this:
		
			<div>
				<div>Stuff</div>
				<div>Stuff</div>
				<div>Stuff</div>
				<div>Stuff</div>
				<div>Stuff</div>
			</div>
			
		Do this instead:
		
			<ul>
				<li>Stuff</li>
				<li>Stuff</li>
				<li>Stuff</li>
				<li>Stuff</li>
				<li>Stuff</li>
			</ul>

		By using this convention, you'll have better control over the elements since they have a natural parent child relationship. Much can be done without the need for classes.
		
	2. ### Use HTML5 elements for extra semantics
	
		HTML5 has brought us a lot of great HTML elements that help us describe the content that they contain. This can eliminate the need for additional classes.
		
		// Briefly explain HTML5 elements …
		



	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	