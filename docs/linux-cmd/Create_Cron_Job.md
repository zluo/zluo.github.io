---
layout: default
title: Cron Jobs
nav_order: 2
parent: Linux Command
---

## How to create a cron job in linux

cron service check files in:
    
    /etc/crontab
    /etc/cron.*
    /var/spool/cron/crontab/{user}

### List cron job

    crontab -l

### Create a cron job

    crontab -e

### Cron job format

    1 2 3 4 5 path/to/command>/dev/null 2>&1

1. Minute (0 - 59)
2. Hour (0 - 23)
3. Day of month (1 - 31)
4. Month (1 - 12)
5. Day of week (0 - 7) (Sunday=0 or 7)

### Examples

. To run /path/to/command five minutes after midnight, every day, enter:

    5 0 * * * /path/to/command

. Run /path/to/script.sh at 2:15pm on the first of every month, enter:

    15 14 1 * * /path/to/script.sh

. Run /scripts/phpscript.php at 10 pm on weekdays, enter:

    0 22 * * 1-5 /scripts/phpscript.php

. Run /root/scripts/perl/perlscript.pl at 23 minutes after midnight, 2am, 4am …, everyday, enter:

    23 0-23/2 * * * /root/scripts/perl/perlscript.pl

. Run /path/to/unixcommand at 5 after 4 every Sunday, enter:

    5 4 * * sun /path/to/unixcommand

### operators

An operator specify multiple values in a field. There are 4 operators:

   . Asterisk (*) : specifies all possible values for a field.
   . Comma (,) : specifies a list of values, for example: “1,5,10”.
   . Dash (-) : specifies a range of values, for example: “5-15”.
   . Separator (/) : specifies a step value, for example: */2 means every 2 hours.

### ShortCut

@reboot	Run once, at startup.
@yearly	Run once a year, “0 0 1 1 *”.
@annually	(same as @yearly)
@monthly	Run once a month, “0 0 1 * *”.
@weekly	Run once a week, “0 0 * * 0”.
@daily	Run once a day, “0 0 * * *”.
@midnight	(same as @daily)
@hourly	Run once an hour, “0 * * * *”.

### Cron logs
    . Centos

        cat /var/log/cron

    . Moden Linux distro

    sudo systemctl status cron
    sudo journalctl -u cron
    sudo journalctl -u cron | grep backup-script.sh
