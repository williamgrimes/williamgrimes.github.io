{:title "Anacron Desktop Notifications"
 :layout :post
 :toc false
 :tags  ["anacron" "linux" "notification"]}

This is a short guide on creating custom scheduled Linux desktop notifications with `anacron` and `notify-send`. This system could be used to set reminders for tasks you intend to complete `@daily`, `@weekly`, `@monthly`, or `@yearly`, and can also display metrics you are interested to follow.

<div align="center">
    <img src="/img/notifications.png" alt="Notifications" style="width:60%">
</div>
<center><b>Caption: </b> linux desktop notifications scheduled daily.</center>
<p></p>

You could use this approach to send notifications for example:
 + to schedule a monthly reminder to pay a bill,
 + get a daily update on a stock price,
 + get daily statistics of covid cases in your area,
 + track the phase of the moon through a daily notification,
 + display a weekly metric of disk usage,
 + send a daily weather report notification.


## Schedulers
### Cron
On unix systems `cron` (from Chronos) is a valuable command-line utility for scheduling jobs and automating system maintenance. The `cron` utility is run as a daemon meaning it is a background process, not under the direct control of an interactive user.


``` shell
$ sudo service cron status
● cron.service - Regular background program processing daemon
     Loaded: loaded (/lib/systemd/system/cron.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2022-08-21 13:29:50 CEST; 1h 53min ago
       Docs: man:cron(8)
   Main PID: 965 (cron)
      Tasks: 1 (limit: 8991)
     Memory: 472.0K
        CPU: 152ms
     CGroup: /system.slice/cron.service
             └─965 /usr/sbin/cron -f -P
```

A crontab (cron table) file, defines the configuration specifying the schedule on which shell commands should run. A crontab file is a list of jobs to be run by the cron daemon, there is a system-wide crontab file at `/etc/crontab` and users may have their own crontab files in addition. A job may be specified for example running a backup script at 10:30 every Saturday morning:

``` shell
30 10 * * 5 /home/username/backup.sh
```

The downside of cron is that it assumes the system has constant up-time, in situations with intermittent up-time step in asynchronous cron also known as anacron.

### Anacron
For a personal machine that is not running continuously anacron  can be used, to control daily, weekly, and monthly jobs that could otherwise be controlled by cron. Anacron is a perfect tool for sending a daily linux notification, when the machine is running. The advantage being that jobs that are scheduled when the machine is not running will be run at the next available opportunity.

Anacron operates by checking whether a scheduled job has been executed in the last days specified in the period parameter. If the job has not been executed, anacron waits for the number of minutes specified in the delay field to elapse after which it runs the specified shell command or script. Each job that being executed is locked so that if there are any other copies of Anacron in the system, such tasks cannot be executed at the same time. Once the execution of the specified task or job completes, Anacron timestamps this and exits when there is no more scheduled jobs to be executed [[^1]]. For more information read the anacron manual page (`man anacron`) [[^2]].

The functionality to run anacron as non-root user is not as straightforward as with `cron`, and can be configured to run from the home directory [[^3]]. To send notifications as a non-root user to a users workspace I decided to use the default anacrontab  at `/etc/anacrontab`:

#### 1. Edit the `/etc/anacrontab`

``` shell
vim /etc/anacrontab
```

The contents of `/etc/anacrontab` are as follows

```shell
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/sbin:/bin:/usr/sbin:/usr/bin
# MAILTO=root
# RANDOM_DELAY=30
# Anacron jobs will start between 6am and 8am.
# START_HOURS_RANGE=6-8

# delay will be 1 minutes + RANDOM_DELAY for cron.daily
1         1    cron.daily          nice run-parts /etc/cron.daily
7         5    cron.weekly         nice run-parts /etc/cron.weekly
@monthly  15   cron.monthly        nice run-parts /etc/cron.monthly
```

Here you can specify new jobs by adding a new line, for example to run a backup script every two days with a delay of 35 minutes after anacron is initialised.

``` shell
2         35    backup         /home/user/backup
```
Jobs in anacron are specified with the following fields:

 + **period** specifies how frequently, in days the job should be executed. For a example, a value of 1 means the job should be run every day.
 + **delay** specifies a time in minutes between the when the anacron starts and when the job is executed, for example 2 minutes.
 + **job identifier** specifies a unique job ID. This is used in log messages to identify the jobs.
 + **command** specifies the command or the name of the script to be executed. If executing all scripts in a directory the `run-parts` command can be used.


#### 2. Add scripts to `/etc/cron.daily`, `/etc/cron.weekly`
In the `cron.daily` (or weekly, ...) folder you can add shell scripts that you want to be run each day (or week). A couple of notes:
 + the scripts should start with a shebang `#!/bin/sh`, not `/bin/bash`, and
 + scripts should be named without any extension e.g. `/etc/cron.daily/moon-phase`.

Rather than add scripts here I created a folder in my home directory `~/Notifications` and created symbolic links to `/etc/cron.daily` and `/etc/cron.weekly`.

