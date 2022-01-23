---
layout: single
title: "How to verify file hashes at the terminal in one line"
date: 2022-01-23 01:00:00 +100
last_modified_at:
categories:
tags: howto terminal md5 sha hash digest
---
Let's talk about verifying file hashes of downloads. If you don't care to verify hashes then you can probably close this tab and go about your day, but as a security professional I'm supposed to care about these things and it'd be terribly embarassing if I got pwned by a bad download. Besides, file downloads [have been compromised before.](https://blog.linuxmint.com/?p=2994)

It's real easy to calculate the hash of a file, but when provided with a file and a file hash (for example, when downloading a linux distro), I recently found myself at a loss as to an easy way to verify that the file you have matches the hash that you're given; calculating the hash of your download and verifying-by-eyeball is clearly the silly way to go about it.

Sometimes your counterparty will be nice enough to give you a digest file, but sometimes all you have is the digest string and digest type.

Let's go through the different ways of verifying your file.

## If you don't have a digest file
I'm putting this first since it's the more common case. If you only have the digest string itself you can `echo` your digest string and the file name to the digest command (for example, `shasum` for the SHA family) like so:

```
echo "da39a3ee5e6b4b0d3255bfef95601890afd80709  dummy.txt" | shasum -a 256 -c
```

Note that -a 256 specifies the SHA-256 algorithm. Check `man shasum` for more details including the list of algorithms. Common ones are `1`, `256`, `512`. The default if no algorithm is specified is `1`.

Note also the **double space** in the input. `shasum` expects this and will complain if it's not present, for example:
```
% echo "1ce7ca2eb7dd9154f81eda0a62df9083f211a7a3c92f41735836591dcda6356f849aac9877160160593fee69f0a7ddc1 dummy.txt" | shasum -a 384 -c
shasum: standard input: no properly formatted SHA checksum lines found
```

You might ask why this double space is required. The answer is that this indicates the input mode of the file. A space indicates text, an asterisk indicates binary, for example:
```
% shasum -b /bin/ls
462b0b66f9df7a369d204427e4a9964cdefde77c */bin/ls
```
Here `shasum -b` indicates that the file should be read in binary mode when calculating the hash, and we can see that the output include an asterisk before the filename to indicate this. There's other input modes too, check the man page.

The `sha1sum` and `sha256sum` (and other) utilities exist and appear to be functionally equivalent to running `shasum` with the appropriate parameter, so the output of  `shasum -a 256 dummy.txt` is compatible with `sha256sum` for example.

The `md5sum` utility also exists although it isn't sensitive to the double space requirement.
Other utilities also exist for other algorithms such as BLAKE2. More info here: [Summarizing files (GNU Coreutils 9.0)](https://www.gnu.org/software/coreutils/manual/html_node/Summarizing-files.html)


## If you have a digest file
A digest file is simply the output of the digest tool itself redirected to a file. You can then run that same digest tool on the file using that tool's 'check' or 'verify' utility. The tool will then check each file listed in your digest against the corresponding hash.

`shasum -a <algorithm> -c filename.sha` 

## Making a digest file
The digest file is simply the output of the digest utility. A digest file is a plain text file where each line of the file consists of an expected hash and a file name annotated with an input mode (usually just a space).

You can create one by redirecting the utility's output to a file as shown below.

```
% sha384sum dummy.txt > dummy.sha
% cat dummy.sha
1d0f284efe3edea4b9ca3bd514fa134b17eae361ccc7a1eefeff801b9bd6604e01f21f6bf249ef030599f0c218f2ba8c  dummy.txt
% sha384sum -c dummy.sha
dummy.txt: OK
```

If you have multiple files to work with, you can compile multiple hashes at once like so:
```
% shasum -a 384 dummy.txt dummy2.txt
1d0f284efe3edea4b9ca3bd514fa134b17eae361ccc7a1eefeff801b9bd6604e01f21f6bf249ef030599f0c218f2ba8c  dummy.txt
a32402f4d4da96288bf12107af53d799d786bb4a85da97b1e77b3432338ac5b75319c4a10415a92eabc9d41968a90cbc  dummy2.txt
```
The same process will work for verifying the hashes. As long as your digest file has multiple lines each with a hash followed file a valid file name then it will verify those hashes against those files.

## A shell script to make it easier
If you find yourself doing this often, you could write something in your bashrc or zshrc (or whatever) to make it quick and easy. Here's an admittedly somewhat inelegant[^1] thing I threw together which checks the four most common hash algorithms I've run into in practice:

```bash
sh_check_hash() {
    if [ $# != 2 ]; then
        echo "Usage: sh_check_hash <hash> <file>"
        echo "Checks MD5 or SHA-1,-256,-512 only"
        return
    fi

    local len=${#1}

    if [ $len = 32 ]; then
        # 32 chars = md5 digest
        echo "Checking MD5"
        echo $1 $2 | md5sum -c
    elif [ $len = 40 ]; then
        # 40 chars = sha1 digest
        echo "Checking SHA1"
        echo "$1  $2" | shasum -a 1 -c
    elif [ $len = 64 ]; then
        # 40 chars = sha-256 digest
        echo "Checking SHA-256"
        echo "$1  $2" | shasum -a 256 -c
    elif [ $len = 128 ]; then
        # 40 chars = sha1 digest
        echo "Checking SHA-512"
        echo "$1  $2" | shasum -a 512 -c
    else
        echo "Bad hash length"
    fi
```

et voila:

```
% sh_check_hash 1d0f284efe3edea4b9ca3bd514fa134b17eae361ccc7a1eefeff801b9bd6604e01f21f6bf249ef030599f0c218f2ba8c dummy.txt
Checking SHA-284
dummy.txt: OK
```

And that's it, that's all I wanted to say.

[^1]: It belongs in another article, but I tend to have a rather utilitarian philosophy about shell scripts and the like. These aren't the place to write poetry.
