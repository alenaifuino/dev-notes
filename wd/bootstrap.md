# Bootstrap
---

[Bootstrap](https://getbootstrap.com/) is a CSS library written to help make clean, responsive, and nice-looking websites without having to remember the gritty details about flexboxes or grids everytime a layout needs to be set up.

The only thing needed to use Bootstrap is by adding a single line which links Bootstrap’s CSS stylesheet:

```css
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
```

Bootstrap’s CSS will make everything look a little cleaner and more modern, but its real power comes with its layout system. Bootstrap uses a column-based model where every row in a website is divided into 12 individual columns, and different elements can be alloted a different number of columns to fill.

Bootstrap’s columns and rows are referenced in HTML with `class="row"` and `class="col-3"` attributes, where the number after `col-` is the number of columns the element should use.

Elements can take up a different number of columns based on the size of the screen with attributes like `class="col-lg-3 col-sm-6`. On a small screen, six columns will be used, but in a large screen, three columns will be used. If another row has to be added, Bootstrap will do so automatically. This is a much easier alternative to something like flexbox (Bootstrap does so behind the scenes).

Bootstrap has a whole host of other pretty components which can easily be applied by simply adding the appropriate class attribute to an element. See Bootstrap’s [documentation](https://getbootstrap.com/docs/4.4/components/alerts/) for an extensive list.
