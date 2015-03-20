This page is a preliminary documentation on Version 2.0 of Grappelli. The behaviour can slightly change within the next couple of weeks.<br>
<b>Feedback is very much appreciated.</b>
<br><br>
<hr />
<br>
<h1>Django Issues</h1>
There´s a whole lot of unresolved Django Issues concerning the Admin-Interface. I´ve listed just a couple of issues <a href='djangoissues.md'>here</a>. E.g., don´t blame us if you don´t see a Unicode representation near an M2M raw-id-field.<br>
<br><br>
<hr />
<br>
<h1>Release Notes</h1>
Here´s a list with the most important changes:<br>
<ul><li>Refactored Stylesheets (including re-writing lots of stuff).<br>
</li><li>CSS cleanup (decoupled styles from Djangos original stylesheets).<br>
</li><li>Removed all Background-Images (excluding Icons). Note: With using Safari, you still have the option of Gradients.<br>
</li><li>Removed almost every !important within Stylesheets.<br>
</li><li>Some Template Changes: Most notable within the Changelist, where we´ve decided to move all Search/Filter functions to the Sidebar (because of actions and list_editables).<br>
</li><li>Icon Updates.<br>
</li><li>TinyMCE Skin Update.<br>
</li><li>Updated to work with Django 1.1.<br>
</li><li>Removed the need for additional context-processors.<br>
</li><li>Updated Bookmark functionality.<br>
</li><li>Cancel-Button on delete confirmation.</li></ul>

Still TODO:<br>
<ul><li>Take a look at the Issues.<br>
<br>
<hr />
<br>
<h1>Requirements</h1>
</li><li>Django 1.1<br>
<br>
<hr />
<br>
<h1>Installation</h1></li></ul>

<ol><li><b>Download Grappelli</b>
<blockquote>Install Grappelli anywhere on your python-path.<br>
<pre><code>svn checkout http://django-grappelli.googlecode.com/svn/branches/grappelli_2 grappelli<br>
</code></pre>
</blockquote></li><li><b>Add Grappelli to your INSTALLED APPS</b>
<blockquote>Open your projects settings-file (settings.py) and add Grappelli to your INSTALLED APPS.<br>
<pre><code>INSTALLED_APPS = (<br>
    ...<br>
    'grappelli',<br>
)<br>
</code></pre>
</blockquote></li><li><b>Change urls.py</b>
<blockquote>Add Grappelli to your url-definitions.<br>
<pre><code>(r'^grappelli/', include('grappelli.urls')),<br>
</code></pre>
</blockquote></li><li><b>Change grappelli/settings.py</b>
<blockquote>Take a look at the available grappelli-settings and change them (if necessary).<br>
</blockquote></li><li><b>Sync your Database</b>
<blockquote>Run the Django 'syncdb' command to create the appropriate tables.<br>
<pre><code>python manage.py syncdb<br>
</code></pre>
<i>This will create the tables for Bookmarks, Help & Navigation.</i>
</blockquote></li><li><b>Optional: Load Fixtures</b>
<blockquote>It´s recommended to load some initial data.<br>
<pre><code>python manage.py loaddata grappelli_navigation.json --settings=settings<br>
python manage.py loaddata grappelli_help.json --settings=settings<br>
</code></pre>
<i>Note that the Admin-Links within the Fixtures begin with /admin/ ... if your Admin-Interface is accessible via a different URL, you have to change this (either change the json-files before loading or change the URLs afterwards).</i>
</blockquote></li><li><b>Symlink/Copy media</b>
<blockquote>Copy the Contents of folder /media/ to your media-directory. Alternatively, you might want to use a symlink.<br>
<pre><code>cp -R /path/to/grappelli/media /path/to/your/media admin<br>
</code></pre>
<i>Note: If possible, avoid using /django/contrib/admin/media/ as your media directory (since it will break future django-updates).</i><br>
<i>If your ADMIN_MEDIA_PREFIX is /media/admin/ (for example), you need a directory   "admin" within your media-directory. Inside of /admin/, you need all Grappelli.</i>
</blockquote></li><li><b>Copy Admin-Templates</b>
<blockquote>Copy the folder /templates/admin to your template-directory.<br>
<pre><code>cp -R /path/to/grappelli/templates/admin /path/to/your/templates admin<br>
</code></pre>
In order to overwrite the original admin-templates you need to make sure that your TEMPLATE_LOADERS are looking at the Filesystem first:<br>
<pre><code>TEMPLATE_LOADERS = (<br>
    'django.template.loaders.filesystem.load_template_source',<br>
    'django.template.loaders.app_directories.load_template_source',<br>
)<br>
</code></pre>
<i>This step is necessary in order to overwrite Djangos Admin-Templates.</i>
<br>
<hr />
<br>
<h1>Setup & Functionality</h1></blockquote></li></ol>

Please take a look at the other Wiki-Pages. What´s described there should still be valid.