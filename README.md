lbcapi is a simple python wrapper for the LocalBitcoins API to make it easier to develop applications that interface with LocalBitcoins.com.

To install
==========
pip install git+https://github.com/shiruken1/lbcapi.git

Usage example (using HMAC)
============
This example uses the library to call the /api/myself/ endpoint

```
from lbcapi import api

hmac_key = Your HMAC key here
hmac_secret = Your HMAC secret here

conn = api.hmac(hmac_key, hmac_secret)
conn.call('GET', '/api/myself/').json()
```

To find out all the available API calls please see the API documentation on LocalBitcoins.com
https://localbitcoins.com/api-docs/

Pagination example
============
Pagination seems to cause problems so, here is an example on how to do it with this library
```
import urlparse
from lbcapi import api

hmac_key = Your HMAC key here
hmac_secret = Your HMAC secret here

conn = api.hmac(hmac_key, hmac_secret)
ads_json = conn.call('GET', '/api/ads/').json()
parsed = urlparse.urlparse(ads_json['pagination']['next'])
params = urlparse.parse_qs(parsed.query)
ads_json_II = conn.call('GET', '/api/ads/', params=params).json()

```


