# ModelAdmin Options #

With Grappelli, you get some additional attributes for defining your ModelAdmin.

## collapse open, collapse closed ##

![http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields.jpg](http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields.jpg)

There are two new classes for displaying fieldsets in the Admin-Interface. With **"collapse open"**, the headline of the fieldset is collapsible and open by default. With **"collapse closed"**, the headline of the fieldset is collapsible but closed by default. Without using a class, the fieldset won´t be collapsible.
```
class EntryOptions(admin.ModelAdmin):
    ...
    fieldsets = (
        ('', {
            'fields': ('title', 'subtitle', 'slug', 'pub_date', 'status',),
        }),
        ('Flags', {
            'classes': ('collapse closed',),
            'fields' : ('flag_front', 'flag_sticky', 'flag_allow_comments', 'flag_comments_closed',),
        }),
        ('Tags', {
            'classes': ('collapse closed',),
            'fields' : ('tags',),
        }),
        ('Image', {
            'fields' : ('image',),
        }),
        ('Content', {
            'classes': ('collapse open',),
            'fields' : ('summary', 'body',),
        }),
        ('Author', {
            'classes': ('collapse closed',),
            'fields' : ('author',),
        }),
    )
    class Media:
        ...
```

## search\_fields\_verbose ##

In order to actually _**see**_ what you´re searching for within a Change-List, you can define **search\_fields\_verbose**.
```
class EntryOptions(admin.ModelAdmin):
    ...
    search_fields = ['id', 'title', 'subtitle', 'pub_date']
    search_fields_verbose = ['ID', 'Title', 'Subtitle', 'Publication Date']
    ...
```


## actions ##

### csv\_export\_selected ###

Export change\_list as csv.

```
from grappelli.actions import csv_export_selected
...
class EntryOptions(admin.ModelAdmin):
    ...
    actions = [csv_export_selected]
    ...
```