---
layout: single
title: "Checkpoint CSA 2018 writeup - Careful Steps"
date: 2019-04-20 01:00:00 +100
categories:
tags: howto bash checkpoint ctf writeup
---
Checkpoint put a CTF online last year with some fun challenges. As of this writing the challenges are still online [here](https://csa.checkpoint.com/index.php?page=chmain)

In this entry I'll explain how I solved the puzzle called "Careful Steps". I'm unaffiliated with Checkpoint and they haven't reviewed this solution.



## Introduction

>This is a bunch of archives we've found and we believe a secret flag is somehow hidden inside them.
>
>We're pretty sure the information we're looking for is in the comments section of each file.
>
>Can you step carefully between the files and get the flag?
>
>Good luck!
>



## Solution
The provided archive contains 2,000 smaller archives, each about 120-130 bytes or so, each with a name like unzipme.x, where x ranges from 0 to 1999.

![so many archives]({{ "/assets/images/2019-04-20-carefulsteps-archives.png" | absolute_url }})

Looking at the first file in a hex editor I can see that it's a rar file. 

![magic bytes]({{ "/assets/images/2019-04-20-carefulsteps-magicrarbytes.png" | absolute_url }})

Using the `unrar` utility reveals that the archive contains a *'Boring.txt'* of size 0. It also reveals that the archive headers contain a comment: *"W,204"*

![rar metadata, including archive comment]({{ "/assets/images/2019-04-20-carefulsteps-rarinfo.png" | absolute_url }})

On a hunch, I try looking at the file unzipme.204 - it turns out this one isn't a rar file but rather a zip. the `zipnote` utility reveals the comment for this one to be *"e, 1567"*. At this point it seems like the comments contain a letter and a reference to the next file we should look at.

The file 1567 is another rar file, and contains the comment *"t,-359"*. There are no negative files to view, so this is a dead end. What if, however, the numbers weren't a reference to an absolute file number, but rather a relative reference?

If I add 1567 to 204 the result is 1771, so let's try and see what the comment of unzipme.1771 is:

![zip metadata, including archive comment]({{ "/assets/images/2019-04-20-carefulsteps-zipinfo.png" | absolute_url }})

It looks like the 'relative reference' hypothesis is correct. Now let's crunch through the first few steps by hand:

```
0: W, 204
204: e, 1567
1771: l, -672
1099: l, -29
1070: <space>, 305
1375: d,217
1592: o,348
1940: n,-104
1836: e,-1712
124, <space>, 1554
1678: b,311
```

This is starting to look like a message, albeit one that wants to waffle on for a while before it gives us the flag that we're looking for; time to automate! After a lot of cursing and googling I whipped up the script below.



```bash
# checkfiles.sh
# steps through a range of archives in the provided directory
# to reconstruct a flag from the archive comments
# built to solve the Checkpoint CSA 2018 problem: Careful Steps
# by Ian Hutchinson 2018

#!/bin/bash

IFS=', '
filepointer=0
outputstring=""
while ((1 > -1))
do
	file="$1/unzipme.$filepointer"
	output=$(file "$file")
	regex="RAR"
	if [[ $output =~ $regex ]]
	then
		output="$(unrar l $file | sed -n 4p)"
		read nextchar jump <<< "$output"
		outputstring="$outputstring$nextchar"
		echo "$outputstring"
		filepointer=$(($filepointer + $jump))
	fi
	regex="Zip"
	if [[ $output =~ $regex ]]
	then
		output="$(zipnote $file | sed -n 4p)"
		read nextchar jump <<< "$output"
		outputstring="$outputstring$nextchar"
		echo "$outputstring"
		filepointer=$(($filepointer + $jump))
	fi	
done

```

This script starts with unzipme.0 and invokes the unix `file` command to determine the file type, based on the file type is then invokes the appropriate utility to view archive comments - either `unrar` with the `l` option (`l` lists the archive contents, and shows archive comments) or `zipnote` - the result is then piped to `sed` to extract the appropriate line.

The line is separated into the next character and the jump. The next character is appended to the output and the jump is used to point to the next file. I don't know how long the flag is going to be, so I just set the script to run indefinitely and print the output at each step, and I'll stop it when it appears to be done.

A portion of the output is shown below.

![the flag!]({{ "/assets/images/2019-04-20-carefulsteps-flag.png" | absolute_url }})

It seems like at the very end it repeats the same character over and over, so that's where I stopped the script's execution. The final message is:
`Welldonebuddy!Youseemtobeabletostepcarefullythroughthefiles.Thisisyourflag:flag{ARchV!es_Ar3_Th3_BeSt}`

It looks like the spaces weren't translated properly, but that doesn't matter. We have the flag for this exercise now!
`flag{ARchV!es_Ar3_Th3_BeSt}`