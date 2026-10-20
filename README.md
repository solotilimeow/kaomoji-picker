# kaomoji picker ٩(◕‿◕)۶

A searchable kaomoji picker for Wayland. Press a shortcut, type a word like `shrug`, `flip table` or `troll`, press Enter, and paste with Ctrl+V.

![Demo: searching for a kaomoji and pasting it](demo.gif)

- **3,179 kaomoji built in**, findable by more than 500 English search words
- **Exact search** that keeps the list order, so the classic kaomoji come first
- **Your own kaomoji** in a plain text file, listed above the built-in ones
- **One Bash script** on top of [fuzzel](https://codeberg.org/dnkl/fuzzel) and [wl-clipboard](https://github.com/bugaevc/wl-clipboard), with nothing to build

Many Wayland pickers type the kaomoji into the window for you with `wtype`, which doesn't work on KDE Plasma. This one copies it to the clipboard instead, so it works the same on every compositor fuzzel runs on.

## Requirements

- A Wayland session on a compositor that fuzzel supports, such as KDE Plasma, Sway or Hyprland. fuzzel doesn't run on GNOME.
- [fuzzel](https://codeberg.org/dnkl/fuzzel) 1.11 or newer
- [wl-clipboard](https://github.com/bugaevc/wl-clipboard)
- libnotify (optional), for the "Copied" notification

| Distro | Install command |
| --- | --- |
| Arch | `sudo pacman -S --needed fuzzel wl-clipboard libnotify` |
| Debian, Ubuntu | `sudo apt install fuzzel wl-clipboard libnotify-bin` |
| Fedora | `sudo dnf install fuzzel wl-clipboard libnotify` |

Check `fuzzel --version` afterwards. Older distro releases ship a fuzzel older than 1.11, which lacks options this script uses.

## Install

```sh
mkdir -p ~/.local/bin
curl -Lo ~/.local/bin/kaomoji https://raw.githubusercontent.com/solotilimeow/kaomoji-picker/main/kaomoji
chmod +x ~/.local/bin/kaomoji
```

Then give it a keyboard shortcut.

**KDE Plasma:** open System Settings → Keyboard → Shortcuts → Add New → Command or Script. Enter the full path, like `/home/you/.local/bin/kaomoji`, and choose a key. Meta+Shift+. sits nicely next to Plasma's emoji picker on Meta+.

**Sway**, in `~/.config/sway/config`:

```
bindsym $mod+Shift+period exec ~/.local/bin/kaomoji
```

**Hyprland**, in `~/.config/hypr/hyprland.conf`:

```
bind = SUPER SHIFT, period, exec, ~/.local/bin/kaomoji
```

To update later, run the `curl` command again. Your own kaomoji aren't affected.

## Usage

Press the shortcut, type a word and press Enter. The kaomoji is copied, and a notification shows it. Paste it with Ctrl+V. Esc closes the picker without copying anything.

Some words to try: `happy`, `cry`, `shrug`, `flip table`, `cat`, `bear`, `sleepy`, `troll`, `sorry`, `high five`, `fish`.

## Your own kaomoji

The first run creates `~/.config/kaomoji.txt`. Add one kaomoji per line: the kaomoji, three spaces, then the words to find it by.

```
(ﾉ´ヮ`)ﾉ*: ･ﾟ   sparkle magic excited
```

Your entries show up above the built-in ones, and a built-in copy of one of yours is hidden. Lines starting with `#` are ignored. Updating the script never touches this file.

## Customizing

Colors and font come from your fuzzel config (`~/.config/fuzzel/fuzzel.ini`). To change the popup's size, edit `--width` (in characters) and `--lines` where the script calls fuzzel. To turn off the notification, delete the `notify-send` lines at the end of the script.

## Contributing

Pull requests that add kaomoji or improve their search words are welcome. Most search words were assigned by category, so a few don't fit their kaomoji perfectly, and fixes for those are welcome too. New entries go in the list at the bottom of `kaomoji`. To keep the list easy to search:

- Use the same format as your own file: kaomoji, three spaces, lowercase search words.
- Skip kaomoji that are already in the list, including near-identical variants.
- Keep every search word at about 50 results or fewer. If a word is that full, use a more specific one.

## Credits

The built-in list is put together from:

- [kaomoji-collection](https://github.com/kaomojiya-collection/kaomoji-collection) by Kaomojiya, for most of the list. The English search words were added for this project.
- [rofimoji](https://github.com/fdw/rofimoji) by Fabian Winter, for the block marked "from rofimoji". Its kaomoji come from [emoticon-data](https://github.com/w33ble/emoticon-data) by Joe Fleming.

All three are released under the MIT License. Their notices are kept in the script and in [LICENSE](LICENSE).

The picker runs on [fuzzel](https://codeberg.org/dnkl/fuzzel) and [wl-clipboard](https://github.com/bugaevc/wl-clipboard).

Built with [Claude](https://claude.ai), Anthropic's AI assistant, which wrote the script and assembled and labeled the kaomoji list.

## License

[MIT](LICENSE)
