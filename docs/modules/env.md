# Environment Variables

Manages user-level environment variables 
for your Windows environment.

**YAML Key:** `envVars`

**Properties:**

- `variable` : The name of the environment variable.
- `value` : The value to set.
- `action` : (Optional) `set` (default) or `append`. 
  `append` adds the value to a path-like variable.

---

## Basic Usage

```yaml
envVars:
  - variable: GOPATH
    value: "%USERPROFILE%\\go"
  - variable: Path
    value: "%USERPROFILE%\\go\\bin"
    action: append
```

---

## Advanced Configuration

### Profile-Specific Variables

Profile-specific environment variables can be 
declared under `profiles.<name>.envVars`. When 
that profile is selected with `--profile`, `set` 
entries replace matching top-level variables, 
while `append` entries add profile-only path segments.

```yaml
envVars:
  - variable: EDITOR
    value: nvim
    action: set

profiles:
  work:
    envVars:
      - variable: EDITOR
        value: code
        action: set
      - variable: Path
        value: "%USERPROFILE%\\work\\bin"
        action: append
```

---

## Real-World config.yaml Examples

### Example 1 — Developer Setup

```yaml
envVars:
  - variable: JAVA_HOME
    value: "C:\\Program Files\\Java\\jdk-17"
    action: set
  - variable: Path
    value: "C:\\Program Files\\Java\\jdk-17\\bin"
    action: append
  - variable: NODE_ENV
    value: development
    action: set
```

### Example 2 — Python Developer Setup

```yaml
envVars:
  - variable: PYTHONPATH
    value: "C:\\Python311"
    action: set
  - variable: Path
    value: "C:\\Python311\\Scripts"
    action: append
  - variable: PIP_DEFAULT_TIMEOUT
    value: "100"
    action: set
```

### Example 3 — Work Profile Setup

```yaml
envVars:
  - variable: EDITOR
    value: nvim
    action: set

profiles:
  work:
    envVars:
      - variable: EDITOR
        value: code
        action: set
      - variable: PROXY_URL
        value: "http://proxy.company.com"
        action: set
      - variable: Path
        value: "%USERPROFILE%\\work\\bin"
        action: append
```

### Example 4 — Minimal Setup

```yaml
envVars:
  - variable: MY_PROJECT
    value: "C:\\Projects"
    action: set
```

---

## Troubleshooting

**Issue: Variable not found after setting**
- Restart terminal after setting variables
- Log out and log back in for system variables
- Run `echo %MY_VAR%` in terminal to verify

**Issue: Path variable not updating**
- Use `action: append` to add to PATH
- Use `action: set` to replace PATH value
- Restart terminal to see PATH changes

**Issue: Profile variables not applying**
- Make sure to use `--profile` flag
- Check profile name matches config
- Verify profile section indentation