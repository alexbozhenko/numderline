
<https://blog.janestreet.com/commas-in-big-numbers-everywhere/>

This is my fork of <https://github.com/trishume/numderline>
with change to not use thosands separators for numbers less than 10000,
as suggested here: <https://news.ycombinator.com/item?id=21362269>

I also commited patched FiraCode font to the out directory.

##

TL;DR on Arch Linux:
Install fira code, and variant with ligatures:

```
yay ttf-fira-code
yay ttf-firacode-nerd
```

Patch the font:

```
python3  patcher.py --group /usr/share/fonts/TTF/FiraCodeNerdFont-Regular.ttf
```

Copy patched font to the system locaiton:

```
sudo cp "out/FiraCode Nerd Font Reg with NGroup.ttf" /usr/share/fonts/
sudo fc-cache -fv
```

Find out that name of the font family to use in the config:

```
fc-list : family  | grep -i ngroup
```

Set  it in vscode in settings.json:

```
    "editor.fontFamily": "FiraCode Nerd Font with NGroup",
    "editor.fontLigatures": true,
    
    "terminal.integrated.fontFamily": "FiraCode Nerd Font with NGroup",
    "terminal.integrated.fontLigatures.enabled": true,
```

Not all terminals support font shaping, but ghostty does:

```
font-family = "FiraCode Nerd Font Mono with NGroup"
```

# Numderline

Numderline is a hacky font patcher that takes a font and converts it into one that underlines alternating groups of 3 digits starting from the right. It can also do other similar tricks.

It was inspired by [my job](https://www.janestreet.com/technology/) involving a lot of staring at numbers in nanoseconds and trying to pick out the milliseconds or microseconds.

A blog post about this and a web page to see and download pre-patched fonts should hopefully be coming soon™.

## Features

- Patch any font to underline alternating groups of 3 digits in numbers
- For use in proportional contexts, can also just insert fake commas with shaping
- Alternatively it can squish digits and group them closer together in threes
- Or some other variants, including small monospace mini-commas!

### Usage

1. Clone the repo
1. Install the FontForge Python API, on macOS I used Homebrew to do this with `brew install fontforge`, or you can use `brew bundle`
1. Install the fonttools API, I used `pip3 install fonttools` to install it in my Homebrew python3, or you can use `pip3 install -r requirements.txt`
1. Run `python3 patcher.py FONT_FILE_TO_PATCH` and look in the `out` folder

You can also run `python3 patcher.py --help` and read the source to see other options.
