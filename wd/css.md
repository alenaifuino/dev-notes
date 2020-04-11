# CSS

CSS (Cascading Style Sheets) is a language used to interact with and style HTML, changing the way it looks according to a series of rules. CSS is what makes websites look nice.

CSS can be applied to HTML in a variety of ways:

* The *style* attribute `<h5 style="color:blue;text-align:center;"></h5>`. The semicolon-separated CSS properties passed to *style* will be applied to whatever the tag contains.
* The `<style></style>` tags. This is a useful paradigm to use when reusing the same styling many times throughout a page. The properties listed will apply to all of the tags that are listed.
* A separate .css file: add `<link rel="stylesheet" href="path/to/styles.css">` to the header, and move the CSS code (same format as used inside the `<style></style>` tags). This is often an even better paradigm because it separates two distinctly different things: structure (HTML) and style (CSS), while also being easier to manage and read.

## Common CSS properties

Those that take arguments in pixels often can take a percentage or simply auto:

* `color: blue`, `color: #0c8e05` can be 1 of ~140 named colors, or a hexadecimal value that represents an RGB value
* `text-align: left` aligns text to left; other possible arguments are center, right, or justify
* `background-color: teal` sets the background to a color, which is the same format as the color property
* `height: 150px` sets the height of an area, in this case to 150px
* `width: 150px` sets the width of an area, in this case to 150px
* `margin: 30px` sets the margin around all four sides of an area, in this case to 30px. Can also be broken up into margin-left, margin-right, margin-top, and margin-bottom
* `padding: 20px` sets the padding around text inside an area. Can be broken up the same way as margin
* `font-family: Arial, sans-serif` sets the font family to be used. A comma-separated list provides alternatives in case a browser doesn’t support a specific font. Generic families such as sans-serif will use browser defaults
* `font-size: 28px` sets the font size
* `font-weight: bold` sets the font weight to quality, a relative measure (lighter), or a number (200)
* `border: 3px solid blue` sets a border around an area.

There are lots of CSS properties that can be used in a lot of different ways. Check out the [extensive documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) for more information.
