# Installation #

Before Installing Grappelli, please take a look at the known [Django Issues](djangoissues.md).

  1. **Download Grappelli**
> > Install Grappelli anywhere on your python-path.
```
svn checkout http://django-grappelli.googlecode.com/svn/trunk/grappelli/ grappelli
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
  1. **Add context-processors**
> > Open your projects settings-file. For Grappelli, you need the _request context processor_. The _authentication context processor_ is needed for the admin-interface anyway. The grappelli.context\_processors.admin\_template\_path is required to check if you use admin\_tools or not (and render the necessary templates).
```
TEMPLATE_CONTEXT_PROCESSORS = (
    "django.core.context_processors.auth",
    "django.core.context_processors.request",
    ...
    "grappelli.context_processors.admin_template_path",
)
```
  1. **Change urls.py**
> > Add Grappelli to your url-definitions.
```
(r'^grappelli/', include('grappelli.urls')),
```
  1. **Change grappelli/settings.py**
> > Take a look at the available grappelli-settings and change them (if needed).
  1. **Copy/Symlink media**
> > Copy the folder /media/ to your admin media-directory. Alternatively, you might want to use a symlink.
```
cp -R /path/to/grappelli/media /path/to/your/admin/media
```
> > _Note: If possible, avoid using /django/contrib/admin/media/ as your media directory (since it will break future django-updates)._<br>
<blockquote><i>If your ADMIN_MEDIA_PREFIX is /media/admin/ (for example), you need a directory   "admin" within your media-directory. Inside of /admin/, you need all Grappelli media files.</i>
</blockquote><ol><li><b>admin_tools (BETA)</b>
<blockquote>if you use admin_tools please check the documentation and make sure your admin_tools setup works without grappelli (if it doesn't work with grappelli). we are currently at the beginning of skinning admin_tools. so there are some features of admin_tools not supported yet, if you use it with grappelli. For further information check <a href='GrappelliAdminToolsSetup.md'>grappelli+admin_tools setup</a></blockquote></li></ol>

Note: If you use Djangos integrated development server, start it with<br>
<pre><code>python manage.py runserver mydomain.com:8000 --adminmedia=/path/to/your/admin/media/<br>
</code></pre>