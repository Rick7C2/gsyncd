gsyncd
=====

Gsyncd is a simple bash script that watches for file changes and gsyncs them to Google Drive. It uses inotify to watch for file system changes and syncs the whole directory to a remote machine using gsync. The script makes sure to aggregate change events during a running rsync, such that after the initial sync a subsequent sync can be triggered (and so on).

Requirements
------------
Right now a linux based system with inotify-tools and rsync installed is required, .e.g for ubuntu/debian based systems run
```
apt-get install inotify-tools rsync
```

For Mac OS X support https://github.com/ggreer/fsevents-tools could be integrated instead of inotify.


Installation
------------
 * Clone the script in a directory of your choice, e.g.
```
cd ~/opt
git clone git@github.com:drunomics/syncd.git
```
 * Best, put syncd in your $PATH, for example by running:
```
cd syncd
sudo ln -s $PWD/syncd /usr/local/bin/syncd
```

Usage
-----
* Copy the gsyncd.conf file to the directory you want to sync, or in some of its parent directories and adapt it your needs.
* Run "gsyncd start" in any directory below of the directory holding your gsyncd.conf file to start the daemon script.
* By default, the script will create a .gsyncd.pid file for tracking the daemon process ID and a .gsyncd.log file to which the gsync output will be written.
* Arguments known are the ones known from initd scripts (start,stop,restart,status) as well as "run" for manually triggering a gsync and "log" for checking the gsync output.
