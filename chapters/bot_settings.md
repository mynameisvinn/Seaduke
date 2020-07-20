# what is `bot_settings`?
one of the first things the script does is fetch bot settings:
```python
# https://github.com/mynameisvinn/Seaduke/blob/f37849cc10336dbe0279a343a509b921109fdca2/source.py#L235
bot_settings=json_loads(zlib_decompress(base64_b64decode('eJx1kF1PwjAUhv/K0iuNpiUMg8Fw4QSTAfFrQQ3GNN12Nua2dpyWj0n877ZAvPOqzTnP+77nnD3JCtSG41ryFCrRkoHXufRICa223z0R4F4yDb/i7wVb7NLx1XTUfVf6fRXG4xTvdq1fr0ZRNHub9IP70ldDYvVWxouNUyYVzKdhcVHfvkbTWbf/2Juw+fNwSH4ctjaqUiLlGowpZH7MhB1wKWpw8pnKlZyH1NYOvk3zX8uODwa4yAygbWei0uAylsrupxMsGuPsP8jSmGbAWK1kYRRS3UqaSIZa02bZkE8rQcgADy4HWFt6u93STCQQK1XSRNXMRa41IBc5SOPQqDAQCGQ+9em1dxZYshZYehHgBvDGO+Vqi8UCqcKcnZPjrXmROoenXvCweOm4IkgRV3ab04H+FvoFdgWNdw==')))

bot_settings['bot_id']= id_generator(size=4)+ '-' + bot_settings['key_id']  # generate random id for thsi bot
```
when executed, `bot_settings` points to a dict:
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
this dict tells the bot a number of important things such as `host_scripts`.