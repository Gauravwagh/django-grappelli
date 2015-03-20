#README/INSTALL/FAQ... for grappelli standalone aka. grappelli 3

# Introduction #

grappelli 3 is a new approach. it's a _"standalone"_ app. means there is no django.contrib.admin necessary.

initial goals:
  * get rid of register(): no more AdminModels and no need to register models.
  * editable admin start page and admin lists and forms
  * complete JavaScript refactoring using exclusively unobtrusive jQuery & jQuery UI
  * complete DOM rewrite (using a CSS grid and semantically sane HTML)

# INSTALL #

**settings.py**
```

#from django.contrib import admin
from grappelli import admin

admin.autodiscover()

urlpatterns = patterns('',
    (r'^admin/', include(admin.site.urls)),
    (r'^grappelli/', include('grappelli.custom.urls')),
)


```

# Included features #

| **Feature** | **Description** |
|:------------|:----------------|
| Autocomplete | Autocomplete field |
| AutoSlugField | Automatically generate slug field from a target input |
| Collapsibles | Enhanced Collapsibles |
| Custom Index | Customizable Admin Index Page |
| Filebrowser | Integration with Django [Filebrowser](http://code.google.com/p/django-filebrowser/) |
| Inline Model Admin |  |
| Help/Documentation for Editors. |  |
| PositionField |  |
| Related Lookups |  |
| RTE (TinyMCE) | Rich Text Editor |
| M2M Autocomplete | ManyToMany Autocomplete field (like facelist) |
| Side Navigation | Additional Navigation Area on the Index-Site |
| Visual Generic Relationships |  |



