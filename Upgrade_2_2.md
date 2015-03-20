# Upgrade from grappelli 2.1 #

  1. **Update Grappelli**
```
# if you use grappelli/trunk
svn up

# if you want to use grappelli/trunk (checkout on python-path)
svn checkout http://django-grappelli.googlecode.com/svn/trunk/grappelli/ grappelli

# if you want to use the release tag
svn checkout http://django-grappelli.googlecode.com/svn/tags/releases/2.2/grappelli/ grappelli
```
  1. **Add context-processors**
> > Open your projects settings-file. For Grappelli, you need the _request context processor_. The _authentication context processor_ is needed for the admin-interface anyway. The grappelli.context\_processors.admin\_template\_path is required to check if you use admin\_tools or not (and renders the necessary templates).
```
TEMPLATE_CONTEXT_PROCESSORS = (
    "django.core.context_processors.auth",
    "django.core.context_processors.request",
    ...
    "grappelli.context_processors.admin_template_path",
)
```
  1. **(optional) Add django-admin-tools**
> > Open your projects settings-file (settings.py) and add admin-tools. Keep Grappelli on top, and django.contrib.admin on the bottom.
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
> > Follow the installation [documentation of django-admin-tools](http://packages.python.org/django-admin-tools/0.3.0/quickstart.html#installing-django-admin-tools)