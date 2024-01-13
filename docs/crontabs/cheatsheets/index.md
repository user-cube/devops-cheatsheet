---
title: Crontab Cheat Sheet
layout: home
nav_order: 1
parent: Crontabs
permalink: docs/crontab/cheatsheets/
last_modified_date: 2024-01-08
---

# Crontab Cheat Sheet

Here's a simple crontab cheat sheet to help you understand the syntax and use crontab effectively:

```bash
# ┌───────── minute (0 - 59)
# │ ┌─────── hour (0 - 23)
# │ │ ┌───── day of month (1 - 31)
# │ │ │ ┌─── month (1 - 12)
# │ │ │ │ ┌─ day of week (0 - 6, where 0 is Sunday)
# │ │ │ │ │
# * * * * * command to be executed

# Examples:

# Run a script every day at 3:30 AM
30 3 * * * /path/to/your/script.sh

# Run a command every Monday at 8:00 PM
0 20 * * 1 /path/to/your/command

# Run a command every hour
0 * * * * /path/to/your/command

# Run a script every weekday at 4:15 PM
15 16 * * 1-5 /path/to/your/script.sh

# Run a command every 15 minutes
*/15 * * * * /path/to/your/command

# Run a command every Sunday at midnight
0 0 * * 0 /path/to/your/command

# Run a script on the 1st day of every month at 2:30 AM
30 2 1 * * /path/to/your/script.sh

# Run a command every 6 hours
0 */6 * * * /path/to/your/command
```
Explanation:

- `*`: Wildcard, meaning "every" (e.g., every minute, every hour).
- `*/n`: Specifies intervals (e.g., every 15 minutes, every 6 hours).
- Specific numbers: For exact values (e.g., 1 for January, 0 for Sunday).
- `-`: Specifies a range (e.g., 1-5 for Monday to Friday).
- Commands or scripts: The actual task to be executed.

Feel free to customize the examples based on your specific scheduling needs. Always double-check your crontab entries, and consider testing commands outside of crontab before scheduling them.

![Crontab Cheat Sheet](https://user-cube.github.io/devops-cheatsheet/assets/images/crontabs/crontab_cheatsheet.png)