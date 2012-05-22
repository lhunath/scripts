# About
`bashlib` is a library of convenience functions for the GNU Bash shell.

Bash is the POSIX-compliant shell you find on most any UNIX system. This library makes it a little easier to make sane and appealing bash scripts.

Amoungst the many features it provides are:

 * `trc`, `dbg`, `inf`, `wrn`, `err`, `ftl`: allow easy printf-style outputting at different verbosity levels.
 * `emit`, `spinner`: provide several types of spinners to keep the user enthralled while waiting for some lengthy task to complete.
 * `ask`: a simple function that makes taking user input just that bit easier.
 * `showHelp`: an easy way to show some documentation on your script's usage.
 * And lots of other tiny but helpful functions for various tasks.


#Usage
Ideally, install bashlib in your `PATH` and put this at the top of your scripts:

    source bashlib

See the comments in the file for information about what the functions do and how to use them.


#Bugs
Report any bugs or feature requests as issues in [GitHub](https://github.com/lhunath/bashlib/issues) or contact <lhunath@lyndir.com>
