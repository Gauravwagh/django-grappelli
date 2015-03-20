# Introduction #

This application will load unit javascript tests in grappelli.

# Installation #

## settings.py ##

Add "grappellitest" to your settings.py and make it available in your PYTHONPATH:

```

INSTALLED_APPS = (

    'django.contrib.auth',

    'django.contrib.admin',

    'django.contrib.contenttypes',

    'django.contrib.sessions',

    'django.contrib.sites',

    'django.contrib.admindocs',

    'grappelli',

    'grappellitest',

)

```

## urls.py ##

Set the urls:

```

from django.conf.urls.defaults import *

from django.conf import settings

from django.contrib import admin

admin.autodiscover()

urlpatterns = patterns('',

    (r'^grappelli/', include('grappelli.urls')),

    (r'^grappelli/test/', include('grappellitest.urls')),

    (r'^admin/(.*)', admin.site.root),

)

```

## Screenshots ##

By then you should have a new link called "tests" available next to the change password link in the top bar. This link leads to a page like this;

![http://i.imgur.com/CywCD.png](http://i.imgur.com/CywCD.png)

For now the only functional part is the grappelli unit tests:

![http://i.imgur.com/3eqVO.png](http://i.imgur.com/3eqVO.png)