---
layout: default
---

## AskPass
Replacement for `x11-ssh-askpass`

* ~~Copy input concept from `x11-ssh-askpass`~~ **DONE**
* Don't customize through Xresources, use GTK themestuffs.
  * How do we do this best for custom widgets?

## Greeter
LightDM Greeter

* Clutter to composite
* Implement some modular means of embedding things in the topbar?
  * Isn't there a libindicator or something that Canonical developed?
    * Does anyone use that?  Should we?

## [Settings](projects/settings/planning.html)
Settings host application

* Use INI or JSON file for settings panels to specify their icon and name and category
  * Category?  Do we provide a list or accept a string?  Both maybe?
* Breadcrumbs navigation
* Don't handle actually setting the settings
  * Let the panels handle all that themselves, whether via dconf, gconf, editing files, whatever
* Panels run as subprocesses which XEmbed themselves
  * Pass the XEmbed identifier as an argument to the process
  * How do we do this on Wayland?

## Settings/Network
Network settings panel

* Support NetworkManager and wicd at least
  * Maybe support netctl?
* Study the [images GNOME3's design team compiled for theirs](https://wiki.gnome.org/Design/SystemSettings/Network)
  * Most of them seem broken, might need to recompile them?
    * Install ElementaryOS in a VM?
* Make a logical divide between permanent and temporary profiles maybe?

## Settings/Display
Frontend for xrandr

* Drag and drop screens like everybody else
  * Invent a GTK widget for this
* Allow application to arbitrary X displays?
* How do we do this on Wayland?

## Settings/Audio
Audio subsystem configuration

* Support ALSA and PulseAudio at least
  * Maybe also support JACK
* For mixing systems, should we provide a means of controlling the mixing in further detail?  Like plugboard-style?

## Email
Make the best damn email client for Linux

* Study the UX of GMail and Sparrow.app
* Implement GMail's IMAP extensions
* Contact Mailbox.app and ask them nicely to let us integrate (pls guise halp)
  * Maybe just read-only?
  * I think we technically have a legal right to reverse-engineer their API for compatibility reasons, if it comes to that?

## Calendar
Calendar & todo list application

* Keep the UI simple
* support syncing with Google Calendar
  * Are there any non-Apple ways to hook into iCloud?
  * Are there any other calendar services?
* Integrate with Mailbox, if we can
  * Would be nice to have emails display as tasks when you delay them

## Photo Manager
Danbooru-influenced photo management application

* Tag inheritance?
* auto-tagging
* Probably gonna have to build Tries and other data structures for Vala.  Damn.
