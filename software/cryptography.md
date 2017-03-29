$ pip install cryptography

https://cryptography.io/en/latest/

>>> from cryptography.fernet import Fernet
>>> key = Fernet.generate_key()
>>> f = Fernet(key)
>>> token = f.encrypt(b"my deep dark secret")
>>> token
'...'
>>> f.decrypt(token)
'my deep dark secret'


