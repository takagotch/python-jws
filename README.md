### python-jws
---
https://github.com/brianloveswords/python-jws

```py
import jws
header = { 'alg': 'HS256' }
payload = { 'claim': 'JSON is the raddest.', 'iss': 'brianb' }
signature = jws.sing(header, payload, 'secret')
jws.verify(header, payload, signature, 'secret')
jws.verify(header, payload, signature, 'badbadbad')


import ecdsa
sk256 = ecdsa.SigningKey.generate(curve=ecdsa.NIST256p)
vk = sk256.get_verifying_key()
header = { 'alg': 'ES256' }
sig = jws.sign(header, payload, sk256)
jws.verify(header, payload, sig, vk)


import jws
from jws.algos import AlgorithmBase, SignatureError
class FXUY(AlgorithmBase):
  def __init__(self, x, y):
    self.x = int(x)
    self.y = int(y)
  def sign(self, msg, key):
    return 'verysecure' * self.x + key * self.y
    
  def verify(self, msg, sig, key):
    if sig != self.sign(msg, key):
      raise SignatureError('nope')
    return True
    
 jws.algos.CUSTOM += [
   (r'^F(?P<x>\d)U(?P<y>\d{2})$', FXUY),
 ]
 
import jws
header = { 'alg': 'F7U12' }
payload = { 'claim': 'wutt' }
sig = jws.sign(header, payload, '<trollface>')
import sillycrypto
sig = jws.sign(header, payload, '<trollface>')
jws.verify(header, payload, sig, '<trollface>')
jws.verify(header, payload, sig, '<trollface>')
jws.verify(header, payload, sig, 'y u no verify?')
```

```sh
pip install jws
```

```
```


