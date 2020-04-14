# Sass
---

Sass is an entirely new language built on top of CSS which gives it a little more power and flexibility when designing CSS stylesheets and allows for the generation of stylesheets in a programmatic way. Ultimately, Sass just makes writing CSS easier.

In order to use Sass, it must first be installed. Once [installed](http://sass-lang.com/install), we can execute `sass style.scss style.css` to compile our Sass file style.scss into sass.css, which can actually be linked to and interpreted by an HTML file.

If recompiling gets annoying, `sass --watch style.scss:style.css` to automatically recompile `style.scss` as `style.css` whenever `style.scss` is modified. Additionally, many website deployment systems, like GitHub Pages, have built in support for Sass. For example, if an .scss file is pushed to GitHub, GitHub Pages will compile it automatically.

One feature of Sass is variables, which are defined as so: `$color: red;`. Anywhere `$color` is passed as a value for a CSS property, e.g. `color: $color`, *red* will be used.

Another feature is nesting, which is a more concise way to style elements which are related to other elements in a certain way.

All `p`s inside `div`s will be have `color: blue`, but also `font-size: 18px`, while `ul`s inside `div`s will have `color: green` instead, but still also `font-size: 18px`.

```css
div {
    font-size: 18px;
    p {
        color: blue;
    }
    ul {
        color: green;
    }
}
```

Another useful feature is *inheritance*, which is similar to the object-oriented concept. Sass’s inheritance allows for slight tweaking of a general style for different components.

`%message` defines a general pattern that can be inherited in other style definitions using the `@extend %message` syntax. In addition, other style properties can be added.

```css
%message {
    font-family: sans-serif;
    font-size: 18px;
    font-weight: bold;
}

.specificMessage {
    @extend %message;
    background-color: green;
}
```
