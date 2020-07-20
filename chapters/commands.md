# executing [arbitrary commands](https://unit42.paloaltonetworks.com/unit-42-technical-analysis-seaduke/) on threads
once seaduke decodes instructions into a json, it can execute accordingly. 

```python
class HandleCommandKlass(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1614

    def __special_process(self,v_bot_command,v_optional):
            ...
            if v_bot_command=='autoload':
                ...
            elif v_bot_command=='migrate':
                ...
            elif v_bot_command=='eval':  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1839
```

## where is `HandleCommandKlass` used?
seaduke creates an instance of [`DoingThreadStuffKlass`](https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2111) in `main()`:
```python
def main():
	threadStuffKlass = DoingThreadStuffKlass()
	...
```
`threadStuffKlass` is a dict container for instances of `pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzQiDy`, which is defined as:
```python
class pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzQiDy(threading_thread):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2057

	def __init__(self,taskID,taskData,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):
		self.task_id=taskID
		self.task_data=taskData
		self.on_complete=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ.get('on_complete',None)
		self.network_handler=NetworkHandlerKlass()
		threading_thread.__init__(self)
		self.processor = pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDeQ()
```
when instantiated, `pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzQiDy` creates an instance of `pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDeQ()` named `self.processor`.

`pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDeQ()` is defined as such:
```python
class pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTyzDeQ(object):
	...
	def process(self,pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzeDQy):
		...
		handle_command_klass=HandleCommandKlass()
```