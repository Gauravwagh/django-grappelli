# Extending Templates #

When using your own templates for certain areas of the Admin-Interface you might want to extend base.html.
For better readability, we decided to split the inclusion of stylesheets and javascripts into different blocks.

For stylesheets there is:
  * **block stylesheets**
  * and **block extrastyle**

For javascripst there is:
  * **block javascripts**
  * and **block extrahead**

If you need to **overwrite** the stylesheets or javascripts, use block stylesheets/javascripts. If you need to **extend** the given styles/js, use the blocks extrastyle/extrahead.

Note: You can (of course) still use block stylesheet with {{ block.super }} to extend the styles. We have just decided for the given structure because of better readability in the templates.

The inclusion of {{ media }} has been moved to a seperate block called "media".