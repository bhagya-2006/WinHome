# Registry Tweaks

Applies Windows Registry tweaks to configure system settings and preferences.

**YAML Key:** `registry`

**Properties:**

- `path` : The registry key path (e.g., `HKCU\\Software\\...`).
- `name` : The value name.
- `value` : The value to set.
- `type` : `string` (default), `dword`, `qword`, or `binary`.

---

## Basic Usage

```yaml
registry:
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: HideFileExt
    value: 0
    type: dword
```

---

## Advanced Configuration

### Multiple Registry Tweaks

```yaml
registry:
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: HideFileExt
    value: 0
    type: dword
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Themes\Personalize
    name: AppsUseLightTheme
    value: 0
    type: dword
```

---

## Real-World config.yaml Examples

### Example 1 — Show File Extensions

```yaml
registry:
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: HideFileExt
    value: 0
    type: dword
```

### Example 2 — Enable Dark Mode

```yaml
registry:
  - path: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Themes\Personalize
    name: AppsUseLightTheme
    value: 0
    type: dword
  - path: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Themes\Personalize
    name: SystemUsesLightTheme
    value: 0
    type: dword
```

### Example 3 — Developer Settings

```yaml
registry:
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: HideFileExt
    value: 0
    type: dword
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: Hidden
    value: 1
    type: dword
```

### Example 4 — Complete System Setup

```yaml
registry:
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: HideFileExt
    value: 0
    type: dword
  - path: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Themes\Personalize
    name: AppsUseLightTheme
    value: 0
    type: dword
  - path: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
    name: Hidden
    value: 1
    type: dword
```

---

## Troubleshooting

**Issue: Registry key not found**

- Check if path is correct
- Open Registry Editor (`regedit`) to verify
- Make sure path uses correct hive (HKCU/HKLM)

**Issue: Access denied**

- Run WinHome as Administrator
- Some HKLM keys require system privileges
- Check key permissions in Registry Editor

**Issue: Wrong value type**

- Use `dword` for numbers (0, 1)
- Use `string` for text values
- Use `qword` for large numbers
- Check existing value type in Registry Editor
