Notes, comments and discussion about changes in my branch.

# Template blocks #

## {% block javascripts %} ##

This block contains the whole JavaScript initialization. By default it goes something like this;

```
{% block javascripts %}
<script type="text/javascript" src="{% admin_media_prefix %}jquery/jquery-1.3.2.min.js"></script>
<script type="text/javascript">
    var ADMIN_URL = "/{% get_admin_url %}/";
    var ADMIN_MEDIA_PREFIX = "{% admin_media_prefix %}";
    var BOOKMARKS_URL = "{% url grp_bookmark_get %}";
    {% get_generic_relation_list %}
    $(function(){
      {% block javascripts.init  %}
        {% include "admin/init.js"  %}
      {% endblock %}
    });
</script>
{% endblock %}
```

You shouldn't have to override this block. You'll most likely to need to customize
widgets initialization, which are located within the `javascripts.init` tag.

## {% block javascripts.init %} ##

Widgets initialization takes place in a block called "javascript.init" which is inside
the block "javascripts". This block will be used to override JavaScript options.

```

$(function(){
  {% block javascripts.init  %}
    {% include "admin/init.js"  %}
  {% endblock %}
});

```

As you can see it actually include a js file containing the actual initialization scripts.
This way it's easy to override only the initialization and pass custom parameters without having to touch grappelli's templates.

To do this simply create a folder named `admin` in your templates folder and create a file named `init.js` (or copy the grappelli one).

Currently the `init.js` file look like this;

```

$.fx.speeds._default = 0; // remove all animations
$('#bookmarks').gBookmarks({url: BOOKMARKS_URL});
$('.changelist-content').gChangelist();
$('#changelist').gActions();
$('input.vTimeField').gTimeField();
$('input.vDateField').gDateField();
$('.inline-group').gInlineGroup();
$('.inline-stacked').gInlineStacked();
$('.inline-tabular').gInlineTabular();

```

You can use this code, however I would advise using the `init.js` file located in `grappelli/templates/admin/` as template since it might have changed since the time I'm writing this.

# jquery grappelli #

## jquery.grappelli.js ##

Provide the base for all grappelli widgets, the dirty hooks and hacks are mostly likely hidden there.

It also provide a popup functionality for the Change history of objects, like this;

