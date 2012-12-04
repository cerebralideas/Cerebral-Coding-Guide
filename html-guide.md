# Cerebral Code-Style for HTML

## Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!

	If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.
	
	For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.	
1. Never leave whitespace at line ends or within blank lines. Many editors and IDE's have a setting to remove all unnecessary white-space.
	
1. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
	- Enforced consistency
	- Eliminating end of line whitespace
	- Eliminating blank line whitespace
	- Commits and diffs that are easier to read
	
1. Set your line length at a maximum of 120 characters
		
1. Insert line-breaks, `\n`, after tag closures, `</>` or closing quote for attributes.
	
1. Double line-breaks should be used to separate same level elements from one another for increased readability.

## Know Your Elements

### Block Elements
	
Common block HTML4 elements:
	
`<html>` `<body>` `<div>` `<ul>` `<li>` `<p>` `<blockquote>` `<h1> - <h6>` `<table>` `<form>` `<fieldset>`
		
New block HTML5 elements:
		
`<header>` `<section>` `<article>` `<footer>` `<aside>`
	
Block-level elements represent a horizontal section of a document. These elements span the whole width of their container or parent element. Block-level elements can contain other block-level elements.
		
Block level elements do not need a break tag, `<br/>`, afterward to ensure any element falls below.
		
Don't do this:
		
	<div><!-- stuff --></div><br/>
			
The break tag is not needed since block elements naturally take up the whole width of the container element.
		
### Inline Elements
	
Common inline HTML4 elements:
		
`<a>` `<span>` `<strong>` `<img>`
		
Inline elements have no inherent width. These elements can be zero pixels wide to the full width of the container element. They get their width by whatever they are containing. So, if you have, say, an `<img>` element, it will just in herent the width of the actual image file it contains.
		
Their height is also dictated by what they contain. Inline elements can't (and won't follow) any top or bottom margin and padding; you can't set any height either.
		
Inline elements should not contain block elements.
		
### Inline-Block Elements
	
There are no natural `inline-block` elements (at least not within the current HTML5 standard), but block elements are best to convert to `inline-block`. These elements are created by the `display: inline-block;` property in CSS. These elements have properties of both block elements and inline. `inline-block` elements can contain any kind of element — block or inline.
		
`inline-block` elements take on the width of whatever they contain, unless specified otherwise. If an `inline-block` element contains a block element, then it will take up the full width of its container. If it contains an inline element, it is the width of whatever it contains. Therefor, if you place a block-level element within an `inline-block` element, you'll need to set a width.
		
### Style (Block) Element

Rarely, if ever, use the `<style>` block element. There are very few reasons to write css within style tags in HTML. Always use external stylesheets!
	
*The one exception is if you need to declare IE specific styling with a conditional stylesheet.*
	
### Script Element

Including inline or in-page JavaScript should be avoided as much as possible. This again is going back to not mixing languages. JavaScript should be in .js files, CSS should be in .css files and HTML should be in .html files. So, if you have some page specific JavaScript that you don't want on your `site.js` file, create a separate `page.js` file and include it in just that page.
	
Don't do this:
	
	<script type="text/javascript">
			
		// Bunch of JS functions and specific to your page.
			
	</script>
		
	Do this instead:
	
		<script type="text/javascript" src="/js/page.js"></script>
	
But remember, cache anything that is used frequently throughout the site. If you are including different .js files throughout your site, find ways to write more reusable JavaScript so that you include it once and for all.

## Attributes

### Classes
	
1. Classes are traditionally used to add the hooks necessary for CSS styling, so *try* to avoid using classes for selecting elements in JS. If you do use classes for selection in JS, then it's best to use a separate class with the prefix of `js-` so that other developers know which classes are used for styling and which are used for the JS. If you don't, another developer could easily change the class to alter styling, and accidentally break the site's JS.
		
