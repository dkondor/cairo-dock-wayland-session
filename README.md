# Wayfire session with Cairo-Dock

This repository provides a systemd session running [Wayfire](https://github.com/WayfireWM/wayfire) as the compositor and [Cairo-Dock](https://github.com/Cairo-Dock/cairo-dock-core) as a dock, along with a few useful components. This is one of the recommended ways to run a Wayland session with Cairo-Dock (see [here](https://github.com/Cairo-Dock/cairo-dock-core/wiki/Running#1-run-the-cairo-dock-desktop-session) for more info).


# Requirements

The goal of this session is to provide a simple, but complete desktop environment, built from a set of required components.

## Essential

These are required to actually be able to log in and start the session :)

 - [Wayfire](https://github.com/WayfireWM/wayfire) tested on version 0.8.0 (in the Ubuntu 24.04 repositories) and newer.
 - Cairo-Dock with Wayland support, version 3.5.99 or newer (see the wiki for instructions to [install](https://github.com/Cairo-Dock/cairo-dock-core/wiki/Installation) it or [build](https://github.com/Cairo-Dock/cairo-dock-core/wiki/Compiling-from-source) it from source).
 - [systemd](https://systemd.io/) set up according to your distribution to manage system services.
 - A login manager capable of starting Wayland sessions; tested with Gdm, but recent versions of LightDM, SDDM, etc. should also work.


## Main components

These are required to get a usable desktop (things might work without some, but usability will be limited):

### SSH agent, keyring and privilege management

 - GNOME keyring daemon and PAM integration ([source](https://gitlab.gnome.org/GNOME/gnome-keyring), Ubuntu / Debian packages: `libpam-gnome-keyring`, `gnome-keyring`)
 - GNOME crypto services SSH agent (Ubuntu package: `gcr4` / Debian package: `gcr`)
 - MATE polkit authentication agent (required for being able to authenticate for privileged actions; the GNOME version does not work; [source](https://github.com/mate-desktop/mate-polkit), Ubuntu / Debian package: `mate-polkit`)

### Screen locking

 - [wayland-screenlock-proxy](https://github.com/dkondor/wayland-screenlock-proxy) a proxy service to integrate screenlockers
 - one of the following screenlockers: [waylock](https://github.com/swaywm/swaylock), [gtklock](https://github.com/jovanlanik/gtklock) or [Waylock](https://codeberg.org/ifreund/waylock) (the first two are available as Ubuntu / Debian packages already)

### Desktop components

 - wallpaper (`wf-background`) from [wf-shell](https://github.com/WayfireWM/wf-shell) (available on Debian testing or Ubuntu)
 - for basic configuration: [wcm](https://github.com/WayfireWM/wcm) (available only on Debian testing / Ubuntu 24.10 or newer)
 - a Wayfire plugin with an extra "overview" action for better integration: [wayfire-scale-ipc](https://github.com/dkondor/wayfire-scale-ipc)


## Recommended components

These allow a more complete desktop experience, including additional settings:
 - GNOME settings daemon components: `gsd-rfkill` and `gsd-xsettings` (part of the `gnome-settings-daemon` package on Ubuntu / Debian)
 - Network manager (`nm-applet`; `network-manager-gnome` package on Ubuntu / Debian)
 - GNOME control center (system settings; `gnome-control-center` package on Ubuntu / Debian)
 - GNOME Tweaks (system theme and appearance settings; `gnome-tweaks` package on Ubuntu / Debian)
 - A notification daemon, e.g. [mako](https://github.com/emersion/mako) (`mako-notifier` package on Ubuntu / Debian)


# Installing

The standard way to build is with Meson:

```
meson setup -Dbuildtype=release build
ninja -C build
sudo ninja -C build install
```

By default, this will install files under `/usr/local`. On most systems, this should work fine; if not, you might need to copy the file `cairo-dock-wayfire.desktop` from `/usr/local/share/wayland-sessions/` to `/usr/share/wayland-sessions/`.


# Running

If installed correctly, you can select "Wayfire/Cairo-Dock" in your graphical login manager. From the command line, it can be started by the `cairo-dock-wayfire-session`, installed under the `libexec` directory in the prefix (i.e. `/usr/local/libexec/cairo-dock-wayfire-session` by default).


