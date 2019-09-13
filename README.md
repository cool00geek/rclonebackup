# Rclone backup

A simple python script to interface with rclone to provide an easy and synced backup solution to the target of your choice

## Features

- Progress bar in notification
- Preset saved commands and remotes
- Secondary and tertiary backups

## Usage

Note that you MUST be using the KDE Plasma desktop environment!!!

Be sure to install rclone and that `rclonebackup` is in your $PATH

Edit `rclonebackup` and set the following variables:

- `local_path` to be where you want your data to be synced locally
- `primary_remote_path` to be the remote (or path on a remote) that you want to sync with the local path
- `secondary_remote_path` to be the secondary remote (or path on remote) that you want to mirror the primary remote/dir to 
- `tertiary_remote_path` is the exact same as secondary, except a different remote to backup the primary remote to

You can now run `rclonebackup` with `push` `pull` `backup1`, or `backup2`

`push` will push new files on local or files that have been modified more recently to the remote (like git push)

`pull` will download changes from the remote to local that are newer on remote

`backup1` will mirror your primary remote to the secondary remote in a subfolder with today's date

`backup2` will mirror your primary remote to the tertiary remote in a subfolder with today's date

## Note

I am NOT responsible for any loss of data that occurs by use of this program. It works for me, but a simple misconfiguration can possibly lead to a LOSS OF DATA. Use it at YOUR OWN RISK!!!

This script also assumes you have a prior understanding of rclone and the configuration. Please familiarize yourself with rclone BEFORE running rclonebackup.

## Cron jobs

It may be helpful to automate the running of the sync

Since it relies on dbus to interface with the notification, be sure to add the following 2 lines to the top of your crontab:

```
DISPLAY=:0.0
XAUTHORITY=/home/vinay/.Xauthority
```

I have my jobs set so local changes get pushed every hour on the hour and remote changes get pulled every hour on the :30

```
30 * * * * /path/to/rclonebackup pull >> /tmp/rclone.log 2>&1
0 * * * * /path/to/rclonebackup push >> /tmp/rclone.log 2>&1
```

I recommend that you modify the commands to your liking (especially the path to your rclonebackup file)



