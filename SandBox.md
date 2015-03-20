# Grappelli Sandbox #

The sandbox is a generic project with a sqlite3 database. It's useful to test a branch or even develop new features.

grappelli is included as external, so to switch from grappelli branches or trunk only a svn switch is necessary (or editing the externals).

```

svn co https://django-grappelli.googlecode.com/svn/branches/sandbox grappelli-sandbox

```

**Tip**: The sandbox comes with fixtures for a default super user so you don't have to create one each time you rebuild the test database. The default username password is **admin/admin**.

**Pro Tip**:

```
rm -f test.db && python manage.py syncdb --noinput
```


# Default username/pass #

| **user** | admin |
|:---------|:------|
| **pass** | admin |

I also included a set of basic apps useful to really test grappelli:

# Contrib #

  * django-grappelli (haineault's branch by default)
  * django-evolution
  * filebrowser
  * sorl

# Repository swapping #

## Permanent method: changing external ##

```

svn propedit svn:externals contrib/

```

You should see this in your default editor:

```

https://django-grappelli.googlecode.com/svn/branches/haineault grappelli
http://django-evolution.googlecode.com/svn/trunk/django_evolution django_evolution
http://django-filebrowser.googlecode.com/svn/trunk/filebrowser/ filebrowser

```

Save the file and do a `svn up`.

## Temporary method: switching ##

In this example I'm switching  the current working copy source for the trunk:

```

cd contrib/grappelli/
svn switch http://django-grappelli.googlecode.com/svn/trunk/

```

**Note to commiters**: make sure you have committed everything before doing this and when you do, perform the commit in the `grappelli` folder, try not to commit `contrib` folder in the sandbox unless it's really intended.