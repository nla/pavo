PAVO Widgets
============

**Beware:** This is currently just a placeholder. This project does not exist yet in a usable form.

Assorted JavaScript widgets for rich digital collection delivery.

Usage
-----

TODO

Widget Reference
----------------

* Books
* Audio
* Misc
 - contactus &mdash; simple feedback form
 - toolbar &mdash; a bar of buttons

Anatomy of a PAVO Widget
------------------------

A typical widget consists of five files plus any additional static assets.

    widgets/helloworld/
        README.md
        config.json
        _helloworld.erb
        helloworld.js
        helloworld.css
        images/
            background.png

### Documentation (README)

Each widget should have a README file with short description of it's purpose and the configuration options
it supports.

```markdown
HelloWorld Widget
=================

Displays a friendly greeting.

## Options

- message: the text to display
```

### Configuration (JSON)

```JSON
{
    "js": [
        "widgets/helloworld/helloworld.js"
    ]
}
```

### Templates (ERB + JST)

Use [ERB syntax] like `<%= foo %>` for server-side templating and [JST syntax] like `${foo}` for the client-side.
It's normal to mix both in the same file.

```HTML
<link rel="stylesheet" type="text/css" href="<%= app_path %>widgets/helloworld/helloworld.css"/>
<div class="pavo-widget helloworld" id="helloworld">
  <div class="saying-hi-to-the-world"></div>
  
  <div id="helloworld_message_template"><!--
    <p>${message}</p>
  --></div>
</div>
```

[ERB syntax]: http://ruby-doc.org/stdlib-1.9.3/libdoc/erb/rdoc/ERB.html
[JST syntax]: https://code.google.com/p/trimpath/wiki/JavaScriptTemplateSyntax

### Stylesheets (CSS)

All widgets must have a top-level class of `.pavo-widget`.

```CSS
.pavo-widget.helloworld p {
    text-decoration: blink;
}
```

### Behaviour (JavaScript)

```JS
require([], function() {
  PAVO.widgets.helloworld = function (wid) {
    // Variables
    var rootel = "#" + wid;

    // Events
    function addListeners() {
    }

    // Methods

    // Initialisation
    function init() {
      addListeners();
      $(".saying-hi-to-the-world", rootel).html(PAVO.templates.render("helloworld_message_template", {
 message: "Hello world"
      }));
    }
    init();
  }

  PAVO.widgets.informLoaded("helloworld");
});
```

Dependencies
------------

Core dependencies:
 - [RequireJS](http://requirejs.org/) for modularity
 - [jQuery](http://jquery.com/) for events and DOM manipulation
 - [Ruby](http://www.ruby-lang.org) for server-side templates
 - [TrimPath JavaScript Templates](https://code.google.com/p/trimpath/wiki/JavaScriptTemplates) for client-side templates

For audio widgets:
 - [jPlayer](http://jplayer.org/) for audio playback

License
-------

TODO