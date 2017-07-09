# Linux Cheatsheet

## Virtual filesystems
### Proc
`/proc` is a virtual filesystem, those files and folders aren't really stored on the hard drive, they contain process information :

Memory configuration : `cat /proc/meminfo`

Processor info : `cat /proc/cpuinfo`

In `/proc`, each of the numbered directories corresponds to an actual process ID (`ps ax`) :
```bash
/proc/PID/cmdline
#Command line arguments.

/proc/PID/cpu
#Current and last cpu in which it was executed.

/proc/PID/cwd
#Link to the current working directory.

/proc/PID/environ
#Values of environment variables.

/proc/PID/exe
#Link to the executable of this process.

/proc/PID/fd
#Directory, which contains all file descriptors.

/proc/PID/maps
#Memory maps to executables and library files.

/proc/PID/mem
#Memory held by this process.

/proc/PID/root
#Link to the root directory of this process.

/proc/PID/stat
#Process status.

/proc/PID/statm
#Process memory status information.

/proc/PID/status
#Process status in human readable form.
```
