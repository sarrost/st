# My personal build of st - the simple (suckless) terminal

The [suckless terminal (st)](https://st.suckless.org/) with some custom features. This build (and README) is originally a fork of [Luke's build](https://github.com/lukesmithxyz/st) with some slight modifications.

## Installation 

```
git clone https://github.com/sarrost/st
cd st
sudo make install
```

### Dependencies

Chances are, you have all of this installed already, but to be safe:

* `make` is required to build
* `fontconfig` is required for the default build, since it asks `fontconfig` for your system monospace font.  
* `libX11` and `libXft`

On OpenBSD, be sure to edit `config.mk` first and remove `-lrt` from the `$LIBS` before compiling.

Be sure to have a composite manager (`xcompmgr`, `compton`, etc.) running if you want transparency.

## Unique features (using rofi)

* **Follow urls** by pressing `alt-l`
* **Copy urls** in the same way with `alt-y`
* **Copy the output of commands** with `alt-o` (`xsel` is required)

## Bindings

* **Scroll** back/forth with `alt-k/j` or holding `alt` and scrolling with the mouse. Faster with `alt-u`/`alt-d`
* **Zoom/change font size**: same bindings as above, but holding down shift as well. `alt-h` returns to default
* **Copy/paste text** with `alt-c/v`

## Pretty stuff

* Compatibility with `.Xresources` and `pywal` for dynamic colors. The `Xdefaults` file shows a usage example.
* Default [gruvbox](https://github.com/morhetz/gruvbox) colors otherwise.
* Transparency/alpha, which is also adjustable from your `.Xresources`.
* Default font is system `mono` at `22pt`, meaning the font probably will **not** match your system font.

## Extra keys

It's free real estate with regards to keysyms. Most key-combos that are possible are available as unique keysysms.

By default st and most other terminals do not recognize or make a distinction between certain key presses. This is for (prehistoric) backwards compatibility purposes. For example `Tab` and `Ctrl-i`, `Enter` and	`Ctrl-m`, `ESC` and `CTRL-[`, etc. Are treated as the same key by default. By default the terminal registers `Enter`, `Ctrl-Enter`, `Shift-Enter` etc. all as the same key. With this build all unique key-combos have unique keysysms, with a few exceptions.

Some terminal programs, such as [vim](https://www.vim.org/), will be stubborn and may require keys such as `Ctrl-i` to by bound to another key entirely (in this build it is bound to non-existent `F13`) in order for it to be distuishable from `Tab`.

## How to configure dynamically with .Xresources

For many key variables, this build of `st` will look for X settings set in either `~/.Xdefaults` or `~/.Xresources`. You must run `xrdb` on one of these files to load the settings.

For example, you can define your desired fonts, transparency or colors:

```
...

*.font:	Liberation Mono:pixelsize=12:antialias=true:autohint=true;
*.alpha: 0.9
*.color0: #111

...
```

The `alpha` value (for transparency) goes from `0` (transparent) to `1` (opaque).

### Colors

To be clear about the color settings:

* This build will use gruvbox colors by default and as a fallback.
* If there are Xresources colors defined, those will take priority.
* But if `wal` has run in your session, its colors will take priority.

Note that when you run `wal`, it will negate the transparency of existing windows, but new windows will continue with the previously defined transparency.

## Notes on Emojis and Special Characters

If st crashes when viewing emojis, install [libxft-bgra](https://aur.archlinux.org/packages/libxft-bgra/) from the AUR if you're on arch.

Note that some special characters may appear truncated if too wide. You might want to manually set your prefered emoji/special character font to a lower size in the `config.h` file to avoid this. By default, JoyPixels is used at a smaller size than the usual text.  

## Patches

* [vertcenter](https://st.suckless.org/patches/vertcenter/)
* [scrollback](https://st.suckless.org/patches/scrollback/)
* [font2](https://st.suckless.org/patches/font2/)
* [fix keyboard input](https://st.suckless.org/patches/fix_keyboard_input/)
* updated to version [0.8.2](https://dl.suckless.org/st/st-0.8.2.tar.gz)


## Contact

* Herbert Magaya <herbert.magaya@protonmail.com>
