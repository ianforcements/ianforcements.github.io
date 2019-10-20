---
layout: single
title: "Checkpoint CSA 2018 writeup - PNG++"
date: 2019-04-27 01:00:00 +100
categories:
tags: howto python checkpoint ctf writeup crypto png
---
Checkpoint put a CTF online last year with some fun challenges. As of this writing the challenges are still online [here](https://csa.checkpoint.com/index.php?page=chmain).

Here's how I solved the challenge entitled "PNG++". Checkpoint were super nice when I asked whether they mind me posting this solution, but they did request that I remind you that I'm not affiliated with them and that they haven't reviewed this solution.

With that out of the way, let's look at the description of the problem.

## Introduction
>This image was encrypted using a custom cipher.
>We managed to get most of its code here
>Unfortunately, while moving things around, someone spilled coffee all over key_transformator.py.
>Can you help us decrypt the image? 
>

The files provided are **encrypted.png** (which isn't a proper png and can't be viewed) and **encrypt.py**, which looks exactly like this:

```python
import key_transformator
import random
import string

key_length = 4


def generate_initial_key():
    return ''.join(random.choice(string.ascii_uppercase) for _ in range(4))


def xor(s1, s2):
    res = [chr(0)]*key_length
    for i in range(len(res)):
        q = ord(s1[i])
        d = ord(s2[i])
        k = q ^ d
        res[i] = chr(k)
    res = ''.join(res)
    return res


def add_padding(img):
    l = key_length - len(img)%key_length
    img += chr(l)*l
    return img


with open('flag.png', 'rb') as f:
    img = f.read()

img = add_padding(img)
key = generate_initial_key()

enc_data = ''
for i in range(0, len(img), key_length):
    enc = xor(img[i:i+key_length], key)
    key = key_transformator.transform(key)
    enc_data += enc

with open('encrypted.png', 'wb') as f:
    f.write(enc_data)
```

## Solution

Firstly, let's look at encrypted.jpg in a hex editor. According to the [png spec](http://libpng.org/pub/png/spec/1.2/PNG-Structure.html) a valid PNG file should start with the bytes `89 50 4E 47 0D 0A 1A 0A`, looking in our file we see that the first eight bytes are `CE 06 03 01 45 5D 54 4D`, so this explains why our PNG won't render properly.

Now let's check out encrypt.py. 

It appears that this script encrypts the file piece-by-piece by XOR-ing each successive piece with a key. The key is transformed between each piece by using key_transformator, which we don't have, so we'll need to look harder to figure out what it does.

On line 5 of encrypt.py the key_length is set to four bytes. We know that our decrypted file should contain the eight magic PNG bytes at the very beginning, and we can compare those against the first eight bytes of our encrypted file. If we XOR these byte-by-byte we will find the key bytes that were used to encrypt the file in the first two blocks, which will provide a clue as to what key_transformator does.

You can see the working below. The original PNG bytes are the eight-byte magic number sequence all PNGs must start with. The encrypted PNG bytes are the first eight bytes from the encrypted.png file. The key bytes are calculated by XORing each original byte with the encrypted counterpart.

|ORIGINAL PNG BYTES:  |89 50 4E 47 |0D 0A 1A 0A|
|ENCRYPTED PNG BYTES: |CE 06 03 01 |45 5D 54 4D|
|-----|------------|-----------|
|KEY BYTES: |47 56 4D 46 |48 57 4E 47|

Comparing the first four key bytes with the second four, it's clear that all key_transformator does is increment each byte of the key by one! It's a simple matter to implement this directly into the encrypt.py script. 
Here's what it looks like:
```python
import string

key_length = 4

def key_transformator(key):
    return ''.join(chr((ord(char)+1)%256) for char in key)

def generate_initial_key():
    return "\x47\x56\x4d\x46"


def xor(s1, s2):
    res = [chr(0)]*key_length
    for i in range(len(res)):
        q = ord(s1[i])
        d = ord(s2[i])
        k = q ^ d
        res[i] = chr(k)
    res = ''.join(res)
    return res


def add_padding(img):
    l = key_length - len(img)%key_length
    img += chr(l)*l
    return img


with open('encrypted.png', 'rb') as f:
    img = f.read()

img = add_padding(img)
key = generate_initial_key()

enc_data = ''
for i in range(0, len(img), key_length):
    enc = xor(img[i:i+key_length], key)
    key = key_transformator(key)
    enc_data += enc

with open('flag.png', 'wb') as f:
    f.write(enc_data)
```

Now that we have the complete encryption algorithm and the key bytes, we can simply run this algorithm on our encrypted file and the original image will appear.

![The flag is guarded by a friendly tiger]({{"/assets/images/2018-10-20-flag.png" | absolute_url }})

And there's the flag:
*flag{|^olling_my_own_c|^ypto}*

