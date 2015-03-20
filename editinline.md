# Reordering Edit-Inlines #

## Note: This is currently not working due to a django-bug. ##

With using Grappelli, you get the option to (re)order edit-lines (Stacked & Tabular) using Drag & Drop. Moreover, the reordering is preserved in the case of errors.

**This is achieved with pure javascript (JQuery) - since Django doesn´t support re-ordering inlines, this is currently the only possiblity.**

Please Note that the order-field must not have a **default-attribute**, because it prevents the reordering.
Take a look at the [Navigation-Model](http://code.google.com/p/django-grappelli/source/browse/trunk/models/navigation.py) to get a better idea of how this is supposed to work.

### Add an Order-Field to your inline-related Model ###

It´s currently necessary to name that field "order". Moreover, you must not use a "verbose name" for that field.

```
class PhotoGallery(models.Model):
    ...

class PhotoGalleryItem(models.Model):
    photogallery = models.ForeignKey(PhotoGallery)
    ...
    order = models.PositiveIntegerField()
    ...
    class Meta:
        ordering = ['order']
```

### Add the sortable-attribute to your Inline-Formset ###
```
class PhotoGalleryInline(admin.StackedInline):
    model = PhotoGalleryItem
    extra = 1
    sortable = True

class PhotoGalleryOptions(admin.ModelAdmin):
    ...
    inlines = [PhotoGalleryInline]

admin.site.register(PhotoGallery, PhotoGalleryOptions)
```