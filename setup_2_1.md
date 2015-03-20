# Setup #

For using Grappelli, you have to follow some rules when it comes to your projects setup.

## Registering Models ##

**Update (2010-08-03): Starting with rev 1093, this is no longer necessary.**

_Note: This is only relevant if you use different Admin Site Objects._

Grappelli assumes, that _every_ Model is registered with your **Main Admin Site**. This is necessary, because with the Original Django Admin-Interface, the Links for Related Lookups are _relative_. This means that you have to register _every_ Related Model within _every_ Admin Site Object (which is senseless, from my point of view). In order to avoid rewriting/customizing dozens of templates, we changed the Links for the Related Lookups to point to your Main Admin Site.

So, what actually _is_ your **Main Admin Site**? It´s the Admin Site Object where all your Models are registered, usually done with _admin.autodiscover()_. It´s important that you change **ADMIN\_URL** within the Grappelli setttings accordingly.

## Defining Generic Relations ##

In order to use **Visual Generic Relationships**, you have to use the names _content\_type_ and _object\_id_ for defining generic relations, see [Generic Relationships](http://code.google.com/p/django-grappelli/wiki/generic) for more on this issue.