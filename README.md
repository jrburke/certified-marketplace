# Certified Apps in the Firefox Marketplace

Can we allow [certified apps](https://developer.mozilla.org/en-US/Firefox_OS/Security/Application_security) to be delivered through the [Firefox Marketplace](https://marketplace.firefox.com/)?

## Why

Why should we consider doing this?

### Timely updates

Apps can be updated without needing a full OS version certification. There are cases where a quick update to some targeted bug fixes really help users and do not rely on a full platform certification.

This is also the expected, desired model of web apps.

### Expands number of certified apps

It would be possible to grant an app certified powers without it needing to be delivered in an OS update. While there should still be a human vetting process, it will be easier to expand the list of certified apps to developers outside the people that have commit writes to Gaia or to the device distributions.

### Decoupled Gaia apps

By allowing direct delivery to the Marketplace, the Gaia apps can be decoupled from each other, and the Gaia repo can focus on aggegrating the apps for device imaging.

### Better app content verification

This is not a primary concern, but it should be possible to provide stronger guarantees that what is in the app zip corresponds directly to what is in an app's open source repo. As it stands now, the app zips pass through many gates on the pathway out to the user, with each gate hop a chance for the app zip to be modified.

## What

What is the purpose of a "certified" app vs a "privileged" one? By identifying this purpose, we can maintain it going forward. There are a couple reasons "certified" apps exist:

### Sensitive APIS

The app uses more sensitive APIs on the device, where the user benefits by very controlled access to those APIs for security and stability reasons.

### Beta platform features

For Firefox OS, advanced platform features may only be available to "certified" apps. This is because those features may still be new and not fully battle tested or their design may not be fully verified, and by restricting their use to "certified" apps, there is a stronger guarantee that those apps will correctly adjust to the platform feature as it changes over time.

This capability is really beneficial to the platform: it provides some real world use of the APIs before opening them up to the broader web. Since certified apps are kept up to date with new Gecko releases, and the certified apps are only delivered with specific Gecko versions, it maintains this sort of "beta" access while not forcing the platform to need to support an older, more awkward or buggy implementation if the feature was just released immediately to the broader web.

## How

Certified apps could be delivered in a similar fashion to privileged apps, but with some extra checks in place:

* The Marketplace should allow specifying Gecko version numbers that are compatible with a given app zip.
* The Marketplace allows multiple app zips for a given app, that can be separated by Gecko version number.
* The apps are signed by a key that prove they are from a blessed developer that has agreed to the certified contract. This signing verification may just need to happen on zip upload, as a start, although it could be extended to the device checking the signature.
* The OS upgrade mechanism on the device needs to be changed: if the OS is updated, and the new Gecko is it a new version number, it needs to ensure it has access to the certified app versions for that Gecko version.


## Open questions

Some of these relate to how to get smaller zip files as some devices are very storage and memory constrained:

* How to deal with graphics: we have 1x, 2x, 2.5x, etc.. graphics for some things. Maybe the hope is to move to vector graphics for everything, but the platform may not move as fast. Maybe we just decide to deliver all the graphics in that case.
* How to deal with localizations. We can avoid some overhead by only delivering localizations that are only used on the device. On localizations, for the email app, the oauth settings to gmail, gmail shows some localizable strings from the oauth client ID profile, so the localizations go beyond just local localized string replacements.

It may make sense to allow different app zips per device resolution and even per locale.

Or in the case of locale, perhaps a separate mechanism to allow installing of new locales via localization zips.