### Desktop Notifications
---
To send linux  notifications of some metrics I'm interested to follow I use the `notify-send` command. This sends desktop notifications to the user via a notification daemon to inform the user about an event or display some form of information without getting in the user's way [[^4], [^5]].

Since it is not possible to execute anacron as a non-root user I configured my scripts to run as `su $USER -c <command>`, and specify the `DBUS_SESSION_BUS_ADDRESS`, an environment variable used by the dbus utility, required to start a message bus from a shell script.

#### Daily notification of Moon Phase in London
To get daily information about the phase of the moon I use the very nice console-oriented weather forecast service from [@igor_chubin](https://twitter.com/igor_chubin), available via curl [[^6]]. In the script I specify variables for the moon phase, day of the moon cycle, location and an update time and create a notification of this using `notify-send`.

``` shell
vim /etc/cron.daily/moon-phase
```
Containing the following:

``` shell
#!/bin/sh

USER=<username>

su $USER -c '
UPDATED=$(date "+%y/%m/%d %H:%M:%S")
LOCATION="London"

MOON_PHASE=$(curl --silent "wttr.in/${LOCATION}?format=%m")
MOON_DAY=$(curl --silent "wttr.in/${LOCATION}?format=%M")

DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus \
/usr/bin/notify-send "Moon in ${LOCATION}    ---   [updated at ${UPDATED}]" \
"Moon phase: ${MOON_PHASE} \nMoon Day: ${MOON_DAY}" \
--app-name=""
'
```

#### Daily notification of Covid Cases in Japan
To get daily information about covid cases in Japan I have used the corona stats online service [^7].

``` shell
vim /etc/cron.daily/covid
```
Containing the following:
``` shell
#!/bin/sh

USER=<username>

su $USER -c '
COUNTRY="Japan"

TODAY_CASES=$(curl --silent  "https://corona-stats.online/$COUNTRY?format=json" | jq ".data[].todayCases")
ACTIVE_PER_MILLION=$(curl --silent  "https://corona-stats.online/${COUNTRY}?format=json" | jq ".data[].activePerOneMillion")
UPDATED=$(curl --silent  "https://corona-stats.online/${COUNTRY}?format=json" | jq ".data[].updated" | date "+%y/%m/%d %H:%M:%S")

DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus \
/usr/bin/notify-send "Covid Cases ${COUNTRY}    ---   [updated at ${UPDATED}]" \
"New Cases: ${TODAY_CASES} \nActive per million ${ACTIVE_PER_MILLION} " \
--app-name=""
'
```

#### Weekly notification of Disk Usage
Finally, to get a weekly update on disk usage, I parsed the `df -h .` command to get information on the disk usage.

``` shell
$ vim /etc/cron.weekly/disk-usage
```
Containing the following:

``` shell
#!/bin/sh

USER=<username>

su $USER -c '
UPDATED=$(date "+%y/%m/%d %H:%M:%S")

DISK_FILESYSTEM=$(df -h . --output=source | tail -1)
DISK_SIZE=$(df -h . --output=size | tail -1 | sed "s|[^0-9]||g")
DISK_USED=$(df -h . --output=used | tail -1 | sed "s|[^0-9]||g")
DISK_AVAILABLE=$(df -h . --output=avail | tail -1 | sed "s|[^0-9]||g")

DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus \
/usr/bin/notify-send "${DISK_FILESYSTEM}    ---   [updated at ${UPDATED}]" \
"${DISK_USED} / ${DISK_SIZE} G disk used, available ${DISK_AVAILABLE} G" \
--app-name=""
'
```

## Conclusion
This guide describes how to setup daily and weekly linux notifications for information that you may find relevant. It is easy to continue to add more scripts and extend this further by adding to the `cron.daily` directory.

In future I would also like to add some conditional notifications, depending on how reliable and useful this system turns out to be. For example you could have a script that sends a notification when it is the day of the full moon only, or when a stock drops below a certain price, or when covid cases fall below a certain level, or when disk usage is more than 80 %. It would also be useful to combine these conditional notifications with the option to send an email [[^8]].

## References
[^1]: [kifarunix: scheduling tasks using anacron in linux](https://kifarunix.com/scheduling-tasks-using-anacron-in-linux-unix/)
[^2]: [linux-die: anacron manual page](https://linux.die.net/man/8/anacron)
[^3]: [grinux: run anacron as user](https://grinux.wordpress.com/2012/04/18/run-anacron-as-user/)
[^4]: [thegeekstuff: Ubuntu notify send](https://www.thegeekstuff.com/2010/12/ubuntu-notify-send/)
[^5]: [manpage: notify send](https://manpages.ubuntu.com/manpages/xenial/man1/notify-send.1.html)
[^6]: [github: wttr](https://github.com/chubin/wttr.in)
[^7]: [corona stats online](https://corona-stats.online)
[^8]: [fedingo: - shell script to check disk space and send email alerts](https://fedingo.com/shell-script-to-check-disk-space-and-send-email-alerts/)
