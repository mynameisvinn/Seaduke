# carving space for itself on disk
any self respecting bot needs to maintain persistence. 

one of seaduke's first tasks is to create a file on disk and, just as important, lock it. seaduke will use this protected file descriptor later when it [registers or saves itself](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/save.md).

```python
class BotKlass(object):
    ...


botKlass = BotKlass()  # an instance of BotKlass() was created even before main() starts

if __name__=="__main__":
    ...
    me = BotInstallKlass(botKlass.key_id)
```
`BotInstallKlass` takes the `key_id` from botKlass object and uses it as a filename:
```python
class BotInstallKlass(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2132

    def __init__(self,*key_id):
    q = key_id[0]
    ...
        f = 'tmp' + q.lower()
    ...
    self.lockfile = os_path.normpath(tempfile_gettempdir()+'/'+ f)
```

`BotInstallKlass` then locks that file with `fcntl`, thus preventing it from being modified by other processes (eg deletion).
```python
class BotInstallKlass(object):

    def __init__(self,*key_id):
        ...
            self.fp=open(self.lockfile,'w')
            try:
                fcntl.lockf(self.fp,fcntl.LOCK_EX|fcntl.LOCK_NB)  # http://tilde.town/~cristo/file-locking-in-python.html
```



