# saving `bot`, `bot` on disk

lets pretend we want seaduke to save itself. perhaps we have the following:
```python

class HandleCommandKlass(object):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1614
    ...

    def __special_process(self,v_bot_command,v_optional):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1661
        ...
        if v_bot_command=='autoload':
            botActionKlass=BotSelfActionsKlass()
            if q.command=='register':
                    w = botActionKlass.register()
                    ...
```
that brings up `botActionKlass`'s register:
```python
class BotSelfActionsKlass(object):
    ...

    def register(self,**pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTzDeiQ):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1140
        ...
        botKlass.save()
```
that brings up a `botKlass`'s save method:
```python
class BotKlass(object):

    def save(self):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L414
        settings_file_path=self.settings_file_path
        with open(settings_file_path,"wb")as settings_file:
            ...
        return self.__settings
```
that brings up botKlass's settings_file_path attribute:
```python
class BotKlass(object):

    @property
    def settings_file_path(self):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L461
        key_id=get_default_settings()['key_id']
        if v_sys_platform.startswith('win'):
            de = 'tmp' + key_id.lower()
        else:
            de = '.' + key_id
        pe = tempfile_gettempdir()
        ...
        return os_path.join(pe, de)
```
if you recall, the `settings_file_path` was [created and locked](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/install.md) by `BotInstallKlass`.