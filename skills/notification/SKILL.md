---
name: notification
description: Guide for sending notification to desktop. Use this when you need attention of human.
argument-hint: Message and title to send
user-invocable: true
---

Sending notification
====================

This skill must be used when an agent needs human attention.
Typical cases:
  - Long-running task completed
  - User input required
  - Error occurs and human intervention is needed
  - Important event happens that user should be aware of

How to send notification
========================

The notification is OS dependent. Follow the instructions below to send appropriately.

Mac

Use `osascript` command with `-e` option. Example:

```shell
osascript -e 'display notification "{message}" with title "{title}" sound name "{sound}"'
```

The `{sound}` argument can be one of:

- `Basso`   # critical alert
- `Funk`    # normal alert
- `Glass`   # low urgency alert

Example:
```shell
osascript -e 'display notification "Your attention is needed" with title "Attention" sound name "Funk"'
```

Linux

Use `notify-send` command.

```shell
notify-send "{message}"
```

Use `-u` option to set urgency:

- `low`
- `normal`
- `critical`

Example:
```shell
notify-send -u critical "Build failed: immediate attention required"
```

If `notify-send` is not installed, use `echo` as fallback and suggest installing `libnotify-bin`.

Windows

Use `New-BurntToastNotification` from PowerShell.

```shell
powershell -Command "New-BurntToastNotification -Text '{message}' -Sound '{sound}'"
```

The `{sound}` can be one of:

- `Default`
- `IM`
- `Mail`
- `Reminder`
- `SMS`

Example:
```shell
powershell -Command "New-BurntToastNotification -Text 'Task completed' -Sound 'IM'"
```

Urgency mapping
---------------
| Situation           | Mac Sound | Linux Urgency | Windows Sound |
|---------------------|-----------|--------------|---------------|
| Critical error      | Basso     | critical     | Reminder      |
| Normal alert        | Funk      | normal       | IM            |
| Low urgency/info    | Glass     | low          | Default       |

Return value handling
---------------------
Check exit codes after sending notifications to ensure delivery.
