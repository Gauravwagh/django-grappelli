# Django Issues #

There are some known problems with the Django admin-interface. I´m going to list them here in order to avoid confusion (because the problems are not related to Grappelli whatsoever). See also: http://code.djangoproject.com/wiki/DjangoDesign<br>
<b>Most of these Issues are around for quite a while and they are unlikely to be solved.</b>

If you think there´s something missing here (or if an Issue has been resolved), please drop me an email.<br>
<br>
<h2>Reordering Edit-Inlines</h2>
<b>UPDATE: We´ve integrated a pure js-based-solution in order to drag/drop inlines with Grappelli 2.2 and newer.</b>

Because in case of errors, formsets are not returned in the right order, reordering inlines is currently not possible.<br>
<i>(Solution seems to be coming ... somewhere.)</i>

see <a href='http://code.djangoproject.com/ticket/14238'>http://code.djangoproject.com/ticket/14238</a>

<h2>Translating App Names</h2>

It´s not possible to translate the names of apps within the admin-interface which leads to a strange language mix (esp. on the index page).<br>
<i>(There´s already a ticket but IMHO it does not solve the problem.)</i>

Update (2010-09): Currently, this doesn´t work at all (even with using locales).<br>
see <a href='http://code.djangoproject.com/ticket/3591'>http://code.djangoproject.com/ticket/3591</a>

<h2>The Admin Index Site</h2>

Currently, the admin index site reflects the structure of your applications/models. We don´t think editors (who use the admin site) are interested in the structure of your project/applications. What they want is the most reasonable list of models, divided into different sections (not necessarily apps).<br>
<i>(Solved with Grappelli-Admin-Tools ... but still looking for a better way to handle this issue.)</i>

<h2>Admin Site Objects and Related Lookups</h2>

If you use different Admin Site Objects, you have to register <i>every</i> related model within <i>every</i> site object you want to use that model for. Grappelli assumes that you registered <i>all</i> models with your main adminsite.<br>
<i>(This is not considered an issue by the django developers.)</i>

<h2>Searching Generic Relations</h2>

It´s not possible to use a "content_object" within the search_fields. As far as I know, there´s no workaround.<br>
<i>(I´m not sure if this will be solved.)</i>

<h2>Messages in Admin</h2>

It´s currently not possible to distinguish between Success- and Error-Messages.<br>
<i>(Solved with the most recent version of Django.)</i>

<h2>M2M RawID Field has no Unicode representation</h2>

see <a href='http://code.djangoproject.com/ticket/10293'>http://code.djangoproject.com/ticket/10293</a> ... the Patch provided there does work.<br>
<br>
<h2>Popups, Actions and list_editables</h2>

With the current version of Django, Actions are visible within popups but delete confirmation doesn´t handle popups correctly. Moreover, list_editables are also visible. From our point of view, editing elements shouldn´t be possible with popups (and hasn´t been before actions are introduced).<br>
<br>
see <a href='http://code.djangoproject.com/ticket/11700'>http://code.djangoproject.com/ticket/11700</a>

<h2>Admin Documentation</h2>

The document structure of the admin_doc templates is a bit messy (about every second template has a different structure). Therefore, it´s hard to style these pages. Trying to do our best to give it a decent look though.<br>
<br>
Moreover, all admin-views lead to an error.<br>
<br>
<h2>Admin Documentation: Translation</h2>

Translation of the Admin Documentation is half-baked.<br>
<br>
<h2>ModelAdmin Media Definitions</h2>

There´s no distinction between Media for Change-Forms and Media for the Changelist. If you define to load TinyMCE within your Model, it´s already loaded in the Changelist. The same goes for Stylesheets.<br>
<br>
We think there should be distinctive Media-Classes for Change-Form and Changelist. Although it´s not <i>that</i> important, because the javascripts & stylesheets are in your browser-cache anyway.<br>
<br>
<h2>Harcoded Stuff</h2>

With "Hardcoded Stuff", I´m referring to HTML-Code within Views (instead of using Templates). There´s a lot of this within the Admin-Interface and therefore it´s just not possible to style some elements.<br>
(Solved with Grappelli ... to be released soon.)<br>
<br>
<h2>HTML/CSS Framework</h2>

For the Admin-Interface to be customizable, flexible and extensible, we need a coherent scheme with either HTML and CSS. If one wants to customize the change-form for example, it shouldn´t be like "ok, let´s add a new block ... let me think ... there´s no class for what I want ... so let´s just add a new class". instead it should be like "ok, let´s add a new block ... I´m checking the HTML/CSS docs ... finding the right class ... done."<br>
otherwise, almost every 3rd-party app using the admin-interface ends up with custom styles and code-blocks.<br>
<i>(Solved with Grappelli ... to be released soon.)</i>