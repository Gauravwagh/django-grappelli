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
    
    'django.contrib.admin',
    ...
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
<blockquote><i>If your ADMIN_MEDIA_PREFIX is /media/admin/ (for example), you need a directory   "admin" within your media-directory. Inside of /admin/, you need all Grappelli media files.</i></blockquote></li></ul>

Note: If you use Djangos integrated development server, start it with<br>
<pre><code>python manage.py runserver mydomain.com:8000 --adminmedia=/path/to/your/admin/media/<br>
</code></pre>