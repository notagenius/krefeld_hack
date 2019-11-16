# krefeld_hack

### API 

http://3.209.31.93:5001/classifier

### POST is with Json, images should be encoded as base64 in string 

{"in_base64_string": base64_string}

python example

```

import requests
import base64
from PIL import Image
import json
import time

def img_to_base64(img_filepath):
     return base64.b64encode(open(img_filepath, 'rb').read())

# test run. jpeg to base64 bytes
filepath = 'classifier/Garbage_datasets/val/paper/paper1.jpg'
encoded_base64 = img_to_base64(filepath)


# experiment 2: post with base64 json, extra encoding as utf-8 is needed
ENCODING = 'utf-8'
base64_string = encoded_base64.decode(ENCODING)
raw_data = {"in_base64_string": base64_string}
json_data = json.dumps(raw_data)
headers = {'Content-type': 'application/json', 'Accept': 'text/plain'}
r2 = requests.post("http://3.209.31.93:5001/classifier", json_data, headers=headers)
print(r2.text)
```
