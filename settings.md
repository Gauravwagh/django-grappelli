# Grappelli Settings #

All Settings can be defined in your projects settings-file (`settings.py`) or the Grappelli settings-file (`grappelli/settings.py`).

When using the projects settings-file, you have to use the prefix "`GRAPPELLI_`" for every setting (e.g. `GRAPPELLI_ADMIN_TITLE` instead of `ADMIN_TITLE`).

## Available Settings ##

| **Name** | **Description** |
|:---------|:----------------|
| `ADMIN_TITLE` | The Site Title of your Admin-Interface. Change this instead of changing index.html |
| `ADMIN_URL` | The URL to your **Main Admin Site**. Necessary in order to get the right URLs for related lookups registered to different admin site objects. |

## Usage example ##

In the main `settings.py`:

```

GRAPPELLI_ADMIN_TITLE = 'My Application'

```

In `grappelli/settings.py`:

```

ADMIN_TITLE = getattr(settings, "GRAPPELLI_ADMIN_TITLE", 'Grappelli')

```

Gettr is used to ensure any settings found in the main `settings.py` file take precedence over the Grappelli's settings file and provide a default value if none is found.