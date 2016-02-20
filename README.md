plexWatch - 0.3.2 (2014-11-19)
=========
***Notify*** and Log ***'Now Playing'*** and ***'Watched'*** content from a Plex Media Server + ***'Recently Added'*** (...and more)

[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CHRZ55VCAJSYG)


** windows and linux codebase has been fully merged **

----------------

### Need Help?
* Linux Forum: http://forums.plexapp.com/index.php/topic/72552-plexwatch-plex-notify-script-send-push-alerts-on-new-sessions-and-stopped/
* Windows Forum: http://forums.plexapp.com/index.php/topic/79616-plexwatch-windows-branch/

### Want a frontend? ***plexWatch/Web***
*  Download: https://github.com/ecleese/plexWatchWeb
*    Forums: http://forums.plexapp.com/index.php/topic/82819-plexwatchweb-a-web-front-end-for-plexwatch/

----------------

### Read More about plexWatch

**What it does**
* backed by a SQLite DB (for state and history)
* CLI to query watched videos, videos being watched and stats on time watched per user
* Limit output per user or exclude users
* ...more to come

### Getting a list of watched shows

* This will only work for shows this has already notified on.

#####  list all watched shows - no limit

```
/opt/plexWatch/plexWatch.pl --watched
======================================== Watched ========================================
Date Range: Anytime through Now

User: jimbo
 Wed Jun 26 15:56:09 2013: jimbo watched: South Park - A Nightmare on FaceTime [duration: 22 minutes, and 15 seconds]
 Wed Jun 26 20:18:34 2013: jimbo watched: The Following - Whips and Regret [duration: 46 minutes, and 45 seconds]
 Wed Jun 26 20:55:02 2013: jimbo watched: The Following - The Curse [duration: 46 minutes, and 15 seconds]

User: carrie
 Wed Jun 24 08:55:02 2013: carrie watched: The Following - The Curse [duration: 46 minutes, and 25 seconds]
 Wed Jun 26 20:19:48 2013: carrie watched: Dumb and Dumber [1994] [PG-13] [duration: 1 hour, 7 minutes, and 10 seconds]
```

##### list watched shows - limit by TODAY only

```
/opt/plexWatch/plexWatch.pl --watched --start=today --start=tomorrow

======================================== Watched ========================================
Date Range: Fri Jun 28 00:00:00 2013 through Sat Jun 29 00:00:00 2013

User: jimbo
Fri Jun 28 09:18:22 2013: jimbo watched: Married ... with Children - Mr. Empty Pants [duration: 1 hour, 23 minutes, and 20 seconds]
```

##### list watched shows - limit by a start and stop date

```
/opt/plexWatch/plexWatch.pl --watched --start="2 days ago" --stop="1 day ago"

======================================== Watched ========================================
Date Range: Fri Jun 26 00:00:00 2013 through Thu Jun 27 00:00:00 2013

 User: Jimbo
  Wed Jun 26 15:56:09 2013: rarflix watched: South Park - A Nightmare on FaceTime [duration: 22 minutes, and 15 seconds]
  Wed Jun 26 20:18:34 2013: rarflix watched: The Following - Whips and Regret [duration: 46 minutes, and 45 seconds]
  Wed Jun 26 20:55:02 2013: rarflix watched: The Following - The Curse [duration: 46 minutes, and 15 seconds]

 User: Carrie
  Wed Jun 26 20:19:48 2013: Carrie watched: Dumb and Dumber [1994] [PG-13] [duration: 1 hour, 7 minutes, and 10 seconds]
```

#### list watched shows: option --nogrouping vs default

#####  with --nogrouping
```
 Sun Jun 30 15:12:01 2013: exampleUser watched: Your Highness [2011] [R] [duration: 27 minutes and 54 seconds]
 Sun Jun 30 15:41:02 2013: exampleUser watched: Your Highness [2011] [R] [duration: 4 minutes and 59 seconds]
 Sun Jun 30 15:46:02 2013: exampleUser watched: Star Trek [2009] [PG-13] [duration: 24 minutes and 17 seconds]
 Sun Jun 30 17:48:01 2013: exampleUser watched: Star Trek [2009] [PG-13] [duration: 1 hour, 44 minutes, and 1 second]
 Sun Jun 30 19:45:01 2013: exampleUser watched: Your Highness [2011] [R] [duration: 1 hour and 24 minutes]
```

