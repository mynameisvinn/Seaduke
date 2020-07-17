# 1) installing `botKlass`
## `BotInstallKlass` installs `botklass` object
a `botKlass` instance was created earlier and it is called `botKlass`. it is immediately installed by `BotInstallKlass`.
```python
class BotKlass(object):
    ...

botKlass=BotKlass()

if __name__=="__main__":
    ...
    me=BotInstallKlass(botKlass.key_id)
```
`BotInstallKlass` takes the `key_id` from botKlass object and uses it as a filename:
```python
class BotInstallKlass(object):

    def __init__(self,*key_id):
    pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDie=key_id[0]
    ...
        pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyQzei='tmp'+pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDie.lower()
    ...
    self.lockfile=os_path.normpath(tempfile_gettempdir()+'/'+pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyQzei)
```
`BotInstallKlass` then locks that file with `fcntl`, thus preventing it from being modified by other processes.
```python
class BotInstallKlass(object):

    def __init__(self,*key_id):
        ...
        if self.platform=='win32':
            ...
        else:
            self.fp=open(self.lockfile,'w')
            try:
                fcntl.lockf(self.fp,fcntl.LOCK_EX|fcntl.LOCK_NB)  # http://tilde.town/~cristo/file-locking-in-python.html
```

