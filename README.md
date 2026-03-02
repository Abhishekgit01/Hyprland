# anyrun — macOS Spotlight Config (All Plugins)

A fully customisable, macOS Spotlight-style config for [anyrun](https://github.com/anyrun-org/anyrun) on Hyprland / CachyOS.

---

## Files

| File | Purpose |
|---|---|
| `config.ron` | Main config — position, size, behaviour, plugin list |
| `style.css` | GTK CSS — macOS frosted-glass look |
| `applications.ron` | App launcher plugin config |
| `websearch.ron` | Web search plugin config |
| `rink.ron` | Calculator + unit converter config |
| `kidex.ron` | File search plugin config |
| `shell.ron` | Shell command plugin config |
| `symbols.ron` | Unicode/emoji picker config |
| `dictionary.ron` | Dictionary lookup config |
| `translate.ron` | Translation plugin config |
| `stdin.ron` | Stdin/dmenu-style plugin config |
| `randr.ron` | Monitor management plugin config |

---

## Installation on CachyOS / Arch Linux

### 1. Install anyrun and all plugins

```bash
# Using the AUR (recommended on CachyOS)
paru -S anyrun-git

# Or build from source
git clone https://github.com/anyrun-org/anyrun
cd anyrun
cargo build --release --all
```

### 2. Install individual plugin packages (AUR)

```bash
paru -S \
  anyrun-applications-git \
  anyrun-websearch-git \
  anyrun-rink-git \
  anyrun-kidex-git \
  anyrun-shell-git \
  anyrun-symbols-git \
  anyrun-dictionary-git \
  anyrun-translate-git \
  anyrun-stdin-git \
  anyrun-randr-git
```

### 3. Deploy these config files

```bash
mkdir -p ~/.config/anyrun
cp -r anyrun/* ~/.config/anyrun/
```

### 4. Start the kidex daemon (for file search)

Add this to your `~/.config/hypr/hyprland.conf`:

```ini
exec-once = kidex
```

### 5. Add a keybind to launch anyrun

In `~/.config/hypr/hyprland.conf`:

```ini
bind = SUPER, SPACE, exec, anyrun
```

### 6. Enable blur (frosted-glass effect)

In `~/.config/hypr/hyprland.conf`:

```ini
# Blur settings
decoration {
  blur {
    enabled = true
    size = 8
    passes = 2
    new_optimizations = true
  }
}

# Apply blur to the anyrun layer
layerrule = blur, anyrun
layerrule = ignorezero, anyrun
```

### 7. NVIDIA fix (if applicable)

If anyrun hangs on close with an NVIDIA GPU:

```ini
# In hyprland.conf
exec-once = export GSK_RENDERER=ngl
```

Or wrap your keybind:

```ini
bind = SUPER, SPACE, exec, GSK_RENDERER=ngl anyrun
```

---

## Plugin Prefixes (Quick Reference)

| Plugin | Trigger | Example |
|---|---|---|
| Applications | *(just type)* | `firefox` |
| Rink (calc) | *(just type)* | `100km in miles` |
| Web Search | `?` | `? arch linux wiki` |
| Shell | `:sh` | `:sh htop` |
| Symbols | `:sym` | `:sym arrow` |
| Dictionary | `:def` | `:def ephemeral` |
| Translate | `:tr` | `:tr hola` |
| File Search | *(just type)* | `config.ron` |
| Monitor | `:dp` | `:dp rotate` |
| Stdin | *(pipe in)* | `echo -e "a\nb" \| anyrun --plugins libstdin.so` |

---

## Customisation

All `EDIT:` comments in each `.ron` and the `style.css` mark the values you are most likely to want to change (colours, terminal emulator, prefixes, max entries, search engines, target language, etc.).

git clone https://github.com/Abhishekgit01/Hyprland.git ~/dotfiles
mkdir -p ~/.config/anyrun
cp -r ~/dotfiles/anyrun/* ~/.config/anyrun/
