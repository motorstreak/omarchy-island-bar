# Omarchy Island Bar

Omarchy's own top bar, with each section (left, center, right) on its own
floating, rounded island instead of one full-width strip. The wallpaper shows
between the islands, which sit a small gap away from the screen edge.

Everything else is Omarchy's bar: the same widgets, layout, settings, gestures
and `omarchy bar` commands, and the same theme colours.

## Install

```bash
omarchy plugin add https://github.com/motorstreak/omarchy-island-bar.git --enable
omarchy bar use island-bar
```

Go back to Omarchy's bar with `omarchy bar use omarchy.bar`. Update with
`omarchy plugin update island-bar`.

## Translucent, blurred islands (optional)

The islands use the theme's bar colour. To make them translucent, add to
`~/.config/omarchy/shell.toml`:

```toml
[bar]
background-alpha = 0.7
```

To blur what shows through them, add to `~/.config/hypr/looknfeel.lua`.
Hyprland has one blur switch for everything, so this turns it on, takes it off
every window again, and gives it to the bar only where the islands are:

```lua
hl.config({ decoration = { blur = { enabled = true, size = 8, passes = 2 } } })
hl.window_rule({ match = { class = ".*" }, no_blur = true })
hl.layer_rule({ match = { namespace = "omarchy-bar" }, blur = true, ignore_alpha = 0.05 })
```

Hyprland applies layer rules when the bar appears, so run
`omarchy restart shell` once after adding them. The only thing ever behind the
bar is the wallpaper, so the blur shows over busy wallpapers and is barely
visible over smooth ones.

## Tuning

At the top of `Bar.qml`:

- `islandGap`: space between the islands and the screen edge
- `islandPad`: padding inside each island
- `islandRadius`: corner radius (half the bar height: fully rounded ends)

Islands apply to a top or bottom bar; a bar on the left or right is drawn as
one strip, as in Omarchy. Making the bar transparent (double-click empty
center-bar space, or `omarchy bar transparent true`) hides the islands too.

## Keeping up with Omarchy

This is a copy of Omarchy's bar (`shell/plugins/bar` in
[basecamp/omarchy](https://github.com/basecamp/omarchy)), so it doesn't get
Omarchy's bar improvements by itself. The island changes are small and
contained in `Bar.qml`: look for `islands`, `band` and `islandColor`.
Omarchy's own notes on the bar are in [docs/omarchy-bar.md](docs/omarchy-bar.md).

## License

MIT, as Omarchy. See [LICENSE](LICENSE).
