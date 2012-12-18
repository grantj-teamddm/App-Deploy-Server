# App Deploy Server

Howdy! This is TeamDDM's App Deploy server code. It's an extremely simple website developed in PHP.

## Requirements

Apache, PHP, mod_rewrite, `.htaccess` (or access to your Apache config).

We do the oh-so-common pretty-url rewrite, so that's what we're doing with the `.htaccess` file.

Currently it assumes that the app lives at the webroot. Need it to be smarter? Pull request, baby.

## Usage

Install. Point Apache.

### Bundles

The server will look at all the directories within in the "bundles" directory. To make a bundle (and thus IPA file) available, you should place a directory with the following files inside the `bundles` directory. So:

    bundles/
        MyAppBundle/
            myBuiltApp.ipa
            myBuiltApp.plist
            icon-72.png
            readme.md

### Required Bundle Files

 - `myBuiltApp.ipa`: You can actually name this whatever you want, as long as it ends in `.ipa`. This is the final app ipa that XCode builds, signed with your ad-hoc or enterprise deployment certificate and profile.
 - `myBuiltApp.plist`: This is the plist file that the organizer will offer to make for you if you choose "Enterprise Deployment". When you make this file, there are two values to use:
   - `IPA_URL`: Use this as a placeholder for the URL to the app file. The deploy server will replace this in your plist with the actual URL to your ipa file.
   - `ICON_72_URL`: Use this as a placeholder for the URL to your app icon. This is optional, but if you provide it, then the iOS device will display this icon while the app is downloading and installing.

### Optional Bundle Files

 - `icon-72.png`: If you provide an icon-72, its URL will be provided to the plist via the ICON_72_URL placeholder. This file will also be used on the front-end of the site to display the icon of the app. If this is missing, the website will use a placeholder instead.
 - `readme.md`: If provided, an `Info` button will be placed next to your app's listing. This provides a standalone page for the app, so that you can detail any special instructions, credits, FAQ's that you want for the app.

## What's not here

 - Login. If you use this for enterprise deployment, make sure you put a login in front of it somehow, unless you are restricting access in some other way. At TeamDDM, we only have this server accessible from our internal network (presently, at least), so we aren't building a login system just yet.
 - Tracking. There's no tracking or information of any kind detailing who ipa's are getting distributed to or when. It just isn't needed yet (although it's something we're definitely thinking about).
