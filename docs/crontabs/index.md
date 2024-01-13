---
title: Crontabs
layout: home
nav_order: 4
has_children: true
permalink: docs/crontab
last_modified_date: 2024-01-08
---

# Crontabs

Crontab is a time-based job scheduler in Unix-like operating systems. It allows users to schedule tasks (commands or scripts) to run periodically at fixed times, dates, or intervals. Each user on a system can have their own crontab file, which lists the scheduled tasks for that user.

Here's a basic overview of how crontab works:

## Editing Crontab

To edit your crontab file, you can use the following command:
```bash
crontab -e
```

This command opens the crontab file in the default text editor (often vi or nano).

## Crontab Syntax:

Each line in the crontab file represents a scheduled task and follows the following format:
```bash
m h dom mon dow command
```
- **m**: Minute (0 - 59)
- **h**: Hour (0 - 23)
- **dom**: Day of the month (1 - 31)
- **mon**: Month (1 - 12)
- **dow**: Day of the week (0 - 6, where 0 is Sunday)
- **command**: The command or script to be executed.

# Examples

To run a script every day at 3:30 AM:

```bash
30 3 * * * /path/to/your/script.sh
```

To run a command every Monday at 8:00 PM:

```bash
0 20 * * 1 /path/to/your/command
```

To run a command every hour:

```bash
0 * * * * /path/to/your/command
```

## Viewing Crontab:

To view your crontab entries, use the following command:
```bash
crontab -l
```

## Removing Crontab:

To remove all your crontab entries, use the following command:
```bash
crontab -r
```

**Note**: Exercise caution when editing crontab files, as incorrect entries can lead to unexpected behavior. It's a good practice to test your commands outside of crontab before scheduling them.

Keep in mind that the specific syntax and available features may vary slightly depending on the operating system and version.
