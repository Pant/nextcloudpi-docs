NCP app developer guide
=======================

[ncp-web]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#ncp-web
[nc-datadir]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-datadir
[ncp-update]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#ncp-update
[nc-backup-auto]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-backup-auto

This section explains the basics for creating a new functionality that will show up in nextcloudpi-config and [`ncp-web`][ncp-web].

See also [how to use the development environment](https://github.com/nextcloud/nextcloudpi/wiki/Development-environment).

## Anatomy of a ncp-app

An ncp configuration option, such as [`nc-datadir`][nc-datadir], is defined by a single bash _.sh_ file in `/usr/local/etc/ncp-config.d`.

In order to be launched from the web interface, it needs a permission mask 660 and ownership root:www-data

```
chown -R root:www-data /usr/local/etc/ncp-config.d 
chmod 660 /usr/local/etc/ncp-config.d/*
```

### Functions
It needs to define two functions called `install()` and `configure()`, and optionally another one called `cleanup()`.

 - The _install()_ function is called during the build process and also during [`ncp-update`][ncp-update] if it hasn't been installed before.
 - The _configure()_ function is called when 
    - launched from [`ncp-web`][ncp-web],or `ncp-config`
    - during installation ( during build, or from [`ncp-update`][ncp-update] ) if it has a field `ACTIVE_=yes`
 - The _cleanup()_ function is only called at the end of the image building process, to leave the system as clean as possible after installation. Optional.


### Public fields
"Fields" that will show up in [`ncp-web`][ncp-web] and nextcloudpi-config for the user to modify are only bash variables with a special name. If a variable ends in underscore `_`, then it will be modifiable by the user. The original value will be left as a suggestion or default.

For instance, the top of the ['nc-backup-auto'][nc-backup-auto] option shows the following variables

```
ACTIVE_=yes
DESTDIR_=/media/USBdrive
INCLUDEDATA_=yes
BACKUPDAYS_=7
BACKUPLIMIT_=4
DESCRIPTION="Periodic backups"
```

And looks like this

![nc-backup-auto](https://ownyourbits.com/wp-content/uploads/2017/08/ncp-web2.jpg)

### Special fields
There's some fields fields that have a special behavior

 - `DESCRIPTION` is used to show a little explanation in the webUI or TUI and is a mandatory field.
 - `ACTIVE_` will show a ✓ next to the option when it has the value `yes`. Optional.
 - `INFO` will display the contents of this string in the interface. Used to provide some additional information such as warnings and instructions. Optional.
 - `INFOTITLE` header for the `INFO` box. Defaults to "Info" if it is not provided. Optional.

Also, any field that reads `yes` or `no` will be displayed as a checkbox in the web interface.

## Code style

Please, check for style and common mistakes by running [shellcheck](http://www.shellcheck.net/) on your script before submitting.

```
shellcheck -s bash myscript.sh
```
