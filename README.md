# These are just my configs

Not meant for sharing, but feel free to take whatever you like. This project is so I can have the same configs on different machines and as a backup.

# XKB Layout US - German Umlauts

This is mostly copied from: https://github.com/rgeber/xkb-layout-us-intl-de

Custom US based keyboard layout adding Umlauts via the right <ALT> key. Use this with `xkb` on Linux/Unix Systems and X11. Once installed the layout will show up as `English (US, intl., German) in your layout selector.

Tested with Debian Linux. The original project was on Arch (see thanks section).

## Installation

**IMPORTANT:** You're about to mess around with system files controlling the way your keyboard works. If things go south you may end up with a very strange state. Whatever you do, **create a backup** of any file you touch.

### As a US veriant

```
# Create a backup (Example)
sudo cp /usr/share/X11/xkb/symbols/us /usr/share/X11/xkb/rules/evdev.xml /root/
```

Append the contents of `intlde` to `/usr/share/X11/xkb/symbols/us`:

```
sudo cat intlde >> /usr/share/X11/xkb/symbols/us
```

### As a seperate language

```
# Create a backup (Example)
sudo cp /usr/share/X11/xkb/symbols/us /usr/share/X11/xkb/rules/evdev.xml /root/
```

Copy `intlde` into `/usr/share/X11/xkb/symbols/` as a new file:

```
sudo cp intlde /usr/share/X11/xkb/symbols/
sudo chown root:root /usr/share/X11/xkb/symbols/intlde   # Optional
```

Now we need to setup the language in the window manager.

### Sway

In the sway config file (typically `~/.config/sway/config`):

```
input type:keyboard {
  xkb_layout us
  xkb_variant intlde
}
```
or
```
input type:keyboard {
  xkb_layout intlde
}
```

Depending on wether you set it up as it's own language or as a variant of another, you want to set `xkb_layout` and `xkb_variant` accordingly. For more info, see https://wiki.archlinux.org/title/Sway

Reload the config with Hyper+Shift+c, and try it out.

### Gnome, KDE, etc.

Next, make the layout available to the various keyboard managers by adding the following block to the variants section of the US Layout. This is a bit tricky as you need to find the right spot in the XML file first.

Variants are defined under `layoutList -> layout`. If you can't find that run a search for `US, intl.`. This should put you in the right spot. Just append the variant block below that:

```
<variant>
  <configItem>
    <name>intlde</name>
    <description>English (US, intl., German)</description>
  </configItem>
</variant>
```

Last but not least, activate the layout using your Desktop's layout manager.

### X.org config

You may choose to set the layout though the cofiguration of X.org directly. The file `10-keyboard.conf` offers an example configuration. This way works regardless of the window managers capabilities.

## Usage

Once active, you'll be able to type `äÄ`, `öÖ`, `üÜ` and `ß` holding down your **right alt key** and optionally the shift key.

| Combination       | Result |
|-------------------|--------|
| RAlt + a          | ä      |
| RAlt + o          | ö      |
| RAlt + u          | ü      |
| RAlt + Shift + a  | Ä      |
| RAlt + Shift + o  | Ö      |
| RAlt + Shift + u  | Ü      |
| RAlt + s          | ß      |
| RAlt + e          | €      |
| RAlt + q          | @      |

* The letters `z` and `y` are like in the German keyboard.
* The RAlt+[Num] and RAlt+Shift+[Num] give special symbols.
* The key left of `y` is remapped to be `(` and `)`, instead of `<` and `>` (the `|` remains).

Have fun!

## Troubleshooting

So far this is a "works form me" repository. Feel free to open issues if things don't work fo you. Make sure to mention your exact OS versions and I'll see what I can do for you.

## Thanks

https://github.com/rgeber/xkb-layout-us-intl-de
