bmiegemolle.github.io
=====================

This is the repository of my home page, which is accessible with the following URLs:

* [http://www.miegemolle.net](http://www.miegemolle.net)
* [http://bmiegemolle.github.io](http://bmiegemolle.github.io)

---

Layout structure highlights
---------------------------

### The root folder

It contains (among other things) all standard pages in English version, such as:

* `index.html`
* `phd.html`
* `blog.html`
* ...

### The `fr` folder

It contains all standard pages (the same as the ones in the root folder), translated in French.

### The `_layouts` folder

This folder contains all layout files, i.e:

* `default.html`: the layout for standard pages in English version (with menus and right frames in English)
* `default_fr.html`: the layout for standard pages in French version (with menus and right frames in French)
* `post.html`: the layout for blog posts (only available in English version)
* `tech.html`: the layout for technical notes (only available in English version)

### The `_posts` folder

All blog posts go in this folder.

### The `tech` folder

This folder contains all multipage technical notes. A folder is created for each note that will include a page per note.

```
tech
    + writing-a-jenkins-plugin
    |     + 01-project-setup.md
    |     + 02-test-your-plugin.md
    |     + 03-deploy-your-plugin.md
```

### The `_includes` folder

It contains all HTML files to be included in other files, in particular:

* `header.html` and `footer.html` used in `_layout/*` files
* a subfolder `tech` that contains monopage technical notes (or menu of multipage ones), that are include in both English and French versions of the technical notes root page.

---

Credits
-------

This website makes use of:

* [Jekyll](http://jekyllrb.com/)
* [Bootstrap](http://getbootstrap.com/)

The icon resources I use are coming from:

* https://www.iconfinder.com/search/?q=iconset%3Awindows-8-metro-style
* https://github.com/danleech/simpleicons
