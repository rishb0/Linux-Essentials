# Systemd Timers in Linux

Systemd timers are a modern replacement for traditional cron jobs in Linux. They are used to schedule tasks to run at specific times or intervals using `systemd`, which is the default init system in many Linux distributions.

## 1. Overview of Systemd Timers

A systemd timer consists of two main components:

1. **Timer Unit (`.timer`)** – Defines when the job should run.
2. **Service Unit (`.service`)** – Defines what should be executed.

Timers provide more flexibility than cron, such as:

- Better logging and tracking via `journalctl`
- Ability to run jobs immediately after boot
- Randomized delays to avoid system overload

## 2. Creating a Systemd Timer

### Step 1: Create a Service Unit

A service unit defines the actual task that will be executed.

Example file: `/etc/systemd/system/myjob.service`

```ini
[Unit]
Description=My Scheduled Job
```

```ini
[Service]
Type=oneshot
ExecStart=/usr/bin/bash -c "echo 'Hello, world!' > /tmp/hello.txt"
```

- `Type=oneshot` means the task runs once and exits.

### Step 2: Create a Timer Unit

A timer unit determines when the service should be executed.

Example file: `/etc/systemd/system/myjob.timer`

```ini
[Unit]
Description=Run My Scheduled Job Every 5 Minutes
```

```ini
[Timer]
OnBootSec=1min
```

```ini
[Timer]
OnUnitActiveSec=5min
```

```ini
[Timer]
Unit=myjob.service
```

```ini
[Install]
WantedBy=timers.target
```

- `OnBootSec=1min` — Runs the job 1 minute after boot.
- `OnUnitActiveSec=5min` — Runs every 5 minutes after that.
- `Unit=myjob.service` — Specifies the service to run.

## 3. Enabling and Managing the Timer

### Enable and Start the Timer

Reload the systemd configuration:

```bash
systemctl daemon-reload
```

Enable and start the timer immediately:

```bash
systemctl enable myjob.timer --now
```

### Check Timer Status

List all timers:

```bash
systemctl list-timers --all
```

Check the status of the timer:

```bash
systemctl status myjob.timer
```

### Manually Trigger the Job

Start the service manually:

```bash
systemctl start myjob.service
```

### Disable and Remove the Timer

Stop the timer:

```bash
systemctl stop myjob.timer
```

Disable the timer:

```bash
systemctl disable myjob.timer
```

Remove the timer and service unit files:

```bash
rm /etc/systemd/system/myjob.timer
```

```bash
rm /etc/systemd/system/myjob.service
```

Reload the systemd configuration:

```bash
systemctl daemon-reload
```

## 4. Alternative Scheduling Options

Instead of `OnUnitActiveSec`, you can use:

- `OnCalendar=daily` — Runs once a day.
- `OnCalendar=Mon * * 12:00:00` — Runs every Monday at 12:00 PM.
- `OnCalendar=* * * 03:15:00` — Runs daily at 3:15 AM.

**Example Timer:**

```ini
[Timer]
OnCalendar=* * * 03:15:00
```

```ini
[Timer]
Persistent=true
```

- `Persistent=true` ensures missed executions (e.g., during a reboot) are run immediately after the system starts.

## 5. Viewing Logs

Check logs for the service:

```bash
journalctl -u myjob.service --no-pager
```

## 6. Why Use Systemd Timers Over Cron?

| Feature           | Cron Jobs         | Systemd Timers                                |
|-------------------|-------------------|-----------------------------------------------|
| **Logging**       | Limited           | Full (`journalctl` logs)                      |
| **Start at Boot** | No                | Yes                                           |
| **Flexibility**   | Fixed intervals   | More options (randomized delays, boot timers) |
| **Failure Handling** | No built-in retry | Can retry failed jobs                         |

Systemd timers are more powerful and integrate better with system logging and startup processes, making them a superior choice for many automated tasks.

------------------------------------------------------------
