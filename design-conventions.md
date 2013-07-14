## Suggestions for Styling Conventions

### Line Width & Height
1. The measure, aka "line length" should be between 20 to 40 times the width of the font's size. Using em's, that should mean 1em font-size should have the line-length of 20 to 40em. The longer the measure, the better for longer reading; the shorter the measure the better for quicker reading.
1. The leading, aka "line-height", should be 1.25, 1.333 or 1.5 times the size of an em. The longer the measure, see above, the taller the leading should be; this is to help prevent loss of reading location (finding the next line to read).			

### Element Spacing
1. Padding and margin should be factors of the leading (line-height). Normally, the distance between two elements should be half or a whole line-height distance (sometimes 1/4 is okay). This is to ensure a good vertical rhythm and a somewhat consistent baseline grid. But, one can use the base-line height as the base for all measure, both vertical and horizontal. Separation between paragraphs is normally a factor of 1, seperation of lists should be 0, 0.5 or 1 factor of the line-height.

### Contextual Links
1. Any `<a>` tag that is not easily distinguishable as a link (such as links in text, versus navigational links) should be underlined by default, with the underline removed on hover (unless some other distinguishable decoration is used, like a border or background). Don't just rely on text-color or a hover to distinguish as that is bad form.
			
### Decorative Elements
1. Text shadow should only be used on larger text, minimally so and for a good reason. The shadow should always be contrasting to the text (don't put a dark shadow on dark text). Lastly, if the text is dark, the shadow should be light colored and bottom-right. If the text is light, the shadow should be dark and top-left. This follows the convention of letterpress and follows the idea that the text is depressed and the light source is coming from top-left.
