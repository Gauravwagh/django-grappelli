# Multiple Admin Sites #

If you need multiple Admin-Sites, you have to use Grappellis Admin-Site subclass.

```
from grappelli.admin import AdminSite

class MyModelAdmin(admin.ModelAdmin):
...

my_admin_site = AdminSite(title="My Admin Site")
my_admin_site.register(MyModel, MyModelAdmin)
```

You need to change your url-patterns as well (of course):
```
from django.conf.urls.defaults import *
from django.contrib import admin
admin.autodiscover()
from myapp.admin import my_admin_site

urlpatterns = patterns('',

    (r'^admin/doc/', include('django.contrib.admindocs.urls')),
    (r'^admin/filebrowser/', include('filebrowser.urls')),
    (r'^grappelli/', include('grappelli.urls')),
    (r'^admin/', include(admin.site.urls)),
    (r'^my/admin/', include(my_admin_site.urls)),
    ...

```