Two Factor Authentication for Nextcloud
=======================================

In Nextcloud, there is the option to set up Two Factor Authentication. The steps you have to follow in order to use it are the following:

1. Install `TOTP` app on Nextcloud.
2. Enable `TOTP` on `Personal Settings`, under `TOTP second-factor auth` section. A QR code will show up.
3. Install `andOTP` on your android phone (you can use any TOTP client you want, `andOTP` is available in F-droid)
4. Scan the QR code that is shown in step 2 with `andOTP`.
5. `andOTP` and Nextcloud are merged and now every 30 seconds a new TOTP password is generated.

Now when you log in you will be prompted, in a second step, to type a TOTP password. Type the password shown in the `andOTP` app.

## App Passwords

You must add `App Passwords` to generate a password for every app that needs access to your Nextcloud account.
Example: Nextcloud Desktop / Mobile Client, DavDroid app, Notes App (Mobile), etc.

To add an App Password do the following.

1. Navigate to Personal settings, under `Settings` section (here you will see every application that has access to your Nextcloud Account). Scroll until you find `App passwords`.
2. Fill in the box that says `App name` with the application's name that you want to use (use a name that is convenient and it is distinguished from other apps).
3. An Application Password is now generated and displayed in a gray box. Type this password (and the your username) on the application you want to use. After you log in hit `Done`. 

*Note: After you type `Done`, the password will never be revealed again. You may want to use a password manager to save this password, or create a new App Password every time you loose a password*





