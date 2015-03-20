**NOTE: This document is for grappelli's development version, which can be significantly different from previous releases.**

# Changelog #

  * Improved support for [django-admin-tools](http://bitbucket.org/izi/django-admin-tools/wiki/Home):
    * menu: major js improvements for bookmarks, new template for custommenu command
    * dashboard: major js/css improvements, added support for module Group accordion and tabs, added support for module draggable and deletable, save state of dashboard in dashboard\_preferences, new template vor customdashboard command
  * JavaScript refactoring:
    * Faster load of DOM and js magic
    * loads (mostly) all js code from grappelli.js
  * minor fix for sortable inlines
# Requirements #


  * [django](http://www.djangoproject.com/)
  * Optional:
    * [django-admin-tools](http://bitbucket.org/izi/django-admin-tools/wiki/Home)
    * [django-filebrowser](http://code.google.com/p/django-filebrowser/)
    * [django-medman](http://code.google.com/p/django-medman/)

**NOTE: grappelli DEV works with the newest release and/or repository checkout of these projects.**

# Installation #

Before Installing Grappelli, please take a look at the known [Django Issues](djangoissues.md).

  1. **Download Grappelli**
> > Install Grappelli anywhere on your python-path.
> > via svn:
```
svn checkout http://django-grappelli.googlecode.com/svn/trunk/grappelli
```
  1. **Add Grappelli to your INSTALLED APPS**
> > Open your projects settings-file (settings.py) and add Grappelli to your INSTALLED APPS **before django.contrib.admin**.
```
INSTALLED_APPS = (
    ...
    'grappelli',
    
    # if you use admin_tools
    'admin_tools.theming',
    'admin_tools.menu',
    'admin_tools.dashboard',
    
    'django.contrib.admin',
    ...
)
```
  1. **Add TEMPLATE\_CONTEXT\_PROCESSORS**
> > Add missing processors:
```
TEMPLATE_CONTEXT_PROCESSORS = (
    # required by django.contrib.admin anyway
    "django.core.context_processors.auth",
    # required by grappelli
    "django.core.context_processors.request",
    ...
    # required to render correct templates (grappelli+admin-tools or grappelli "standalone")
    "grappelli.context_processors.admin_template_path",
)
```
  1. **Add grappelli urls to urls.py**
> > Add Grappelli to your url-definitions.
```
(r'^grappelli/', include('grappelli.urls')),
```
  1. **Copy/Symlink media**
> > Copy the folder /media/ to your admin media-directory. Alternatively, you might want to use a symlink.
```
cp -R /path/to/grappelli/media /path/to/your/admin/media
```
> > _Note: If possible, avoid using /django/contrib/admin/media/ as your media directory (since it will break future django-updates)._<br>
<blockquote><i>If your ADMIN_MEDIA_PREFIX is /media/admin/ (for example), you need a directory "admin" within your media-directory. Inside of /admin/, you need all Grappelli media files.</i>
</blockquote><ol><li><b>start django server with additional parameters</b>
<pre><code>python manage.py runserver localhost:8000 --adminmedia=/path/to/your/admin/media/<br>
</code></pre></li></ol>

<h1>Grappelli Settings</h1>

All Settings can be defined in your projects settings-file (<code>settings.py</code>).<br>
<br>
All grappelli settings use the prefix "<code>GRAPPELLI_</code>" (e.g. <code>GRAPPELLI_ADMIN_TITLE</code> instead of <code>ADMIN_TITLE</code>).<br>
<br>
<h2>Available Settings</h2>

<table><thead><th> <b>Name</b> </th><th> <b>Description</b> </th></thead><tbody>
<tr><td> <code>GRAPPELLI_ADMIN_TITLE</code> </td><td> The Site Title of your Admin-Interface. Change this instead of changing index.html </td></tr>
<tr><td> <code>GRAPPELLI_ADMIN_URL</code> </td><td> The URL to your <b>Main Admin Site</b>. Necessary in order to get the right URLs for related lookups registered to different admin site objects. </td></tr></tbody></table>

<h2>Usage example</h2>

<pre><code><br>
GRAPPELLI_ADMIN_TITLE = 'My Application'<br>
<br>
</code></pre>

Grappelli is used to ensure any settings found in the main <code>settings.py</code> file take precedence over the Grappelli's settings file and provide a default value if none is found.<br>
<br>
<br>
<h1>Visual Generic Relations</h1>

In order to use <b>Visual Generic Relations</b>, you have to use the names <i>content_type</i> and <i>object_id</i> for defining generic relations.<br>
<br>
Making Generic Relations work/look like ForeignKeys: When editing a Generic Relation, you first choose the Content Type and then the Object-ID. With Grappelli, you instantly get the related object displayed right near the Object-ID.<br>
<br>
<b>Note: You have to use names which include "content_type" and "object_id" for this to work.</b>

For example, your Model could look like this:<br>
<br>
<pre><code>from django.contrib.contenttypes import generic<br>
from django.contrib.contenttypes.models import ContentType<br>
from django.db import models<br>
<br>
class ContainerItem(models.Model):<br>
    # ...<br>
    content_type = models.ForeignKey(ContentType, blank=True, null=True, related_name="content_type")<br>
    object_id = models.PositiveIntegerField(blank=True, null=True)<br>
    content_object = generic.GenericForeignKey("content_type", "object_id")<br>
    # ...<br>
    content_type_2 = models.ForeignKey(ContentType, blank=True, null=True, related_name="content_type_2")<br>
    object_id_2 = models.PositiveIntegerField(blank=True, null=True)<br>
    content_object_2 = generic.GenericForeignKey("content_type_2", "object_id_2")<br>
</code></pre>

<img src='http://vonautomatisch.at/media/uploads/grappelli/generic_relation.jpg' />

<b>Thanks to Weston Nielson (<a href='http://code.google.com/p/django-genericadmin/'>http://code.google.com/p/django-genericadmin/</a>) for his inspiration</b>.<br>
<br>
<h1>ModelAdmin Options</h1>

With Grappelli, you get some additional attributes for defining your ModelAdmin.<br>
<br>
<h2>Related Lookups</h2>

When entering a value (ID) for a ForeignKey, the related object is instantly displayed right beside the input-field (after the search-icon).<br>
<br>
<img src='http://vonautomatisch.at/media/uploads/grappelli/foreignkey_relatedlookup.jpg' />

This also works for a M2M-field.<br>
<br>
<img src='http://vonautomatisch.at/media/uploads/grappelli/m2m_lookup.jpg' />

<h3>Usage</h3>

<h4>model.py</h4>

<pre><code>class MyModel(models.Model):<br>
    related = models.ForeignKey(RelatedModel, verbose_name=u"Related Lookup", null=True, blank=True)<br>
    # ...<br>
</code></pre>

<h4>admin.py</h4>

<pre><code>class MyModelAdmin(admin.ModelAdmin):<br>
    list_display  = ('__unicode__',)<br>
    raw_id_fields = ('related',)    <br>
    # ...<br>
</code></pre>

<h2>collapse open/closed</h2>

<img src='http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields.jpg' />

There are two classes for displaying fieldsets in the Admin-Interface. With <b>"collapse open"</b>, the headline of the fieldset is collapsible and open by default. With <b>"collapse closed"</b>, the headline of the fieldset is collapsible but closed by default. Without using a class, the fieldset won´t be collapsible.<br>
<pre><code>class EntryOptions(admin.ModelAdmin):<br>
    ...<br>
    fieldsets = (<br>
        ('', {<br>
            'fields': ('title', 'subtitle', 'slug', 'pub_date', 'status',),<br>
        }),<br>
        ('Flags', {<br>
            'classes': ('collapse closed',),<br>
            'fields' : ('flag_front', 'flag_sticky', 'flag_allow_comments', 'flag_comments_closed',),<br>
        }),<br>
        ('Tags', {<br>
            'classes': ('collapse closed',),<br>
            'fields' : ('tags',),<br>
        }),<br>
        ('Image', {<br>
            'fields' : ('image',),<br>
        }),<br>
        ('Content', {<br>
            'classes': ('collapse open',),<br>
            'fields' : ('summary', 'body',),<br>
        }),<br>
        ('Author', {<br>
            'classes': ('collapse closed',),<br>
            'fields' : ('author',),<br>
        }),<br>
    )<br>
    class Media:<br>
        ...<br>
</code></pre>

<h2>search_fields_verbose</h2>

In order to actually <i><b>see</b></i> what you´re searching for within a Change-List, you can define <b>search_fields_verbose</b>.<br>
<pre><code>class EntryOptions(admin.ModelAdmin):<br>
    ...<br>
    search_fields = ['id', 'title', 'subtitle', 'pub_date']<br>
    search_fields_verbose = ['ID', 'Title', 'Subtitle', 'Publication Date']<br>
    ...<br>
</code></pre>

<h2>actions</h2>

<h3>csv_export_selected</h3>

Export change_list as csv.<br>
<br>
<pre><code>from grappelli.actions import csv_export_selected<br>
...<br>
class EntryOptions(admin.ModelAdmin):<br>
    ...<br>
    actions = [csv_export_selected]<br>
    ...<br>
</code></pre>

<h1>InlineModelAdmin Options</h1>

<h2>collapse open/closed</h2>

<img src='http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg' />

There are two options for displaying inline-groups. With <b>"collapse open"</b>, the inline-group is collapsible and open by default. With <b>"collapse closed"</b>, the inline-group is collapsible but closed by default. Without using a class, the inline-group won´t be collapsible.<br>
<pre><code>class NavigationItemInline(admin.StackedInline):<br>
    <br>
    classes = ('collapse open',)<br>
    ...<br>
</code></pre>


<h2>sortable inlines</h2>

You can make inlines sortable (drag/drop) using a position field (i.e. PositiveSmallIntegerField) and an additional property with admin.StackedInline or admin.TabularInline.<br>
<br>
The field specified in the sortable_field_name will be hidden in the change_form.<br>
<br>
<pre><code>#model.py<br>
<br>
class TabularOne(models.Model):<br>
    ...<br>
    # position field<br>
    position = models.PositiveSmallIntegerField("Position")<br>
    class Meta:<br>
        ordering = ['position']<br>
    ...<br>
<br>
#admin.py<br>
class TabularOne(admin.TabularInline):<br>
    ...<br>
    # define the sortable<br>
    sortable_field_name = "position"<br>
    ...<br>
</code></pre>

<h1>Using TinyMCE</h1>

<ol><li><b>Copy and Change tinymce_setup.js</b>
<blockquote>Copy tinymce_setup.js (in order to not break future updates) and adjust the setup/behaviour of TinyMCE according to your needs - see <a href='http://wiki.moxiecode.com/index.php/TinyMCE:Configuration'>http://wiki.moxiecode.com/index.php/TinyMCE:Configuration</a>
</blockquote></li><li><b>Change the media-definition of your ModelAdmin</b>
<pre><code>    class Media:<br>
        js = ['/media/admin/tinymce/jscripts/tiny_mce/tiny_mce.js', '/path/to/your/tinymce_setup.js',]<br>
</code></pre>
</li><li><b>Check the file tinymce_setup.js and change it (if you need to).</b></li></ol>

<img src='http://vonautomatisch.at/media/uploads/grappelli/tinymce.jpg' />

<h1>Multiple Admin Sites</h1>

<b>Note: deprecated docu! this part need a rework.</b>

If you need multiple Admin-Sites, you have to use Grappellis Admin-Site subclass.<br>
<br>
<pre><code>from grappelli.admin import AdminSite<br>
<br>
class MyModelAdmin(admin.ModelAdmin):<br>
...<br>
<br>
my_admin_site = AdminSite(title="My Admin Site")<br>
my_admin_site.register(MyModel, MyModelAdmin)<br>
</code></pre>

You need to change your url-patterns as well (of course):<br>
<pre><code>from django.conf.urls.defaults import *<br>
from django.contrib import admin<br>
admin.autodiscover()<br>
from myapp.admin import my_admin_site<br>
<br>
urlpatterns = patterns('',<br>
<br>
    (r'^admin/doc/', include('django.contrib.admindocs.urls')),<br>
    (r'^admin/filebrowser/', include('filebrowser.urls')),<br>
    (r'^grappelli/', include('grappelli.urls')),<br>
    (r'^admin/', include(admin.site.urls)),<br>
    (r'^my/admin/', include(my_admin_site.urls)),<br>
    ...<br>
<br>
</code></pre>

<h1>grappelli + admin-tools</h1>

Grappelli is not only a skin for django.contrib.admin. It is a skin for django-admin-tools too. Thus grappelli has it's old bookmarks feature back. Additionally you can customize the order and hierarchy of the admin index and app_index, add modules like <i>Recent Actions</i>, <i>Link List</i>, and some more very nice features from admin-tools.<br>
<br>
Basically it works like described in the  <a href='http://packages.python.org/django-admin-tools/0.3.0/index.html'>django-admin-tools docu</a> but some things are different because of the different UI.<br>
<br>
<h2>DashboardModule.css_classes</h2>

<b>Required</b>
<ul><li><i>column_1</i>, <i>column_2</i> or <i>column_3</i>: defines in which column the module is rendered. Without one of those the module isn't rendered at all.</li></ul>

<b>Optional</b>
<ul><li><i>open</i>/<i>closed</i>: modules are <i>open</i> by default. you can set <i>closed</i> to render the module closed.</li></ul>

<pre><code>#poject's/dashboard.py<br>
class CustomIndexDashboard(Dashboard):<br>
    <br>
    def __init__(self, **kwargs):<br>
        Dashboard.__init__(self, **kwargs)<br>
        <br>
        self.children.append(modules.LinkList(<br>
            title=_('Media Management'),<br>
            css_classes=['column_1'],<br>
            children=[<br>
                {<br>
                    'title': _('Django FileBrowser'),<br>
                    'url': '/admin/filebrowser/browse/',<br>
                    'external': False,<br>
                    'description': 'Python programming language rocks !',<br>
                },<br>
            ]<br>
        ))<br>
        <br>
        self.children.append(modules.AppList(<br>
            title=_('User...'),<br>
            models=('django.contrib.auth.models.User',),<br>
            css_classes=['column_1', 'open'],<br>
        ))<br>
        <br>
        self.children.append(modules.AppList(<br>
            title=_('Administration'),<br>
            include_list=('django.contrib',),<br>
            css_classes=['column_1', 'closed'],<br>
        ))<br>
        <br>
        self.children.append(modules.AppList(<br>
            title=_('Administration'),<br>
            exclude_list=('django.contrib',),<br>
            css_classes=['column_1', 'closed'],<br>
        ))<br>
        ...<br>
</code></pre>