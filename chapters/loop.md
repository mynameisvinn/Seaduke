# `main()` is an event loop that polls for instructions
```python
def main():  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2183
    threadStuffKlass = DoingThreadStuffKlass()
    networkHandleKlass = NetworkHandlerKlass()
    while 1:
        ...
        networkTasks=networkHandleKlass.get_tasks()
        ..
        if networkTasks:
            ...
                    if not threadStuffKlass.have_task(taskID):
                        try:
                            threadStuffKlass.put(taskID,taskData)
               				...
            time_sleep(random_randint(3,7))
        else:
            time_sleep(random_randint(*botKlass.update_interval))
            botKlass.tick_count+=1
```
after instantiating `threadStuffKlass` and `networkHandleKlass`, seaduke enters into an event loop. in this loop, seaduke asks `networkHandleKlass` to check for instructions. 

if `networkHandleKlass` receives instructions that have not been executed, seaduke places it on `threadStuffKlass` and executes. after executing, seaduke waits for three or seven seconds before cycling.

if `networkHandleKlass` does not receive anything (ie `networkTasks` is None) then it waits for a few seconds and cycles back.