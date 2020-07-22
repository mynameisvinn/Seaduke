# executing tasks on threads
after seaduke [fetches instructions](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/fetch.md) from a remote server and [decodes it](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/decode.md), it will execute tasks using multithreading. 

## create a thread executor called `threadStuffKlass`
[main()](https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2183) creates an instance of `DoingThreadStuffKlass` called `threadStuffklass`:
```python
def main():  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2183
    threadStuffKlass = DoingThreadStuffKlass()
```

## putting tasks on `threadStuffKlass`
if `main()` receives a valid task from `NetworkHandleKlass`, then `main()` puts the task (aka `taskData` on `threadStuffKlass`:
```python
def main():
    threadStuffKlass=DoingThreadStuffKlass()
    networkHandleKlass=NetworkHandlerKlass()
    while 1:
        ...
        networkTasks=networkHandleKlass.get_tasks()
        ...
        if networkTasks:
            ...
                            threadStuffKlass.put(taskID, taskData)  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2198
```
## what happens when you put something on `threadStuffKlass`?
`threadStuffKlass` is an instance of `DoingThreadStuffKlass`:
```python
class DoingThreadStuffKlass(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2111

    def __init__(self):
        self.threads={}

    def put(self, taskID, taskData):
        DiQ = QiDy(taskID,taskData,on_complete=self.on_thread_complete)
        DiQ.daemon=True
        self.threads[taskID]=DiQ
        DiQ.start()

```
we see that calling `threadstuffklass.put()` creates an instance of `QiDy` called `DiQ`.

## what is `QiDy`?
`QiDy` is a class:
```python
class QiDy(threading_thread):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2057

    def __init__(self,taskID,taskData,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):
        self.task_id=taskID
        self.task_data=taskData
        self.on_complete=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ.get('on_complete',None)
        self.network_handler=NetworkHandlerKlass()
        threading_thread.__init__(self)
        self.processor=DeQ()
```
when instantiated, it creates an instance of `DeQ` called `self.processor`.

## what is class `DeQ`?
```python
class DeQ(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1974
    pass
```

## tying it all together
python's interpreter executes the object `DiQ` by calling its `run` method. 
```python
class QiDy(threading_thread):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2057

    def run(self):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2088
        ...
            v_return_message = self.processor.process(self.task_data)
```
which in turns calls `self.processor.process()`:
```python
class DeQ(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1974

    def process(self, task_data):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1997
        with self.cd(botKlass.current_dir):
            networkTask = json_loads(task_data)
            v_return_message=None
            ...
            if networkTask['command']==v_cmd:
                ...
            elif networkTask['command']==v_upl:
                ...
            elif networkTask['command']==v_srv:
                ...
        return v_return_message
```
so we see that seaduke can receive commands such as `v_cmd`, `v_upl`, `v_srv`.