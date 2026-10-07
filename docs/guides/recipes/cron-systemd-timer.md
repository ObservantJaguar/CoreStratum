---
title: Schedule a Task with cron/systemd-timer
parent: Recipes
grand_parent: Guides
---

# Schedule a Task with cron/systemd-timer

## Goal

Run a script on a fixed schedule (classic cron), or with systemd timers for better control and logging.

## Task

Run `/path/to/script.sh` every day at 02:00.

## Steps

### Option A - cron

1. Open the crontab editor:

```bash
crontab -e
```

2. Add the schedule line (minute hour day-of-month month day-of-week):

```cron
0 2 * * * /path/to/script.sh
```

3. Save and exit. The job is now active.

### Option B - systemd timer

1. Create a service unit `/etc/systemd/system/script.service`:

```ini
[Unit]
Description=Daily script

[Service]
Type=oneshot
ExecStart=/path/to/script.sh
```

2. Create a timer unit `/etc/systemd/system/script.timer`:

```ini
[Unit]
Description=Run daily script at 02:00

[Timer]
OnCalendar=*-*-* 02:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

3. Enable and start the timer:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now script.timer
```

## Verification

- Cron: the job is listed:

```bash
crontab -l
```

- systemd: the timer is active and shows the next run:

```bash
systemctl list-timers script.timer
sudo journalctl -u script.service
```

## Gotchas

- **cron uses a minimal `PATH`** - `script.sh` will not find `/usr/local/bin` tools unless you write absolute paths or set `PATH=...` at the top of the crontab. Always use absolute paths for the script and its dependencies.
- **Silent failures** - cron sends output only to the local mail spool, which is often unread. Redirect the script log: `... && /path/script.sh >> /var/log/script.log 2>&1`.
- **Missed runs after downtime** - with a timer, `Persistent=true` runs the task immediately after boot if it was missed while the machine was off; cron simply skips the missed run. Choose per your needs.
- **`Type=oneshot`** - without it the service exits "successfully" the moment it is started and the timer result may be misleading; for a plain script use `oneshot`.

## Related

- [Processes and scheduling](../../foundations/standards/index.md)
- [Systemd units](../../operating-systems/linux/index.md)