# PositionField #

"This module provides PositionField, a model field for Django that allows instances of a model to be sorted by a user-specified position. Conceptually, the field works like a list index: when the position of one item is changed, the positions of other items in the collection are updated in response." (from django-positions at google-code).

Take a look at the [Navigation-Model](http://code.google.com/p/django-grappelli/source/browse/trunk/grappelli/models/navigation.py) to get a better idea of how this is supposed to work.

**The original implementation of the Position-Field is done by Joel Watts. For more details, please take a look at** http://github.com/jpwatts/django-positions.