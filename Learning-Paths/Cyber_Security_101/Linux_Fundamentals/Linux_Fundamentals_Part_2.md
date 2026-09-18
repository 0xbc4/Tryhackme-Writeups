# Linux Fundamentals Part 2

- TryHackMe: [Linux Fundamentals Part 2](https://tryhackme.com/room/linuxfundamentalspart2)
- Difficulty: Info
- Access: Premium room
- Estimated time: 20 minutes
- Topics: `SSH`, `Linux flags`, `filesystem`, `permissions`, `common directories`

![Linux Fundamentals Part 2 room icon](../../../assets/room-icons/linux-fundamentals-part-2.png)

Room icon source: [TryHackMe CDN](https://cdn-images.tryhackme.com/room-icons/linuxfundamentalspart2-1785241447270.png)

> This room is a continuation of Linux Fundamentals Part 1. Use the commands only on an authorized TryHackMe machine.

## Objective

Part 2 continues the Linux journey with remote access over SSH, command flags and switches, filesystem operations, Linux permissions, and important system directories.

## Accessing Linux over SSH

SSH provides an encrypted remote terminal session. The general syntax is:

```bash
ssh username@target-ip
```

For a non-standard SSH port, use `-p`:

```bash
ssh -p 2222 username@target-ip
```

The first connection may ask you to confirm the server fingerprint. Verify the fingerprint through a trusted channel before accepting it in a real environment.

Useful SSH options include:

| Option | Purpose |
| --- | --- |
| `-p` | Connect to a specific port |
| `-i` | Use a private key file |
| `-v` | Enable verbose troubleshooting output |
| `-o` | Set an SSH configuration option |

Never share private keys or passwords in a writeup.

## Flags and switches

Many Linux commands change their behavior through flags. The short form usually uses one dash, while a long option uses two dashes:

```bash
ls -l
ls --all
ls -la
```

Use built-in help and manual pages to discover options:

```bash
command --help
man command
```

Examples:

```bash
ls --help
man ssh
man chmod
```

The exact output can vary slightly between distributions and command versions, so use the machine’s local documentation as the source of truth.

## Filesystem interaction

Part 2 extends the navigation commands from Part 1 with file and directory management:

```bash
pwd
ls -la
mkdir reports
touch notes.txt
cp notes.txt reports/
mv notes.txt reports/notes-old.txt
rm reports/notes-old.txt
rmdir reports
```

Important cautions:

- `rm` permanently removes files and does not use a recycle bin.
- `rm -r` can remove an entire directory tree.
- Confirm the current path with `pwd` before destructive commands.
- Use absolute paths carefully when operating as an administrator.

Useful inspection commands include:

```bash
file sample.bin
head -n 10 access.log
tail -n 10 access.log
wc -l access.log
```

## Permissions 101

Linux permissions are assigned to three classes:

1. **User**: The file owner.
2. **Group**: Users belonging to the file’s group.
3. **Others**: Everyone else.

The three basic permissions are:

- `r`: Read
- `w`: Write
- `x`: Execute

Inspect permissions with:

```bash
ls -l script.sh
```

Example output:

```text
-rwxr-x--- 1 alice analysts 120 Sep 18 12:00 script.sh
```

This means the owner can read, write, and execute; the group can read and execute; and others have no access.

### Numeric permissions

Permissions can also be represented numerically:

| Permission | Value |
| --- | ---: |
| Read | 4 |
| Write | 2 |
| Execute | 1 |

For example, `755` means:

- Owner: `7` (`rwx`)
- Group: `5` (`r-x`)
- Others: `5` (`r-x`)

Change permissions with `chmod`:

```bash
chmod 755 script.sh
chmod u+x script.sh
chmod o-r sensitive.txt
```

Change ownership with `chown` when authorized:

```bash
sudo chown username:group file.txt
```

Avoid giving files broader permissions than necessary. In particular, do not use `chmod 777` as a generic fix.

## Common directories

| Directory | Typical purpose |
| --- | --- |
| `/home` | Personal directories for regular users |
| `/root` | Home directory for the root user |
| `/etc` | System-wide configuration files |
| `/var` | Variable data such as logs and caches |
| `/tmp` | Temporary files |
| `/usr` | User-space applications and shared data |
| `/bin` | Essential user command binaries |
| `/sbin` | Essential system administration binaries |
| `/opt` | Optional or third-party software |
| `/dev` | Device files |
| `/proc` | Kernel and process information interface |
| `/sys` | Kernel and device information interface |

Explore directories safely with:

```bash
ls -la /etc
ls -la /var/log
```

Do not modify system files unless the exercise explicitly requires it.

## Practical workflow

A safe workflow for this room is:

1. Start the authorized lab machine or AttackBox.
2. Record the target IP and SSH port.
3. Connect with `ssh username@target-ip`.
4. Confirm the account and location with `whoami` and `pwd`.
5. Use `--help` or `man` before unfamiliar flags.
6. Inspect permissions with `ls -l`.
7. Practice file operations in a temporary directory.
8. Terminate the machine when finished.

## Answer notes

This room is Premium and its question values may depend on the deployed machine. Verify machine-specific answers directly in the room rather than copying values from another session.

Stable command reference:

| Task | Command or concept |
| --- | --- |
| SSH login | `ssh username@target-ip` |
| Custom SSH port | `ssh -p PORT username@target-ip` |
| Command help | `command --help` |
| Manual page | `man command` |
| Show permissions | `ls -l` |
| Change permissions | `chmod MODE file` |
| Change owner | `chown user:group file` |
| Current path | `pwd` |
| Temporary workspace | `/tmp` |
| System configuration | `/etc` |
| System logs | `/var/log` |

## Conclusion

Linux Fundamentals Part 2 builds on basic terminal navigation by introducing remote access, command documentation, filesystem management, permission models, and the layout of a Linux system. These concepts are essential for both offensive and defensive security work.