#####  without --nogrouping [default]
```
  Sun Jun 30 15:12:01 2013: exampleUser watched: Your Highness [2011] [R] [duration: 1 hour, 56 minutes, and 53 seconds]
  Sun Jun 30 15:46:02 2013: exampleUser watched: Star Trek [2009] [PG-13] [duration: 2 hours, 8 minutes, and 18 seconds]
```


### Stats - users total watched time with total per day

* --start, --stop, --user options can be supplied to limit the output

```
/opt/plexWatch/plexWatch.pl --stats

Date Range: Anytime through Now

======================================== Stats ========================================

user: Stans's total duration 3 hours and 56 seconds
 Thu Jul 11 2013: Stan 16 minutes and 58 seconds
 Fri Jul 12 2013: Stan 1 hour, 41 minutes, and 59 seconds
 Sat Jul 13 2013: Stan 1 hour, 1 minute, and 59 seconds

 user: Franks's total duration 2 hours, 43 minutes, and 2 seconds
  Thu Jul  4 2013: Frank 57 minutes and 1 second
  Sun Jul 14 2013: Frank 1 hour, 46 minutes, and 1 second
```



<br/>
## Additional options

#### --stats

```
 --start=...                     limit watched status output to content started AFTER/ON said date/time
 --stop=...                      limit watched status output to content started BEFORE/ON said date/time
 --user=...                      limit output to a specific user. Must be exact, case-insensitive
 --exclude_user=...              exclude users - you may specify multiple on the same line. '--notify --exclude_user=user1 --exclude_user=user2
```
#### --watched

```
 --start=...                     limit watched status output to content started AFTER/ON said date/time
 --stop=...                      limit watched status output to content started BEFORE/ON said date/time
 --nogrouping                    will show same title multiple times if user has watched/resumed title on the same day
 --user=...                      limit output to a specific user. Must be exact, case-insensitive
 --exclude_user=...              exclude users - you may specify multiple on the same line. '--notify --exclude_user=user1 --exclude_user=user2'
```
### Advanced --recently_added options
```
* All Movie Sections : ```./plexWatch.pl --recently_added=movie```

* All Movie / TV Sections : ```./plexWatch.pl --recently_added=movie,show```

* Specific Section(s) : ```./plexWatch.pl --recently_added --id=# --id=#```

```

./plexWatch.exe --recently_added

        * Available Sections:

        ID    Title                Type       Path
        -------------------------------------------------------------------
        8     Concerts             movie      /NFS/Videos/Music
        6     Movies               movie      /NFS/Videos/Film
        17    Holiday Movies       movie      /NFS/Videos/Others/Holiday_Movies
        5     TV Shows             show       /NFS/Videos/TV

        * Usage:

        All Movie Sections    : ./plexWatch.pl --recently_added=movie
        All Movie/TV Sections : ./plexWatch.pl --recently_added=movie,show
        Specific Section(s)   : ./plexWatch.pl --recently_added --id=# --id=#
```

<br/>
## Advanced options - config.pl

#### Grouping of watched shows

```
$watched_show_completed = 1; always show completed show/movie as it's own line (default 1)
```

```
$watched_grouping_maxhr = 2; do not group shows together if start/restart is > X hours (default is 3 hours)
```

#### SQLite backups

By default this script will automatically backup the SQLite db to: $data_dir/db_backups/ ( normally: /opt/plexWatch/db_backups/ )

* you can force a Daily backup with --backup

It will keep 2 x Daily , 4 x Weekly  and 4 x Monthly backups. You can modify the backup policy by adding the config lines below to your existing config.pl
```perl
$backup_opts = {
     'daily' => {
         'enabled' => 1,
         'keep' => 2,
     },
     'monthly' => {
         'enabled' => 1,
         'keep' => 4,
     },
     'weekly' => {
         'enabled' => 1,
         'keep' => 4,
      },
  };
```

Idea, thanks to https://github.com/vwieczorek/plexMon. I initially had a really horrible script used to parse the log files...  http://IP:PORT/status/sessions is much more useful. This was whipped up in an hour or two.. I am sure it could use some more work.
