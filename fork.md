# forking
starting with:
```python
if v_sys_platform!='win32':  # v_sys_platform=sys.platform
    forkmeiamfamous()
```
if sys is not win32 (perhaps it is darwin), then seaduke will fork itself.
```python
def forkmeiamfamous():
    import os as os_unix
    os_popen2=os.popen2
    os_getpid=os.getpid
    os_mkdir=os.mkdir
    os_chdir=os.chdir
    os_unix_fork=os_unix.fork
    os_getcwd=os.getcwd
    os_path=os.path
    os_open=os.open
    os_close=os.close
    os_o_excl=os.O_EXCL
    os_unix_umask=os_unix.umask
    os_o_creat=os.O_CREAT
    os_unix_setsid=os_unix.setsid
    os_remove=os.remove
    os_unlink=os.unlink
    os_o_rdwr=os.O_RDWR
    os_chmod=os.chmod
    os_fstat=os.fstat
    try:
        if botKlass.frozen:
            attr__MEIPASS=getattr(sys,'_MEIPASS',None)
            os_chmod(attr__MEIPASS,0555)
        os_unix_forked=os_unix_fork()
        if os_unix_forked>0:
            sys_exit(0)
    except OSError,e:
        pass
    
    # the following three syscalls decouples the child proc from parent https://www.oreilly.com/library/view/python-cookbook/0596001673/ch06s08.html
    os_chdir("/")  # change working directory to home directory
    os_unix_setsid()  # not 100% sure but it keeps child process running even if parent proc exits
    os_unix_umask(0)
    
    try:
        os_unix_forked=os_unix_fork()
        if os_unix_forked>0:
            sys_exit(0)
    except OSError,e:
        pass
```
* question: what is the point of forking parent process?