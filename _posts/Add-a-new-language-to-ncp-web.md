Add a new language to ncp-web
=============================

In order to create a new language for _ncp-web_, follow these steps

- start your [development environment](https://github.com/nextcloud/nextcloudpi/wiki/Development-environment)

- download the templates from [here](https://ownyourbits.com/downloads/l10n_templates.zip)

- learn your language code [here](https://www.metamodpro.com/browser-language-codes)

- those files should be copied to `etc/ncp-config.d/l10n/<app>/<languagecode>.json`, except for `__core__.json`, which goes to `ncp-web/l10n/<languagecode>.json`. You can find the languagecode for your currently used language [here](http://mybrowserinfo.com/detail.asp), under 'User Language'. 

- edit those files to add the translation to your language. You can check the results in your browser at `https://localhost:4443`. Refresh to see any changes

- add the language code to `ncp-web/ncp-web.cfg`

- send a pull request with the changes to the _devel_ branch

Example: translate the original template of `nc-backup`

```
{
    "translations": {
        "BACKUPLIMIT": "BACKUPLIMIT",
        "Backup this NC instance to a file": "Backup this NC instance to a file",
        "COMPRESS": "COMPRESS",
        "DESTDIR": "DESTDIR",
        "INCLUDEDATA": "INCLUDEDATA",
        "nc-backup": "nc-backup"
    }
}
```

to German

```
{
    "translations": {
        "BACKUPLIMIT": "Maximale Anzahl", 
        "Backup this NC instance to a file": "Erstelle eine Backupdatei von dieser NC-Instanz", 
        "COMPRESS": "Kompression", 
        "DESTDIR": "Zielverzeichnis", 
        "INCLUDEDATA": "Inkl. Dateien", 
        "nc-backup": "Backup erstellen" 
    } 
}
```


