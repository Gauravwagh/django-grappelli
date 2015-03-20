# InlineModelAdmin Options #

With Grappelli, you get some additional attributes for defining your InlineModelAdmin.

## collapse open, collapse closed ##

![http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg](http://vonautomatisch.at/media/uploads/grappelli/collapsed_fields_inline.jpg)

You have two options for displaying inline-groups. With **"collapse open"**, the inline-group is collapsible and open by default. With **"collapse closed"**, the inline-group is collapsible but closed by default. Without using a class, the inline-group won´t be collapsible.
```
class NavigationItemInline(admin.StackedInline):
    
    classes = ('collapse open',)
    ...
```


## sortable inlines ##

You can make inlines sortable. All you need some kind of position field (i.e. PositiveSmallIntegerField) in the model and an additional property in the admin.StackedInline or admin.TabularInline of the model.

The field specified in the sortable\_field\_name will be hidden in the change\_form. You can edit the order of the inlines via drag&drop of the symbol left to the delete button of the inline (screenshot will follow).

```
#model.py

class TabularOne(models.Model):
    ...
    position = models.PositiveSmallIntegerField("Position")
    class Meta:
        ordering = ['position']
    ...

#admin.py
class TabularOne(admin.TabularInline):
    ...
    # this is what grappelli needs to know it's a sortable inline
    sortable_field_name = "position"
    ...
```