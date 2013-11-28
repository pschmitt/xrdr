# xrdr

## Description

Simple Xrandr wrapper written in Bash. Supports up to 3 screens (for now).

## Dependencies
* xrandr
* dzen2 (for identifying screens)

## Installation

### ArchLinux

```bash
wget https://raw.github.com/pschmitt/xrdr/master/PKGBUILD
makepkg -si
```

### Other distros

```bash
wget https://raw.github.com/pschmitt/xrdr/master/xrdr
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

### Hooks

If you want to automatically execute a script after display adjustement, create `$HOME/xrdr/xrdr.hook`. Here's mine:

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
