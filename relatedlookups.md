# Related Lookups #

When entering a value (ID) for a ForeignKey, the related object is instantly displayed right beside the input-field (after the search-icon).

![http://vonautomatisch.at/media/uploads/grappelli/foreignkey_relatedlookup.jpg](http://vonautomatisch.at/media/uploads/grappelli/foreignkey_relatedlookup.jpg)

This also works for a M2M-field.

![http://vonautomatisch.at/media/uploads/grappelli/m2m_lookup.jpg](http://vonautomatisch.at/media/uploads/grappelli/m2m_lookup.jpg)

## Usage ##

#### model.py ####

```
class GrappelliFields(models.Model):
    gr_test = models.ForeignKey(User, verbose_name=u"Related lookup on users", null=True, blank=True)
    # ...
```

#### admin.py ####

```
class GrappelliFieldsAdmin(GrappelliModelAdmin):
    list_display  = ('__unicode__',)
    raw_id_fields = ('gr_test',)    
    # ...
```