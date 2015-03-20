# Visual Generic Relationships #

Making Generic Relations work/look like ForeignKeys: When editing a Generic Relation, you first choose the Content Type and then the Object-ID. With Grappelli, you instantly get the related object displayed right near the Object-ID.

**Note: You have to use names which include "content\_type" and "object\_id" for this to work.**

For example, your Model could look like this:

```
from django.contrib.contenttypes import generic
from django.contrib.contenttypes.models import ContentType
from django.db import models

class ContainerItem(models.Model):
    # ...
    content_type = models.ForeignKey(ContentType, blank=True, null=True, related_name="content_type")
    object_id = models.PositiveIntegerField(blank=True, null=True)
    content_object = generic.GenericForeignKey("content_type", "object_id")
    # ...
    content_type_2 = models.ForeignKey(ContentType, blank=True, null=True, related_name="content_type_2")
    object_id_2 = models.PositiveIntegerField(blank=True, null=True)
    content_object_2 = generic.GenericForeignKey("content_type_2", "object_id_2")
```

![http://vonautomatisch.at/media/uploads/grappelli/generic_relation.jpg](http://vonautomatisch.at/media/uploads/grappelli/generic_relation.jpg)

**Thanks to Weston Nielson (http://code.google.com/p/django-genericadmin/) for his inspiration**.