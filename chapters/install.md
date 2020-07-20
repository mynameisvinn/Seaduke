# carving space for itself on disk
one of seaduke's first tasks is to create a file on disk and, just as important, lock it. seaduke uses this protected file descriptor when it [registers or saves itself](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/save.md).

`BotInstallKlass` takes the `key_id` from botKlass object and uses it as a filename:
```python
botKlass = BotKlass()  # an instance of BotKlass() was created even before main() starts

if __name__=="__main__":
    ...
    me = BotInstallKlass(botKlass.key_id)


class BotInstallKlass(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2132

    def __init__(self,*key_id):
    q = key_id[0]
    ...
        f = 'tmp' + q.lower()
    ...
    self.lockfile = os_path.normpath(tempfile_gettempdir()+'/'+ f)
```

`BotInstallKlass` locks this file with `fcntl`, thus protecting it from being modified by other processes (eg deletion).
```python
class BotInstallKlass(object):

    def __init__(self,*key_id):
        ...
            self.fp=open(self.lockfile,'w')
            try:
                fcntl.lockf(self.fp,fcntl.LOCK_EX|fcntl.LOCK_NB)  # http://tilde.town/~cristo/file-locking-in-python.html
```
that's it for `BotInstallKlass`.