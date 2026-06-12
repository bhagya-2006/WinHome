# Dotfiles

Creates symbolic links for your dotfiles 
to manage configuration files across your 
Windows development environment.

**YAML Key:** `dotfiles`

**Properties:**

- `src` : The source file path.
- `target` : The target link path. 
  Environment variables and `~` are supported.

---

## Basic Usage

```yaml
dotfiles:
  - src: dotfiles/.gitconfig
    target: ~/.gitconfig
  - src: dotfiles/.zshrc
    target: ~/.zshrc
```

---

## Advanced Configuration

### Using Environment Variables in Paths

```yaml
dotfiles:
  - src: dotfiles/settings.json
    target: "%APPDATA%\\Code\\User\\settings.json"
  - src: dotfiles/.gitconfig
    target: ~/.gitconfig
```

---

## Real-World config.yaml Examples

### Example 1 — Git Configuration

```yaml
dotfiles:
  - src: dotfiles/.gitconfig
    target: ~/.gitconfig
  - src: dotfiles/.gitignore_global
    target: ~/.gitignore_global
```

### Example 2 — Shell Configuration

```yaml
dotfiles:
  - src: dotfiles/.bashrc
    target: ~/.bashrc
  - src: dotfiles/.zshrc
    target: ~/.zshrc
  - src: dotfiles/.profile
    target: ~/.profile
```

### Example 3 — VSCode Settings

```yaml
dotfiles:
  - src: dotfiles/vscode/settings.json
    target: "%APPDATA%\\Code\\User\\settings.json"
  - src: dotfiles/vscode/keybindings.json
    target: "%APPDATA%\\Code\\User\\keybindings.json"
```

### Example 4 — Complete Developer Setup

```yaml
dotfiles:
  - src: dotfiles/.gitconfig
    target: ~/.gitconfig
  - src: dotfiles/.zshrc
    target: ~/.zshrc
  - src: dotfiles/vscode/settings.json
    target: "%APPDATA%\\Code\\User\\settings.json"
  - src: dotfiles/windows-terminal/settings.json
    target: "%LOCALAPPDATA%\\Packages\\terminal\\settings.json"
```

---

## Troubleshooting

**Issue: Symbolic link not created**
- Make sure WinHome is run as Administrator
- Check if source file exists
- Verify source path is correct

**Issue: Target path not found**
- Check environment variables are correct
- Make sure target directory exists
- Use full path if `~` is not working

**Issue: Link already exists**
- Delete existing file at target path
- Re-run WinHome to create new link
- Check if another program created same file
