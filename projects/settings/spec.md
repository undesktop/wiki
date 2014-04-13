---
layout: default
---

# Settings Specification {#prelude}
This specification was not authored by professional spec-writers.  For unspecified or vague things,
please refer to the [freedesktop.org Desktop Entry Spec][desktop-entry-spec].  This specification
draws heavily from that document.

[desktop-entry-spec]: http://standards.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html

## Settings Host {#host}
The **Settings Host** ("Host") handles listing, displaying, launching, and managing communications
to and from its Settings Panel ("Panel") subprocesses.

To retrieve the list of Panels, the Host uses [the same algorithm specified for desktop files
][desktop-entry-algo] (except in `$XDG_DATA_DIRS/spanels/` instead) and looks for [Settings Panel
Specification](#panel-spec-format) ("Spec") files.  For an idea of the defaults, see [Appendix A
](#appendix-a)

When the User requests that the Host should display a Panel, the Host will launch that Panel as a
subprocess according to the settings in the Spec file and then communicate with it as specified in
the [Host-Panel Communications](#host-panel-comm) section.

[desktop-entry-algo]: http://standards.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#desktop-file-id

## Settings Panel {#panel}
The **Settings Panels** handle the actual settings management.  They are given absolute freedom to
display whatever they want to display.

## Settings Panel Specification Format {#panel-spec-format}
The Settings Panel Specification Format uses the [Glib Key File Format][gkeyfile] with the sections
and keys specified in [Appendix B](#appendix-panel-file).  The format can be extended exactly the
same as a desktop file (`X-` prefix on a key or section)

[gkeyfile]: https://developer.gnome.org/glib/unstable/glib-Key-value-file-parser.html#glib-Key-value-file-parser.description

## Host-Panel Communications {#host-panel-comm}
The Host launches the Panel with the XEmbed window id as the first argument.  When the Host unloads
a Panel, it should send a SIGHUP to the child process.

To communicate with the Panel and other processes, we use a D-Bus connection.  The Host should
register itself under the name `org.undesktop.settings` and implement the methods specified in
[Appendix C](#appendix-dbus-methods)

## Appendix A: Search Paths {#appendix-search-paths}

Location                 | Defaults                                             | Description             |
:------------------------+:-----------------------------------------------------+:------------------------|
`$XDG_DATA_DIRS/spanels` | `/usr/local/share/settings/`, `/usr/share/settings/` | System-wide search path |
`$XDG_DATA_HOME/spanels` | `$HOME/.local/share`                                 | Per-user search path    |
{:.search-paths-table}


## Appendix B: `.panel` file {#appendix-panel-file}
The basic format of the panel file requires that there be a group header named `Settings Panel`.
There may be other groups present in the file, but this is the most important group which is always
required. There should be nothing preceding this group in the file except possibly comments.

Key          | Description                                                         | Value Type     | Req |
:------------+:--------------------------------------------------------------------+:---------------+:---:|
`Version`    | Version of the Settings Panel Specification the file conforms with. | string         | no  |
`Name`       | Specific name of the Panel                                          | localestring   | yes |
`Icon`       | Icon to represent the Panel. If this is an absolute path, that file will be used.  Otherwise, the algorithm described in the [Icon Theme Specification][icon-theme-spec] will be used to locate the icon. | string         | yes |
`Comment`    | Extended description of the Panel's purpose.                        | localestring   | yes |
`Categories` | Categories in which the Panel should be grouped. For the list of standardized options, see [Appendix D](#appendix-d). Non-standard categories should be prefixed with an `X-` and handled according to the specification's section on extensibility. | string[]       | yes |
`Keywords`   | A list of strings which may be used in addition to other metadata to describe this entry. This may be useful for searching functions.  The values are not meant for display. | localestring[] | no |
`Exec`       | Program to execute, possibly with arguments.                        | string         | yes |
{:.panel-file-table}

[icon-theme-spec]: http://freedesktop.org/wiki/Standards/icon-theme-spec

## Appendix C: D-Bus Methods {#appendix-dbus-methods}

### Panel->Host Commands
> Should we do OOP shit with these or something? `Nuck`{:.sig}
{:.note}

`progress_bar_set_text(string text)`
`progress_bar_set_fraction(double fraction)`
`progress_bar_pulse()`

### Host->Panel Commands
> Half of these seem like they ought to be abstracted more `Nuck`{:.sig}
{:.note}

`search_box_activated()`
`search_box_text_changed()`
`search_box_set_text(string text)`
`search_box_set_sensitive(bool sensitive)`

### Anything->Host Commands
`load_panel(string specfile)`


