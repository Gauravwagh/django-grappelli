# Related Lookups #

When entering a value (ID) for a ForeignKey, the related object is instantly displayed right beside the input-field (after the search-icon).

![http://vonautomatisch.at/media/uploads/grappelli/foreignkey_relatedlookup.jpg](http://vonautomatisch.at/media/uploads/grappelli/foreignkey_relatedlookup.jpg)

This also works for a M2M-field.

![http://vonautomatisch.at/media/uploads/grappelli/m2m_lookup.jpg](http://vonautomatisch.at/media/uploads/grappelli/m2m_lookup.jpg)

## Usage ##

#### model.py ####

```
class MyModel(models.Model):
    related = models.ForeignKey(RelatedModel, verbose_name=u"Related Lookup", null=True, blank=True)
    # ...
```

#### admin.py ####

```
class MyModelAdmin(admin.ModelAdmin):
    list_display  = ('__unicode__',)
    raw_id_fields = ('related',)    
    # ...
```