![http://imgur.com/0UM7q.png](http://imgur.com/0UM7q.png)

## ui.gAutocomplete.js (dev) ##

### FK Autocomplete widget ###

#### Admin configuration ####

```
from grappelli.admin import GrappelliModelAdmin
class MyModelAdmin(GrappelliModelAdmin):
    list_display = ('__unicode__',)
    autocomplete = {
        'fk_field_name': {
            'search_fields': ('username', 'first_name', 'last_name'),
            'input_format':  '{label:s}',           # optional
            'list_format':   '{id:d} - {label:s}',  # optional
        }
    }

```

#### Options ####

|**Option**|**Description**|
|:---------|:--------------|
|`search_fields`| On which fields to perform the search |
|`input_format`| Object format in the input field (display format, not save format) |
|`list_format`| Objects format of the result list |

This is the first draft:

**Default appearance**

![http://imgur.com/q7cO6.png](http://imgur.com/q7cO6.png)

**Focused**

![http://imgur.com/zAYWH.png](http://imgur.com/zAYWH.png)

**Completing**

![http://imgur.com/hhYkO.png](http://imgur.com/hhYkO.png)

`*` Note: the orange is a system color of my os (under Windows this would most likely be blue)

**Browse button**

![http://imgur.com/WhHg5.png](http://imgur.com/WhHg5.png)

## ui.gAutoSlugField.js ##

This field can work in two way, the first is standalone where only a slugfield is presented to the user. The other way is with a related field like below. The slugfield
gets updated as the related field is changed;

![http://imgur.com/KQnF4.png](http://imgur.com/KQnF4.png)

| **options**  | **default** | **description** |
|:-------------|:------------|:----------------|
| delay | `0.8` | Delay after keyup before slugify (this is necessary to allow the user to type) |


## ui.gBookmarks.js ##

Replacement for Bookmark.js.

![http://imgur.com/vYUL4.png](http://imgur.com/vYUL4.png)

### Options ###

| **options**  | **default** | **description** |
|:-------------|:------------|:----------------|
| url | `/grappelli/bookmark/get/` | URL for the Ajax loading of bookmarks |
| effects | `false` | Use UI effects |


## ui.gChangelist.js ##

Replacement for Changelist.js.


## ui.gInlines ##

### ui.gInlineGroup ###

Mainly take care of UI behavior of inline groups (stacked & tabular).

  * Handles "add" button
  * Handles inline "delete" buttons
  * Handles open/collapse of groups
  * Handles ordering (almost working)

### ui.gInlineStacked ###

This widget takes care of inline stacked elements.

### ui.gInlineTabular ###

This widget takes care of inline tabular elements.


## ui.gDateField.js ##

Provide date field calendar using the jQuery UI datepicker.

![http://imgur.com/wX4cq.png](http://imgur.com/wX4cq.png)

### Default datepicker options ###

| **options**  | **default** | **description** |
|:-------------|:------------|:----------------|
| dateFormat  | `'yy-mm-dd'` | Date formet |
| buttonImageOnly | `true` | Button without text |
| showOn | `'button'` | Show only when button is clicked (ie: not focused field) |
| showButtonPanel | `true` | Show "Cancel" and "Today" buttons |
| closeText | `gettext('Cancel')` | Show "Cancel" and "Today" buttons |
| buttonImage | ADMIN\_MEDIA\_PREFIX +'img/icons/icon-calendar.png' | Image path for the button |

For a complete list of the Datepicker options please refer to the official jQuery UI documentation: http://docs.jquery.com/UI/Datepicker


## ui.gTimeField.js ##

This is a jQuery reimplementation of the "clock picker" found in Grappelli2.

![http://imgur.com/YhBUy.png](http://imgur.com/YhBUy.png)

As you can see not much changed in appearance.

### Options ###

| **options**  | **default** | **description** |
|:-------------|:------------|:----------------|
| buttons | `[]` | List of button (check example below) |

| closeText | `gettext('Cancel')` | Show "Cancel" and "Today" buttons |
|:----------|:--------------------|:----------------------------------|
| buttonImage | ADMIN\_MEDIA\_PREFIX +'img/icons/icon-calendar.png' | Image path for the button |

Example list of button (default one actually):

```
[
   {label: 'Now', callback: function(e, ui){ 
       return ui.element.val(new Date().getHourMinuteSecond()); 
   }},
   {label: 'Midnight', callback: function(e, ui){ 
       return ui.element.val('00:00:00'); 
   }},
   {label: '06:00', callback: function(e, ui){ 
       return ui.element.val('06:00:00'); 
   }},
   {label: 'Noon', callback: function(e, ui){ 
       return ui.element.val('12:00:00'); 
   }}
]
```

## ui.gActions.js ##

Admin actions hook.

## ui.gSelectFilter.js (proposal/removed) ##

I'm currently trying to implement a more intuitive way to handle permission.. here's what it looks so far:

![http://imgur.com/EIC5u.png](http://imgur.com/EIC5u.png)

**Note**: I've removed this plugin for the moment. A generic implementation is too difficult to achieve without refactoring some core components of Django, which seems an enormous overhead at the moment.

## ui.gSelectFilter.js (actual) ##

Same select filter, jQuery style.

![http://imgur.com/d6eyj.png](http://imgur.com/d6eyj.png)

## jquery.urlify.js ##

Basically the same as the old URLify.js but scoped into an anonymous function and made accessible via `$.urlify` to avoid polluting the global namespace.

# Other changes #

## collapse-open and collapse-open-items ##

It's now possible to control the collapse state of inline groups
and inline items independently.

**Example:**

```

class MyModel(admin.ModelAdmin):
    classes = ('collapse-open collapse-closed-items',)
    # ...

class MyModel2(admin.ModelAdmin):
    classes = ('collapse-open collapse-open-items',)
    # ...

```

# Themeroller #

The calendar and popup (for the object history) are themed with jQuery UI Themeroller.

[This is the currently used theme](http://alturl.com/52ht).


# Todo #

  * find a proper autocomplete widget
  * remove core.js
  * remove admin/ordering.js
  * remove admin/RelatedObjectLookups.js

# Changes #

  * jQuery UI 1.7.2 integration
  * created a [jQuery UI theme](http://alturl.com/m4pf) with grappelli's colors
  * removed Bookmark.js, created a jQuery widget (gBookmarks in jquery.grappelli.js)
  * removed Changelist.js, created a jQuery widget (gChangelist in jquery.grappelli.js)
  * removed Inline.js, created a jQuery widget (gInlineStacked and gInlineTabular in jquery.grappelli.js)
  * created jquery.grappelli.js which contains grappelli widgets
  * refactored SelectBox.js (minor refactors/optimizations
  * refactored SelectFilter2.js (minor refactors/optimizations)
  * removed actions.js, created a jQuery widget (gActions in jquery.grappelli.js)
  * removed calendar.js, replaced with jQuery UI Datepicker
  * removed dateparse.js, jQuery provide date parsing facilities
  * removed getElementsBySelector.js, obsoleted by jQuery
  * removed timeparse.js, didn't find anywhere where it was used..
  * refactored urlify.js, created jquery.urlify.js to replace it
  * "History" button now opens a dialog (will make it optional and disabled by default if needed)
  * removed CollapsedFieldsets.js, created a jQuery widget (gInlineGroup in jquery.grappelli.js)
  * removed CollapsedInlineFieldsets.js, created a jQuery widget (gInlineStacked in jquery.grappelli.js)
  * removed DateTimeShortcuts.js, created a jQuery widget (gTimeField and gDateField/gTimeField in jquery.grappelli.js)
  * created gAutocomplete and gFacelist (for FK and M2M autocompletes)
  * added `collapse-open-items` class
  * max length of related lookup text now include the suffix " ..."
  * suffix " ..." of related lookup text is now configurable (maxTextSuffix)
  * max length of related lookup text is now configurable (maxTextLength)
  * unescape now works on all characters instead of a limited subset
  * when adding a related object, it is now added in all other inlines selects as well


# Todo #

  * autocomplete theme
  * iron out themeroller theme
  * change drag handles
  * related lookups (m2m)
  * JavaScript merge/minify