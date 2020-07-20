# forkmeimfamous
## what's the point of forkmeimfamous?
`forkmeimfamous` forks seaduke as a [daemon process](https://www.oreilly.com/library/view/python-cookbook/0596001673/ch06s08.html), thus allowing it to run as a background process even though the parent process (which was called by the user) no longer exists. 

```python
if v_sys_platform!='win32':  # v_sys_platform=sys.platform
    forkmeiamfamous()


def forkmeiamfamous():  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2211
    ...
    try:
        ...
        if os_unix_forked>0:
            sys_exit(0)
    except OSError, e:
        pass
    
    # the following three syscalls decouples the child proc from parent https://www.oreilly.com/library/view/python-cookbook/0596001673/ch06s08.html
    os_chdir("/")  # change working directory to home directory
    os_unix_setsid()  # not 100% sure but it keeps child process running even if parent proc exits
    os_unix_umask(0)
    
    try:
        os_unix_forked = os_unix_fork()
        if os_unix_forked>0:
            sys_exit(0)
    except OSError,e:
        pass
```


## extra credit
you can run the following script to how `forkmeimfamous` does what it does. in fact, `forkmeimfamous` is almost identical to the following example.
```python
import sys, os

def proc():
    """ An example daemon main routine; writes a datestamp to file
        /tmp/daemon-log every 10 seconds.
    """
    import time

    f = open("forkme.dat", "w")
    while 1:
        f.write('%s\n' % time.ctime(time.time(  )))
        f.flush(  )
        time.sleep(10)


if __name__ == "__main__":
    # Do the Unix double-fork magic; see Stevens's book "Advanced
    # Programming in the UNIX Environment" (Addison-Wesley) for details
    print("starting...")

    try:
        pid = os.fork()
        if pid > 0:
            # Exit first parent
            sys.exit(0)
    except OSError as e:
        print (sys.stderr, "fork #1 failed: %d (%s)" % (e.errno, e.strerror))
        sys.exit(1)

    # Decouple from parent environment
    os.chdir("/")
    os.setsid(  )
    os.umask(0)

    # Do second fork
    try:
        pid = os.fork()
        if pid > 0:
            # Exit from second parent; print eventual PID before exiting
            print ("Daemon PID %d" % pid)
            sys.exit(0)
    except OSError as e:
        print (sys.stderr, "fork #2 failed: %d (%s)" % (e.errno, e.strerror))
        sys.exit(1)

    # Start the daemon main loop
    proc()
```