# HTML

## Contents

* [Tags Reference](#tags-reference)
  * Sectioning
* [Text Editors](#text-editors)
  * Visual Studio Code
  * Atom
  * Emacs
  * Vi/Vim
---

HTML (HyperText Markup Language) is used to lay out the structure of a webpage.

`<!DOCTYPE html>` is placed at the start of an HTML file to indicate to the browser that HTML5 is being used.

HTML is made up of tags. Tags generally come in pairs, with data being in between the tags. Generally, tags are indented to help visualize their hierarchy, but any indentation is purely stylistic. Tags can also have attributes, which are data fields, sometimes required and sometimes optional, that provide additional information to the browser about how to render the data.

The Document Object Model is a way to conceptualize webpages by representing them as an interconnected hierarchy of nodes. In HTML, the nodes of the DOM would be the different tags and their contained data, with the `<html></html>` tag being at the very top of the tree.

## Tags Reference

There are lots of useful tags with HTML5, but not all browsers, especially older browsers, will support these new features. Nonetheless, these new features can be used with increasing confidence that they will be rendered appropriately for a significant portion of users.

* `<html></html>` contents of the website
* `<head></head>` metadata about the page that is useful for the browser when displaying the page
* `<title></title>` title of the page
* `<body></body>` body of the page
* `<h1></h1>` header (h1 is the largest header, h6 is the smallest one)
* `<ul></ul>` unordered list
* `<ol></ol>` ordered list
* `<li></li>` list item (must be inside either `<ul></ul>` or `<ol></ol>`)
* `<img src="path/to/img.file" height="200" width="300">` image stored at _src_ attribute, which can also be a URL. Note that this is a single tag without an end tag. Both _height_ and _width_ are optional (if one is omitted, the browser will auto-size the image), and can also take a percentage: _height=50%_ to automatically scale the image to a certain portion of the page
* `<table></table>` table
* `<th></th>` table header (must be inside `<table></table>`)
* `<tr></tr>` table row (must be inside `<table></table>`)
* `<td></td>` table data (cell, must be inside `<tr></tr>`)
* `<form></form>` form that can be filled out and submitted by the user
* `<input type="text" placeholder="Full Name" name="name">` input field. _type_ attribute indicates the type of data, _placeholder_ is the greyed-out text shown before the field is filled, and _name_ is an identifier for the input field
* `<input type="radio"> Option 1` radio-button option for a form, where only one out of all the options may be selected
* `<button></button>` button used to submit the form
* `<a href="path/to/file.html">Hi!</a>` link to file.html, some URL, or some other content marked by id by passing #id to _href_

### Sectioning

Two special tags allow us to break up a our webpage into sections:

`<div></div>` vertical division of a webpage
`<span></span>`  section of a webpage inside, for example, text

Both `<div></div>` and `<span></span>` don’t really do much by themselves, but they allow for the labelling of sections of a webpage. Different sections of a webpage can be referenced with the _id_ and _class_ attributes. ids uniquely identify elements, but there can be an arbitary number of elements with a given class.

## Text Editors

[Visual Studio Code](https://code.visualstudio.com/)

Visual Studio Code is a source code editor developed by Microsoft that includes support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring.

* Available for Windows, Mac, Linux
* Cost: Free
* Style: GUI

[Atom](https://atom.io/)

Atom is a free and open-source text and source code editor for macOS, Linux, and Microsoft Windows with support for plug-ins written in Node.js, and embedded Git Control, developed by GitHub.

Both Atom and Visual Studio Code are hugely popular and the majority of web developers will probably be using one or the other. Both feature multiple cursors and they share many of the same keyboard shortcuts. Also much like Visual Studio Code, Atom has a rich ecosystem of packages that you can use to customize your editor.

* Available for Windows, Mac, Linux
* Cost: Free
* Style: GUI

[Emacs](https://www.gnu.org/software/emacs/)

Emacs is an open source text editor that's been around since the 1970s. Along with Vim, it's one of the most popular Linux text editors.

Emacs is often described as an operating system because even in a clean install there are several included applications that you wouldn't expect inside a text editor, like a news reader, several calculators, a number of games, file encryption/decryption, and a package manager for plugins written in Emacs Lisp.

All Emacs commands exist in the same namespace so it's not uncommon to differentiate commands by having chains of keystrokes like Ctrl-x Ctrl-f to open a file. Because of the incredible customizability, it's among the editors with the steepest learning curves. You will most likely want to customize it: installing plugins, trying them, testing for conflicts, uninstalling the ones that have conflicts, and repeating.

* Available for Windows, Mac, Linux
* Cost: Free
* Style: Command-Line or GUI


[Vi/Vim](https://www.vim.org/)

Vim, or Vi IMproved is the other text editor in the Unix Editor Wars. Vim runs anywhere that standard C can run and is often in the base install for most Linux and non-Windows systems including macOS. It also offers a fairly robust tutorial to learn how to use it. Learn it once and you can use it everywhere.

Vim relies on modes, or scopes, when certain commands are applicable. In the command mode, the user can move around a file or execute commands. For instance, in insert mode, you can edit a file. While you are creating an HTML file (and are in HTML mode), you might be able to expand html:5 into the boilerplate for an empty HTML file.

* Available for Windows, Mac, Linux
* Cost: Free and open source
* Style: Command Line or GUI
