# Cerebral Code-Style for CSS

1. ## Whitespace Rules

	A. Never mix spaces and tabs; this is the **law**!
	
	B. If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.
	
		For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.
	
	C. Never leave whitespace at line ends or within blank lines.
	
	D. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	
		- Enforced consistency
		
		- Eliminating end of line whitespace
		
		- Eliminating blank line whitespace
		
		- Commits and diffs that are easier to read
		
		
	F. Insert line-breaks, `\n`, after tag closures, `</>`.
	
	G. Double line-breaks should be used to separate same level elements from one another for increased readability.

2. ## Know Your Elements

	A. ### Block Elements
	
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
		
	B. ### Inline Elements
	
		Common inline HTML4 elements:
		
		`<a>` `<span>` `<strong>` `<img>`
		
		Inline elements have no inherent width. These elements can be zero pixels wide to the full width of the container element. They get their width by whatever they are containing. So, if you have, say, an `<img>` element, it will just in herent the width of the actual image file it contains.
		
		Their height is also dictated by what they contain. Inline elements can't (and won't follow) any top or bottom margin and padding; you can't set any height either.
		
		Inline elements should not contain block elements.
		
	C. ### Inline-Block Elements
	
		There are no natural `inline-block` elements, but block elements are best to convert to `inline-block`. These elements are created by the `display: inline-block;` property in CSS. These elements have properties of both block elements and inline. `inline-block` elements can contain any kind of element — block or inline.
		
		`inline-block` elements take on the width of whatever they contain, unless specified otherwise. If an `inline-block` element contains a block element, then it will take up the full width of its container. If it contains an inline element, it is the width of whatever it contains.

3. ## Attributes

	A. ### Classes
	
		1. Classes are traditionally used to add the hooks necessary for CSS styling. 
		
		2. Name classes with semantic names that describe either their purpose or their content. **Remember: use a naming convention that someone that is unfamiliar with the project could read and understand. Use either camel case or underscores for complex names.
		
			Don't do this:
			
				<!-- Too ambigous -->
				<div class="b1">
				
				<!-- hyphens don't allow double-click highlighting -->
				<div class="display-item">
				
			Do this instead:
			
				<div class="blogArticle">
				
				<button class="primary_action">
				
			But, if you adopt a project, continue using whatever convention that has already been established. Don't mix and match.
			
		3. Try to avoid using multiple classes if possible.
		
			Try to avoid this:
			
				<article class="blog article sticky first yellow">
				
			Do this instead:
			
				<div class="blog">
					<article class="stickyArticle">
				
			Now you can use `.blog .stickyArticle {}` in your CSS and then `.blog div:first-child {}` to style the first element in the list.
			
		4. Try to use classes for CSS and ID's for Javascript. Using classes rather than ID's for CSS prevents many specificity problems, and encourages code reuse.
		
	B. ### ID's
	
		ID's must be unique and not shared with any other element in the document, they should follow the same naming pattern as classes and you can only have one ID per element. ID's should be reserved for JavaScript when possible.
		
	C. ### Style
	
		Style attributes should never be used, ever! Use classes to style elements.
		
	D. ### Events
	
		Inline Events like `onclick=""` should be used very carefully, if at all. Try to avoid mixing languages.
		
4. ## Comments

	A. Comments should be used anytime there is ambiguity or complexity. If you are using PHP `includes` then a comment explaining what is being included is always a good idea.
	
	B. Use comments for closing tags that could be far from there opening tag. This helps debug issues where finding a close tag for a div can be near impossible when there are 20 div's between it and it's opening tag.
	
		Example:
		
			<body>
				<div class="content">
				
					…
					
					…
					
					…
				</div><!-- .content -->
			</body>
			
5. ## Conventions

	A. ### Use unordered lists for more than just text lists.
	
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
		
	B. ### Use HTML5 elements for extra semantics
	
		HTML5 has brought us a lot of great HTML elements that help us describe the content that they contain. This can eliminate the need for additional classes.
		



	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	