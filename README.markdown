# About
`timetravel` is a command-line tool for accessing the files in your Time Machine backups.

Time Machine is an OS X technology for performing continuous backups of your files to local or remote disks.  Since OS X 10.7 (Lion), Time Machine makes local backups of all your files.  This means you have snapshot versions of all your files at different times in the past.  If you are running Lion right now, you already have these snapshots.

To access all this backup data, OS X comes with a program named Time Machine, which opens a GUI front-end which lets you use Finder to browse your backups.  This interface is really slow and tedious for anyone used to navigating their system on the command-line.  To solve this problem, `timetravel` was written.

![Demo](http://stuff.lhunath.com/shots/shot.1333636642.png )

#Usage
`timetravel` takes the following options:

* `-H [host]`: Specify the host whose backups to search.
* `-T [time]`: Specify the time of the snapshots to search.
* `-D [disk]`: Specify the label of the disk whose backups to search.
* `-l`: List all known backups of the file.
* `-r`: Restore the file from backup.
* `-d`: Show the difference of the file with its backup.
* `-f`: Don't abort before destructive operations.

`timetravel` also takes a file argument.  This can be any file or directory that exists either on your file system or in a backup.  Files may be specified using an absolute or relative pathname.  Relative names are resolved against the current working directory. When no file is given, `timetravel` will work with the current working directory instead.

When no operation option is given (such as `-l`, `-r` or `-d`), `timetravel` will show you the contents of the file in the backups.

When showing the contents of directories, their files are enumerated.  When showing the contents of a file, a pager is opened for it if `timetravel`'s standard output is a terminal.  If `timetravel` is piped or redirected, the contents of the file is written out raw.  This allows you to recover files to new filenames or do things like searching them with `grep`.

When no host, time or disk is specified (using `-H`, `-T` or `-D`), `timetravel` will use default values for them.  The host will default to the name of your computer, the time will default to `Latest` and the disk will default to `Macintosh HD`.  When using `timetravel` to list snapshots (the `-l` option), these will default to empty values instead.  Note that when listing snapshots, these values are actually search prefixes.  If, for example, you use `-T 2012-06`, all snapshots in June 2012 will be searched.  Empty values will cause all snapshots of that type to be searched.

#Bugs
Report any bugs or feature requests as issues in [GitHub](https://github.com/lhunath/timetravel/issues) or contact <lhunath@lyndir.com>