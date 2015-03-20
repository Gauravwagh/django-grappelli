# Customizing Index Page #

With Grappelli, you have the possiblity to change the admin index page. Instead of listing apps acccording to INSTALLED\_APPS, you´re able to group apps and list them in the most meaningful way. Moreover, you can display subsections of your admin index page with either using groups or collections.

Let´s say you´re using Djangos built-in Authentication and you´re extending the User-Model. You´re using django-registration as well. Now, we´re going to group all these apps:
```
from grappelli.sites import GrappelliSite

from django.contrib.auth.models import User, Group
from django.contrib.auth.admin import GroupAdmin, UserAdmin

from www.user.models import UserProfile, UserExtendedProfile
from www.user.admin import UserExtendedProfileOptions, UserProfileOptions

from www.registration.models import RegistrationProfile
from www.registration.admin import RegistrationProfileOptions

user_site = GrappelliSite()
user_site.register(UserExtendedProfile, UserExtendedProfileOptions)
user_site.register(UserProfile, UserProfileOptions)
user_site.register(Group, GroupAdmin)
user_site.register(User, UserAdmin)

user_site.groups = {
    0: {
        'title': 'User Management Administration', # optional
        'name': 'User Management',
        'apps': ['auth', 'user'],
        'template': 'custom/index_group_usermanagement.html', # optional
        'classes': ['collapse-open'], # optional
        'show_apps': True, # optional
    },
    1: {
        'name': 'Registration',
        'apps': ['registration']
    }
}

user_site.collections = {
    0: {
        'title': 'User Admin',
        'groups': [0,1]
    },
}
```

When using admin.autodiscover() you can define a GrappelliSite like this:
```
from django.contrib import admin
from grappelli.sites import GrappelliSite
admin.site = GrappelliSite()
admin.autodiscover()

admin.site.groups = {
    0: {
        'title': 'User Management Administration', # optional
        'name': 'User Management',
        'apps': ['auth', 'user'],
        'template': 'custom/index_group_usermanagement.html', # optional
        'classes': ['collapse-open'], # optional
        'show_apps': True, # optional
    },
    1: {
        'name': 'Registration',
        'apps': ['registration']
    }
}


admin.site.collections = {
    0: {
        'title': 'User Admin',
        'groups': [0,1]
    },
}
```

Of course, you still have to setup the urls for this admin-site. If you use a file admin.py within your project to define the admin-sites, you´ll do something like this:
```
from myproject.admin import admin, user_site

urlpatterns = patterns('',
    ...
    (r'^admin/', include(admin.site.urls)),
    (r'^user_admin/', include(user_site.urls)),
```

Please Note that you can use GrappelliSite without defining Groups. The apps registered with this site will be listed in the usual way. When you define Groups and you also have apps which are not part of any group, these apps will be shown at the bottom of the page.

The admin index-page then looks something like this (note that the screenshot below is a more complex example ...):

![http://vonautomatisch.at/media/uploads/grappelli/group.jpg](http://vonautomatisch.at/media/uploads/grappelli/group.jpg)

## Changing the order of Models within your Apps ##

With the Django Admin-Interface, the Models within Apps are ordered by Name - which is not necessarily the most logical order. To reorder the Models, you can use an attribute order within ModelAdmin.

```
class NavigationOptions(admin.ModelAdmin):
    
    # List Options
    list_display = ('order', 'title',)
    ...
    
    # Grappelli Options
    order = 0

class BookmarkOptions(admin.ModelAdmin):
    
    # List Options
    list_display = ('user',)
    ...
    
    # Grappelli Options
    order = 1

```
Now, the Model "Navigation" will be listed as first with "Bookmarks" below.

## Links to Groups and Collections ##

If you want your Editors to view subsections of the admin index page, you can display links to Groups and/or Collections using Grappellis built-in Navigation-Sidebar. E.g., a link to the Collection defined with key "0" is something like "/admin/?c=0".

When having lots of apps/models, it might be useful to define a couple of Collection in order to break down the admin index page into smaller sections. Referring to the above Screenshot, everything which is listed under "Inhalte" in the Navigation-Sidebar is basically a Collection.

## Renaming Apps ##

It´s currently not possible to rename apps with GrappelliSite, because the app-name is used within the breadcrumbs (and changing the breadcrumbs is not possible with subclassing AdminSite).

## Where do I put all this? ##

Well, that´s up to you. You can - for example - use a file admin.py within your project. Just make sure that within urls.py, you import admin from your admin-file.

Instead of
```
from django.contrib import admin
```
you then write (if you´re using just one admin-site)
```
from myproject.admin import admin
```
or (if you´re using several different admin-sites)
```
from myproject.admin import admin, user_site
```

For smaller projects with just a couple of apps and one admin-site, you can also use urls.py to define your admin-stuff.