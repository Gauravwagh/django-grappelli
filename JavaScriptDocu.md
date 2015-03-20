# Javascript Documentation #

This page gives you basic information about the JavaScript code of grappelli.

## Loading Order ##

Here I try to explain what JS files grappelli loads, and a short description which code is executed onReady/onLoad.

You can always (re)check this yourself by using firebugs _Net_ tab selecting _JS_. Which is highly recommended, because it often depends on your configuration (Model, AdminModel, tinymce setup, admin\_tools, filebrowser,...) which js-files are loaded.

  * `media/admin/jquery/jquery-1.4.2.min.js`
  * `media/admin/jquery/ui/js/jquery-ui-1.8.custom.min.js`
    * datepicker functionality
  * `media/admin/js/grappelli.init.js`
    * assigns `jQuery.noConflict(true)` to `django.jQuery`
  * `media/admin/js/grappelli.timepicker.js`
    * grappellis timepicker (ui.widget)
  * `media/admin/js/grappelli.RelatedObjectLookups.js`
    * js magic for raw\_id\_field, m2m\_fields, generic\_foreign\_key,...
    * onReady
      * assigns event listeners
      * makes dom maipulation for html which is hardcoded in django.contrib.admin's python code
  * `media/admin/js/grappelli.min.js`
    * collapsibles, dom hacks, date- and timepicker
    * onLoad:
      * initHacks: i.e. drops text after DateFields (hardcoded in django.contib.admin's python code)
      * initCollapsibles: assigns event listeners to collapse handlers. some "special" behavior for collapsibles in header menu (admin\_tools only).
      * initDateTimePicker: adds dom and assigns events to Date- and TimeField
  * `media/admin/js/core.js`
    * from django.contrib.admin. no customizations.
  * `media/admin/js/admin/RelatedObjectLookups.js`
    * empty to prevent 404. see grappelli.RelatedObjectLookups.js.
  * `admin/jsi18n/`
    * from django.contib.admin. no customizations.
  * `media/admin/js/jquery.min.js`
    * empty to prevent 404. grappelli "own" jQuery is all we need.
  * `media/admin/js/jquery.init.js`
    * empty to prevent 404. see grappelli.init.js.
  * `media/admin/js/actions.min.js`
    * empty to prevent 404. see grappelli.change\_list.js.
  * `media/admin/js/urlify.js`
    * from django.contrib.admin. no customizations.
  * `media/admin/js/prepopulate.min.js`
    * empty to prevent 404.
  * `media/admin/tinymce/jscripts/tiny_mce/tiny_mce.js`
    * see tinymce docu
  * `media/admin/tinymce_setup/tinymce_setup.js`
    * basic tinymce setup shipped with grappelli. see tinymce docu for further customizations.
  * `media/admin/js/calendar.js`
    * empty to prevent 404. see ui.widget datepicker.
  * `media/admin/js/admin/DateTimeShortcuts.js`
    * from django.contrib.admin. no customizations.
  * `media/admin/js/grappelli.change_list.js`
    * ui.widget. handles js magic in change\_list (actions, filter, search,...)
    * onReady (call in change\_list.html):
      * assigns events to actions checkboxes, filter dropdown, search field,...
      * makes dom/css manipulations to make grid flexible
  * `media/admin/tinymce/jscripts/tiny_mce/*`
    * all kinds of tiny\_mce language and plugin files are loaded at last (caption obvious: if tiny\_mce field is in the page only.)