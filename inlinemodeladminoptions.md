# InlineModelAdmin Options #

With Grappelli, you get some additional attributes for defining your InlineModelAdmin.

## collapse-open, collapse-closed ##

![http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg](http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg)

You have two options for displaying inline-groups. With **"collapse-open"**, the inline-group is collapsible and open by default. With **"collapse-closed"**, the inline-group is collapsible but closed by default. Without using a class, the inline-group won´t be collapsible.
```
class NavigationItemInline(admin.StackedInline):
    
    classes = ('collapse-open',)
    ...
```

## allow\_add ##

With using _allow\_add_, you´ll get the "+"-Button for Inlines.
```
class NavigationItemInline(admin.StackedInline):
    
    classes = ('collapse-open',)
    allow_add = True
    ...
```