# Faulty Login - 100 points 
The problem contains the following description and a zip file.
```
Say hello to my super effective flag dispenser. Only the real user will be able to get the flag. Go ahead and try your best luck.
```
The zip file contains two files named `login.py` and `output.txt`. The contents of the files are as follows.

**login.py**
```py
from Crypto.Hash import SHA256
from Crypto.Util.number import long_to_bytes
from getpass import getpass
from .utils import check_user, check_flag

def hash_string(s):
    h = SHA256.new()
    h.update(s.encode())
    hash = h.hexdigest()
    return long_to_bytes(int(hash, 16))

username = input("Enter your username: ").strip()
pin = getpass("Enter your 8-digit pin: ").strip()

if not check_user(hash_string(username), hash_string(pin)):
    print("Invalid credentials. Exiting.")
    exit(1)

with open("private/flag.txt", 'r') as f:
    flag = f.read().strip()

if not check_flag(hash_string(flag)):
    print("Invalid flag. Exiting.")
    exit(1)

def encrypt(s, key):
    s = s.encode('utf-8')
    key = key.encode('utf-8')
    encrypted = b''
    for i in range(0, len(s), len(key)):
        encrypted += bytes([s[(i+j)%len(s)] ^ key[j] for j in range(len(key))])
    return encrypted

encrypted_flag = encrypt(flag, pin)
print("Here is the encrypted flag:", encrypted_flag)
```
**output.txt**
```
Enter your username: admin
Enter your 8-digit pin: 
Here is the encrypted flag: b'PM@ZFTNx\tgy\t@\x01jn\tJk\n|qGoi\x0f\x05\t|O\\C'
```

## Solution Approach:
The problem is a simple XOR cipher with a key consisting of 8 digits. The `hash_string` function seems to be a distraction as it is not much useful.

With the 8-digit pin, it is practical to go for a brute-force solution. Run a brute-force script with keys from `00000000` to `99999999` and search for flags with `iutctf{}` wrapper. This approach will work but take a considerable time.

A smarter way is to get the first seven digits of the key using the `iutctf{` string. And then brute-force the last digit with only 10 candidate flags.
```py
def decrypt(s, key):
    key = key.encode('utf-8')
    decrypted = b''
    for i in range(0, len(s), len(key)):
        decrypted += bytes([s[(i+j)%len(s)] ^ key[j] for j in range(len(key))])
    return decrypted

encrypted_flag = b'PM@ZFTNx\tgy\t@\x01jn\tJk\n|qGoi\x0f\x05\t|O\\C'
partial_flag = 'iutctf{'

print(decrypt(encrypted_flag, partial_flag).decode()[:7]) #9849225

for i in range(10):
    pin = '9849225' + str(i)
    
    flag = decrypt(encrypted_flag, pin)
    print(pin)
    print(flag)
``` 
The code will output the pins and the corresponding candidate flag. The rest is easy as the correct flag is the only intelligible one. The correct pin is `98492256`.

## Flag:
```
iutctf{N0_M0r3_X0r_3NCrYP710N}
```
