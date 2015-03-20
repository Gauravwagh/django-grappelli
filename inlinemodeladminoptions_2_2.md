# InlineModelAdmin Options #

With Grappelli, you get some additional attributes for defining your InlineModelAdmin.

## collapse open, collapse closed ##

![http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg](http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg)

There are two options for displaying inline-groups. With **"collapse open"**, the inline-group is collapsible and open by default. With **"collapse closed"**, the inline-group is collapsible but closed by default. Without using a class, the inline-group won´t be collapsible.
```
class NavigationItemInline(admin.StackedInline):
    
    classes = ('collapse open',)
    ...
```


## sortable inlines ##

You can make inlines sortable (drag/drop) using a position field (i.e. PositiveSmallIntegerField) and an additional property with admin.StackedInline or admin.TabularInline.

The field specified in the sortable\_field\_name will be hidden in the change\_form.

```
#model.py

class TabularOne(models.Model):
    ...
    # position field
    position = models.PositiveSmallIntegerField("Position")
    class Meta:
        ordering = ['position']
    ...

#admin.py
class TabularOne(admin.TabularInline):
    ...
    # define the sortable
    sortable_field_name = "position"
    ...
```