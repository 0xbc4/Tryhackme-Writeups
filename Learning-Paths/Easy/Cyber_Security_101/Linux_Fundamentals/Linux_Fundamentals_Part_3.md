# Linux Fundamentals Part 3

- TryHackMe: [Linux Fundamentals Part 3](https://tryhackme.com/room/linuxfundamentalspart3)
- Difficulty: Info
- Access: Premium room
- Estimated time: 18 minutes
- Topics: `text editors`, `Linux utilities`, `processes`, `cron`, `package management`, `logs`

![Linux Fundamentals Part 3 room icon](../../../../assets/room-icons/linux-fundamentals-part-3.png)

Room icon source: [TryHackMe CDN](https://cdn-images.tryhackme.com/room-icons/linuxfundamentalspart3-1785241447458.png)

> This room is a continuation of Linux Fundamentals Parts 1 and 2. Use the commands only on an authorized TryHackMe machine.

## Objective

Part 3 focuses on utilities used in day-to-day Linux administration and security work. It introduces terminal text editors, file transfer and search utilities, process management, scheduled tasks, package management, and system logs.

## Terminal text editors

Linux systems commonly provide terminal-based editors. Two examples are `nano` and `Vim`.

Open a file with Nano:

```bash
nano notes.txt
```

Useful Nano shortcuts:

| Shortcut | Action |
| --- | --- |
| `Ctrl + O` | Write or save the file |
| `Ctrl + X` | Exit Nano |
| `Ctrl + W` | Search within the file |
| `Ctrl + K` | Cut the current line |
| `Ctrl + U` | Paste a cut line |
|

Open a file with Vim:

```bash
vim notes.txt
```

Vim starts in normal mode. Common actions include:

- `i`: Enter insert mode.
- `Esc`: Return to normal mode.
- `:w`: Save the file.
- `:q`: Quit.
- `:wq`: Save and quit.
- `:q!`: Quit without saving.

Be careful with editors opened as root. A file saved with elevated privileges may change ownership or overwrite important system configuration.

## General and useful utilities

### Download and transfer data

`wget` downloads a resource from a URL:

```bash
wget https://example.com/file.txt
```

`curl` can retrieve URLs and is useful for testing HTTP services:

```bash
curl https://example.com
curl -I https://example.com
```

Use these commands only with systems and URLs you are authorized to access.

### File inspection and searching

```bash
file sample.bin
wc -l access.log
sort names.txt
uniq names.txt
strings suspicious.bin
```

Search command output with a pipe:

```bash
ps aux | grep ssh
```

Search for a file by name:

```bash
find /home/tryhackme -name '*.txt'
```

Read documentation before using unfamiliar options:

```bash
command --help
man command
```

## Processes 101

A process is a running instance of a program. Every process has a process ID, or PID.

List processes:

```bash
ps
ps aux
```

Monitor processes interactively:

```bash
top
```

Find a process by name:

```bash
pgrep process-name
ps aux | grep process-name
```

Stop a process by PID:

```bash
kill PID
```

If a process does not respond to a normal termination signal, a stronger signal may be used as a last resort:

```bash
kill -9 PID
```

Use `kill -9` carefully because it does not allow the process to clean up gracefully.

### Foreground and background jobs

Run a command in the background:

```bash
long_running_command &
```

Suspend a foreground process with `Ctrl + Z`, then resume it in the background:

```bash
bg
```

Bring the most recent background job to the foreground:

```bash
fg
```

List shell jobs:

```bash
jobs
```

## Automation with cron

Cron schedules commands to run automatically. User cron entries can be viewed with:

```bash
crontab -l
```

Edit the current user’s cron table with:

```bash
crontab -e
```

A cron schedule has five time fields followed by the command:

```text
minute hour day-of-month month day-of-week command
```

Example:

```text
*/5 * * * * /home/tryhackme/check.sh
```

This runs the script every five minutes. The cron service and system-wide schedules may be stored in locations such as:

```text
/etc/crontab
/etc/cron.d/
/etc/cron.hourly/
/etc/cron.daily/
/etc/cron.weekly/
```

When investigating scheduled tasks, inspect the command, owner, file permissions, and referenced paths. Do not create persistence on systems you do not own or administer.

## Package management

Ubuntu and Debian systems commonly use APT to manage packages.

Update the local package index:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install a package:

```bash
sudo apt install package-name
```

Remove a package:

```bash
sudo apt remove package-name
```

Search for a package:

```bash
apt search package-name
```

The package index should be refreshed before installing software when practical. Review package names and repository sources before granting administrative privileges.

## Logs

Logs record activity from the operating system, services, and applications. Common locations include:

```text
/var/log/
```

Useful commands for reading logs:

```bash
ls -lah /var/log
cat /var/log/syslog
less /var/log/auth.log
tail -f /var/log/syslog
grep -i "failed" /var/log/auth.log
```

`journalctl` reads logs collected by systemd:

```bash
journalctl
journalctl -u ssh
journalctl --since "1 hour ago"
```

When investigating an event, record timestamps, usernames, source addresses, process names, and related services. Preserve the original evidence and avoid editing logs.

## Answer notes

This room is Premium and its question values may depend on the deployed machine or the exact task content. Verify room-specific answers directly in TryHackMe rather than copying values from another session.

Stable command reference:

| Topic | Command or concept |
| --- | --- |
| Terminal editor | `nano file.txt` or `vim file.txt` |
| Download a file | `wget URL` |
| HTTP request | `curl URL` |
| List processes | `ps aux` |
| Process monitor | `top` |
| Stop a process | `kill PID` |
| List cron entries | `crontab -l` |
| Update packages | `sudo apt update` |
| Install a package | `sudo apt install package-name` |
| System logs | `/var/log/` and `journalctl` |

## Conclusion

Part 3 completes the introductory Linux series by connecting everyday administration tasks with security work. Editors, utilities, process tools, cron, APT, and logs are all useful when troubleshooting systems, investigating activity, and maintaining a Linux machine.
