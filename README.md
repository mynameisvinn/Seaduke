# what is this?
an ongoing dissection of [seaduke malware](https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2211)

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

* [installing botKlass](https://github.com/mynameisvinn/Seaduke/blob/master/install.md)
* [seh_wrapper](https://github.com/mynameisvinn/Seaduke/blob/master/sehwrapper.md)
* [how does seaduke fetch instructions from the mothership?](https://github.com/mynameisvinn/Seaduke/blob/master/fetch.md)
* [decode](https://github.com/mynameisvinn/Seaduke/blob/master/decode.md)