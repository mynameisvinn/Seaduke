# what is this?
an anatomy of [seaduke](https://github.com/pan-unit42/iocs/blob/master/seaduke/decompiled.py)

```python
if __name__=="__main__":
    time_sleep(botKlass.run_delay)
    if not botKlass.was_first_run:
        botKlass.was_first_run = True
    if v_sys_platform != 'win32':
        forkmeiamfamous()
    me = BotInstallKlass(botKlass.key_id)

    try:
        seh_wrapper()
    except SystemExit:
        me = None
        time_sleep(1)
        sys_exit(0)
    except Exception as e:
        me = None
        time_sleep(1)
        sys_exit(0)
```
* initializing [bot settings](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/bot_settings.md) so bot knows how to bot
* forking itself so it can run as a [daemon/background process](https://github.com/mynameisvinn/Seaduke/blob/master/fork.md)
* [installing](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/install.md) botKlass, which really means carving space for itself on disk
* [seh_wrapper](https://github.com/mynameisvinn/Seaduke/blob/master/sehwrapper.md)
* doing an [event loop]() and polling for instructions
* how does seaduke [fetch instructions](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/fetch.md) from the mothership?
* [decode](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/decode.md) tasks
* [executing tasks](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/execution.md) with `threadStuffKlass`
* executing [arbitrary commands](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/commands.md)
* [saving]() bot bot