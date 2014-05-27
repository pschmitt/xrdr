# xrdr

## Description

Simple XRandR wrapper written in Bash. Supports simple layout files and theoretically an infinite number of screens

## Dependencies

* [XRandR](http://www.x.org/wiki/Projects/XRandR/)
* [dzen2](https://github.com/robm/dzen) (for identifying screens)

## Installation

### ArchLinux

```bash
wget https://raw.github.com/pschmitt/xrdr/master/PKGBUILD
makepkg -si
```

### Other distros

```bash
wget https://raw.github.com/pschmitt/xrdr/master/xrdr
chmod +x xrdr
```

### Usage

* `xrdr auto`: Automatically expand if more than one display is detected. If only one display is attached, invoque `xrandr --auto` to dismiss old screens.
* `xrdr extend`: Extend displays
* `xrdr copy`: Copy output (some portions may be missing if the primary and secondary screens use different ratios)
* `xrdr identify`: Identify displays. Outputs screen name and resolution on screen (using dzen2)
* `xrdr primary`: Turn off all screens, except the first one
* `xrdr secondary`: Turn off all screens, except the second one
* `xrdr tertiary`: Turn off all screens, except the third one
* `xrdr count`: Output the number of currently connected screens
* `xrdr vertical SCREENNUMBER`: **Return** 0 if said screen is in portrait mode, 0 otherwise
* `xrdr layout`: Print current layout to stdout
* `xrdr LAYOUT_FILE`: Apply layout from `LAYOUT_FILE`

### Hooks

If you want to automatically execute a script after display adjustement, create `$HOME/.config/xrdr/xrdr.hook`. Here's mine:

```
xmonad --restart
sleep 2 && nitrogen --restore
```

### Configuration

A valid configuration is automatically (`$HOME/.config/xrdr/xrdr.conf`) written after execution. You can overwrite it, but bear in mind that it gets rewritten after exectuting xrdr. If you want a persistant config consider using `/etc/xrdr.conf`, espcially if the screens aren't in the right order.

Example:

```
PRIMARY_SCREEN="DFP1"
SECONDARY_SCREEN="DFP5"
TERTIARY_SCREEN="DFP6"
```

### Layouts

As of version 2.5.0 instead of using the explicit command line options you can write a layout config file. Take a look at the [sample](layout.conf.sample) in the repo. Mine looks like this:

```
2 | 1* | 3r
```

This will place screen #1 in between screen #2 and #3 and set it as the primary display. Display #3 will be rotated 90° (right):

```
                               ----
                              |    |
 -----------    -----------   |    |
| Display 2 |  | Display 1 |  | #3 |
 -----------    -----------   |    |
                              |    |
                               ----
```


Multiline layouts *should* work too, but I didn't test it that much as I don't use it myself.
