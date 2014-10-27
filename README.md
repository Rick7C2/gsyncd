gsyncd
=====

Gsyncd is a simple bash script that watches for file changes and gsyncs them to Google Drive. It uses inotify to watch for file system changes and syncs the whole directory to a remote machine using gsync. The script makes sure to aggregate change events during a running gsync, such that after the initial sync a subsequent sync can be triggered (and so on).

Requirements
------------
Right now a linux based system with inotify-tools and gsync installed is required, .e.g for ubuntu/debian based systems run
```
apt-get install inotify-tools
```

For gsync follow the directions
...
https://github.com/iwonbigbro/gsync/wiki/Installation
...


Installation
------------
 * Clone the script in a directory of your choice, e.g.
```
cd ~/opt
git clone git@github.com:Rick7C2/gsyncd.git
```
 * Best, put gsyncd in your $PATH, for example by running:
```
cd gsyncd
sudo ln -s $PWD/gsyncd /usr/local/bin/gsyncd
```

Usage
-----
* Copy the gsyncd.conf file to the directory you want to sync, or in some of its parent directories and adapt it your needs.
* Run "gsyncd start" in any directory below of the directory holding your gsyncd.conf file to start the daemon script.
* By default, the script will create a .gsyncd.pid file for tracking the daemon process ID and a .gsyncd.log file to which the gsync output will be written.
* Arguments known are the ones known from initd scripts (start,stop,restart,status) as well as "run" for manually triggering a gsync and "log" for checking the gsync output.
