# Scheduled Tasks

Configures scheduled tasks on Windows using 
the Task Scheduler. This module automates 
repetitive tasks on a defined schedule.

**YAML Key:** `scheduled_tasks`

**Properties:**

- `name` : The name of the task.
- `description` : A description for the task.
- `author` : The author of the task.
- `path` : The path for the task definition.
- `triggers` : A list of triggers for the task.
- `actions` : A list of actions for the task.

---

## Basic Usage

```yaml
scheduled_tasks:
  - name: "My Daily Task"
    description: "Runs a script every day."
    author: "WinHome"
    path: "\\MyTasks\\DailyScript"
    triggers:
      - type: "daily"
        startBoundary: "2026-01-01T08:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\myscript.bat"
```

---

## Advanced Configuration

### Multiple Triggers

```yaml
scheduled_tasks:
  - name: "MultiTriggerTask"
    description: "Runs on multiple schedules."
    author: "WinHome"
    path: "\\MyTasks\\MultiTrigger"
    triggers:
      - type: "daily"
        startBoundary: "2026-01-01T08:00:00"
      - type: "weekly"
        startBoundary: "2026-01-01T09:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\task.bat"
```

---

## Real-World config.yaml Examples

### Example 1 — Daily Backup Task

```yaml
scheduled_tasks:
  - name: "DailyBackup"
    description: "Backs up important files daily."
    author: "WinHome"
    path: "\\MyTasks\\DailyBackup"
    triggers:
      - type: "daily"
        startBoundary: "2026-01-01T02:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\backup.bat"
```

### Example 2 — Weekly System Cleanup

```yaml
scheduled_tasks:
  - name: "WeeklyCleanup"
    description: "Cleans temp files every week."
    author: "WinHome"
    path: "\\MyTasks\\WeeklyCleanup"
    triggers:
      - type: "weekly"
        startBoundary: "2026-01-01T03:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\cleanup.bat"
```

### Example 3 — Startup Task

```yaml
scheduled_tasks:
  - name: "StartupScript"
    description: "Runs script on system startup."
    author: "WinHome"
    path: "\\MyTasks\\Startup"
    triggers:
      - type: "boot"
        startBoundary: "2026-01-01T00:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\startup.bat"
```

### Example 4 — Multiple Tasks

```yaml
scheduled_tasks:
  - name: "DailyBackup"
    description: "Daily backup task."
    author: "WinHome"
    path: "\\MyTasks\\DailyBackup"
    triggers:
      - type: "daily"
        startBoundary: "2026-01-01T02:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\backup.bat"
  - name: "WeeklyCleanup"
    description: "Weekly cleanup task."
    author: "WinHome"
    path: "\\MyTasks\\WeeklyCleanup"
    triggers:
      - type: "weekly"
        startBoundary: "2026-01-01T03:00:00"
    actions:
      - type: "exec"
        path: "C:\\scripts\\cleanup.bat"
```

---

## Troubleshooting

**Issue: Task not appearing in Task Scheduler**
- Make sure WinHome is run as Administrator
- Check the path value is correct
- Open Task Scheduler to verify task exists

**Issue: Task not running at scheduled time**
- Check trigger startBoundary date format
- Make sure system clock is correct
- Verify task is enabled in Task Scheduler

**Issue: Action script not found**
- Use full path for script location
- Make sure script file exists
- Check for typos in path value
