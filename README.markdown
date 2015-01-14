This repo holds some generally useful scripts I've written.  If any of these turn out useful to you, buy some beer in celebration and drink it to my health and good fortune.

## [bashlib](https://github.com/lhunath/scripts/tree/master/bashlib)
`bashlib` is a library of convenience functions for the GNU Bash shell.

Bash is the POSIX-compliant shell you find on most any UNIX system. This library makes it a little easier to make sane and appealing bash scripts.

Amoungst the many features it provides are:

 * `trc`, `dbg`, `inf`, `wrn`, `err`, `ftl`: allow easy `printf`-style outputting at different verbosity levels.
 * `emit`, `spinner`: provide several types of spinners to keep the user enthralled while waiting for some lengthy task to complete.
 * `ask`: a simple function that makes taking user input just that bit easier.
 * `showHelp`: an easy way to show some documentation on your script's usage.
 * And lots of other tiny but helpful functions for various tasks.

### Usage
The recommended way of using `bashlib` is by creating a symlink in `PATH` to the `bashlib` script in your check-out of this repo.  Eg.

    ln -s ~/.src/scripts/bashlib/bashlib ~/.bin/

Then your scripts can use it by doing a `source` without specifying the location, like this:

    source bashlib

See the comments in the file for information about what the functions do and how to use them.


## [timetravel](https://github.com/lhunath/scripts/tree/master/bashlib)
`timetravel` is a command-line tool for accessing the files in your Time Machine backups.

Time Machine is an OS X technology for performing continuous backups of your files to local or remote disks.  Since OS X 10.7 (Lion), Time Machine makes local backups of all your files.  This means you have snapshot versions of all your files at different times in the past.  If you are running Lion right now, you already have these snapshots.

To access all this backup data, OS X comes with a program named Time Machine, which opens a GUI front-end that lets you use Finder for browsing your backups.  This is really slow and tedious for anyone used to navigating their system on the command-line.  To solve this problem, `timetravel` was written.

[See a codestre.am demo.](http://codestre.am/18c63b95276c6fa8fd1c28e24)

### Usage
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

## [mvn-tools](https://github.com/lhunath/scripts/tree/master/mvn-tools)

`mvn-tools` is a collection of utilities for working with maven repositories and
java web application distributions.

- mvn-auto: Build only the Maven artifacts in a multi-module project that have been modified since the last build. Compares the mtime of each file in `src/` against the product in `target/` to determine whether the artifact is outdated.
- mvn-install: Add a Java archive or ZIP as an artifact to the local repository. The script asks you for all required information.
- mvn-meta: Maintains a tree that caches hashes of repository files. Primarily a library; used by mvn-web.
- mvn-release: Generate releases for your artifacts, deploy and tag/branch in GIT. Uses maven-release-plugin and works best when you extract all versions of project artifacts out of your pom.xml's (except from <parent>).
- mvn-sync: Uses rsync to synchronize your local repository with a remote one for building remotely.
- mvn-tools: Installer / common library for the framework.
- mvn-web: Used to manage live extracted files from JBoss to a safe location where you can easily edit and see live changes.  Also allows you to apply your edits to these files back onto your repository.

## [tunmgrd](https://github.com/lhunath/scripts/tree/master/tunmgrd)

`tunmgrd` is a daemon that you use to bring up and keep up SSH connections.  Great for setting and keeping up tunnels, port forwards and master connections.

I've had a really hard time finding a quality product that did this for me in a portable and sane manner.  In the end, I decided I'd be better off writing it myself.  The goals for `tunmgrd` is:

- Good and safe code
- Extensive configurability
- Clear and correct documentation
- Useful reporting
- Useful client utilities to interact with the daemon

[![demo of tunmgrd](http://stuff.lhunath.com/tunmgrd-demo.png)](https://asciinema.org/a/15436)

## [diagnose](https://github.com/lhunath/scripts/tree/master/diagnose)

`diagnose` is a tool for checking what's going on with your connectivity to the Internet.

"Internet connectivity" is a very vague term and generally means "I can connect to stuff over the public network".  This tool checks if you can reach a bunch of popular servers and if issues are detected tries some simple tests to diagnose possible causes.

### Usage

Run `diagnose` and look at what it tells you.  If breakage is detected, it will generally issue some mildly useful advice.

## [parseJSON](https://github.com/lhunath/scripts/tree/master/parseJSON)

`parseJSON` is a filter used to convert JSON data into a structure much more friendly to parsing from bash scripts.

Each output element describes one key-value structure in the JSON stream.  By default, elements are output separated by newlines (one on a line).  Elements consist of a sequence of type characters (`.` for object key and `#` for array index), followed by the value of the key, and finally a `=` followed by the value of the structure.  Eg. the output of:

    parseJSON <<< '{"foo":"bar", "child":[5, 6, {"cow":"moo"}]}'

is:

    .foo=bar
	.child#0=5
	.child#1=6
	.child#2.cow=moo

### Usage
`parseJSON` takes the following options:

* `-z`: Use a NUL byte as delimitor between data structures.
* `-d [delim]`: Use `delim` as delimitor between data structures.  `printf`-style escapes are accepted (eg. `\0`).
* `-v`: Verbosely describe what happens during the parsing of the JSON data.

# Bugs
Report any bugs or feature requests as issues in [GitHub](https://github.com/lhunath/scripts/issues) or contact <lhunath+gh@lyndir.com>


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/lhunath/scripts/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

