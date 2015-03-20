# Release Notes #

### 2.2 (2010-10-04): ###

  * Compatible with Django 1.2.3.
  * Basic support for django-admin-tools.
    * Customizing the Admin Index Page
    * Menu in header (bookmark functionality is back)
  * Changelist:
    * Added CSV-Export Action
    * Added Tooltips (see search)
  * Changeform:
    * Inlines are sortable

### 2.1 (2010-05-20): ###

  * Compatible with Django 1.2.
  * Added grid-based HTML/CSS Framework.
  * Removed all extra-functionality like Bookmarks/Navigation.
  * Customizing the Admin Index Page can be done with Grappelli-Admin-Tools.
  * Changelist:
    * We´ve removed the Sidebar.
    * Filters are collapsible.
    * Actions and the Submit-Row are now fixed at the bottom of the page.
    * Actions are only visible if you select a checkbox.
    * The Submit-Row is only visible if you change/focus a form-element.
    * Actions and list\_editables are deactivated for popups.
    * Pagination is on top and at the bottom of the table.
  * Changeform:
    * The Submit-Row is now fixed at the bottom of the page.

### 2.0 (2009-11-13): ###

  * Compatible with Django 1.1.
  * Refactored Stylesheets (including re-writing lots of stuff).
  * CSS cleanup (decoupled styles from Djangos original stylesheets).
  * Removed all Background-Images (excluding Icons).
  * Removed almost every !important within Stylesheets.
  * Some Template Changes: Most notable within the Changelist, where we´ve decided to move all Search/Filter functions to the Sidebar (because otherwise, with actions and list\_editables activated, it gets a bit confusing).
  * Icon Updates.
  * TinyMCE Skin Update.
  * Updated to work with Django 1.1.
  * Updated Bookmark functionality.
  * Cancel-Button on delete confirmation.
  * Admin Index Page is now customizable.
  * Removed FileBrowser-Templates (they are now part of the FileBrowser).

  * And a lot of smaller changes ...