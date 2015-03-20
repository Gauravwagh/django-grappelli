# Coding Standards #



## Javascript ##

UI components have been broken down in encapsulated jQuery UI widgets.

### Folder structure ###

| media/jquery/grappelli | Folder that contains all the grappelli code |
|:-----------------------|:--------------------------------------------|
| media/jquery/grappelli/src | Source code, this is where you modify widgets |
| media/jquery/grappelli/dist | Contains the compressed/minified distribution files |
| media/jquery/grappelli/src | Source code, this is where you modify widgets |
| media/jquery/grappelli/src | Contains external libraries |

### Build instruction ###

To compile and minify the source code use the following commands;

```

$: cd media/jquery/grappelli/
$: python build.py -m

```

This will generate the following files;

  * dist/jquery.grappelli.js
  * dist/jquery.grappelli.min.js

### Switching between droduction vs development code ###

Edit the file templates/admin/base.html to toggle between minified/merged and source code.

### Widget ###

[Official documentation](http://docs.jquery.com/UI_Developer_Guide#The_widget_factory)

#### Structure ####

Here's a minimal bare bone widget boiler plate:

```
$.widget('ui.gWidgetName', {
    options: {
        autoSelector: '#changelist',
	speed: 0.5
    },
    _init: function() {
        var ui = this;
	alert(ui.options.spee); 
    }
});
```

#### Variables ####

| `ui.element` | Element on which the widget was called |
|:-------------|:---------------------------------------|
| `ui.options` | Widget options object |

Now here's a breakdown of what's going on line by line.

  1. creating the widget, which will be callable via `$(selector).gWidgetName();`
  1. setting up default options. These options can be overrided at initialization time: `$(selector).gWidgetName({spee: 1.0});`
  1. `autoSelector` is a grappelli specific option used for widget autoloading
  1. `speed` is a simple default option example
  1. end options ..
  1. obviously `_init` is called upon initialization.
  1. grappelli widgets systematically use ui to refer at `this` for scope managing convenience.
  1. will alert 0.5

#### Public vs Private methods ####

Method prefixed with an underscore (_) will not be available publicly. Otherwise, the method will be accessible and callable like this;_

```
$(selector).gWidgetName('methodName', options);
```



#### Changing config after initialization ####

```
$(selector).gWidgetName('option', 'speed', 1.0);
```

### Global config manager ###

You can set and get global configurations with these methods;

```

$.grappelli.conf.set('Hello', 'World');

$.grappelli.conf.get('Hello'); // outputs 'World'

```

## CSS ##

### jQuery UI CSS Framework ###

| `.ui-helper-hidden` | Applies display: none to elements. |
|:--------------------|:-----------------------------------|
| `.ui-helper-hidden-accessible` | Applies accessible hiding to elements (via abs positioning off the page) |
| `.ui-helper-reset` | A basic style reset for UI elements. Resets things such as padding, margins, text-decoration, list-style, etc. |
| `.ui-helper-clearfix` | Applies float wrapping properties to parent elements. |
| `.ui-helper-zfix` | Applies iframe "fix" css to iframe elements when needed in overlays. |

[Full API documentation](http://docs.jquery.com/UI/Theming/API)