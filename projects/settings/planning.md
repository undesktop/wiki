---
layout: default
---

# Settings Host Planning

## Layout Mockup
![]({{ site.github.url }}/img/Settings-layout.svg){:.wide-image}

## Other Projects' Solutions

### ElementaryOS
[ElementaryOS](http://launchpad.net/switchboard) seems to handle it via GtkPlug and an ini-format
`.plugin` file, perhaps aim for compatibility with their API?  Their
[example](https://code.launchpad.net/~xapantu/switchboard/plug-sample) is pretty easy to follow.

### GNOME3
GNOME3 appears to use GModules to implement their settings daemon.  Unity uses a fork of this.

### KDE
KDE seems to work based on configuration skeletons: you specify the fields it will expose, and then
it exposes them properly.

### OSX?
*To Be Researched*

### iOS
*To Be Researched*

### Android
*To Be Researched*