1. Name classes with semantic names that describe either their content or their purpose. **Remember: use a naming convention that someone that is unfamiliar with the project could read and understand its use.** I prefer using camel case for classes and id naming. Underscores can also be used for complex names, but once you choose a convention, stick with it.
		
	Don't do this:
			
		<!-- Too ambigous -->
		<div class="b1">
				
		<!-- Hyphens can be troublesome when double clicking to copy -->
		<!-- Try to double click the class below -->
		<div class="display-item">
		<!-- You can't can you? That's why I hate using hyphens -->
				
	Do this instead:
			
		<div class="blogArticle">
				
		<button class="primary_action">
				
**But, if you adopt a project, continue using whatever convention that has already been established. Don't mix and match.**
			
1. Try to avoid using too many classes. You can do this by using parent-child relationships, [pseudo-classes](http://www.w3.org/wiki/CSS/Selectors#Pseudo-classes), [pseudo-elements](http://www.w3.org/wiki/CSS/Selectors#Pseudo-elements) and [pattern matching](http://www.w3.org/TR/CSS2/selector.html#pattern-matching). Whatever you do, don't rely on just a bunch of classes.
		
	Try to avoid this:
			
		<article class="blogItem article sticky first yellow">
					
	Do this instead:
			
		<div class="blog">
			<article class="stickyArticle">
				
	Now you can use `.stickyArticle {}` in your CSS and then `.blog > div:first-child {}` to style the first element in the list. *Please note: if you do use a generic element as the end node, make sure to use the `child-selector` for performance with at least the immediate parent selector with a class.*
			
1. Try to use classes for CSS and ID's for Javascript. Using classes, rather than ID's, for CSS prevents many specificity problems, encourages code reuse, ad ID's are much faster for JS.
If you do use classes for JS, prefix them with js-, so that other developers understand your intent and not think it's for style.
		
### ID's
	
ID's must be unique and not shared with any other element in the document, they should follow the same naming pattern as classes and you can only have one ID per element. ID's should be rather permanent and not modified often. ID's should be reserved for JavaScript when possible, and not used in CSS.
		
Why should you try to avoid using ID's in CSS? Well, because it's easy to get into a messy CSS specificity issue as ID's take precendence over other selector types. 
		
### Style
	
Style attributes should never be used, ever! Use classes to style elements.
		
### Events
	
Inline Events like `onclick=""` should be used very carefully, if at all. Try to avoid mixing languages. If you do use it, make sure you are calling a single function that's on an external .js file. No logic or statements other than a single function call should be contained within a inline event.
		
## Comments

1. Comments should be used anytime there is ambiguity or complexity.
	
	Example:
		
		<?php
	
			/* Custom WP Carousel Loop:
					* Create new hero query from the custom post 
					* type Hero Carousel Items, loop through the items
					* and post them to page.
			*/
	
			// Custom hero query
			$hero_query = new WP_Query('post_type=hero_carousel_items&&oderby=menu_order');
				
			// Post counter: used for alternating image placement
			$postCount = 0;
	
			// Loop through the retrieved items
			while ($hero_query->have_posts()) : $hero_query->the_post(); ?>
	
				<?php $postCount++; ?>				
				<?php include 'hero.php'; ?>
	
			<?php endwhile; ?>
	
1. Use comments for closing tags that could be far from there opening tag. This helps debug issues where finding a close tag for a div can be near impossible when there are 20 div's between it and it's opening tag.
	
	Example:
			
		<body>
			<div class="content">
					
						…
						
						…
						
						…
			</div><!-- .content -->
		</body>
			
## Conventions

### Use unordered lists for more than just text lists.
	
If you have repeating, related content, whether they are menus, multiple articles, images, videos, links … use unordered lists as elements.
	
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

### Use the least amount of elements as possible.

For maintainablity purposes and performance reasons, the least amount of elements to create the needed structure, the better. To accomplish this, use CSS3 to remove the need to redundant element wrapping, like for rounded corners and such.

## Know Your HTML5 Elements

Coming soon …