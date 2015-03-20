# Using TinyMCE #

  1. **Copy and Change tinymce\_setup.js**
> > Copy tinymce\_setup.js (in order to not break future updates) and adjust the setup/behaviour of TinyMCE according to your needs - see http://wiki.moxiecode.com/index.php/TinyMCE:Configuration
  1. **Change the media-definition of your ModelAdmin**
```
    class Media:
        js = ['/media/admin/tinymce/jscripts/tiny_mce/tiny_mce.js', '/path/to/your/tinymce_setup.js',]
```
  1. **Check the file tinymce\_setup.js and change it (if you need to).**

![http://vonautomatisch.at/media/uploads/grappelli/tinymce.jpg](http://vonautomatisch.at/media/uploads/grappelli/tinymce.jpg)