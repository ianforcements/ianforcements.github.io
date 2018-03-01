---
layout: single
title:  "Network packet capture from Virtualbox guests"
date:   2018-02-12 01:00:00 +0100
categories: 
tags: howto dhcp virtualbox wireshark packet
---
I'm starting this blog to, amongst other purposes, document some things I have to spend any meaningful about of time searching for. Hopefully these entries will be able to save time for someone!

Another thing I'm doing in 2018 is writing a rudimentary DHCP server, for fun and learning. This lead me to wonder, what do DHCP packets actually look like in the wild? What better way to see this than spin up a VM and watch the packets as the guest wakes up!

I initially thought I'd have to do some black magic using wireshark but it turns out VirtualBox has this feature built in - you have to use VBoxManage however, this being the CLI for Virtualbox.

Documentation on VBoxManage is here. There's an enormous array of features:  
<https://www.virtualbox.org/manual/ch08.html#idm3660>

In particular, I'm invoking the 'modifyvm' mode and accessing the networking settings documented here:  
<https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm>

Once a VM exists and is ready to go (I cooked up a fresh one running a liveCD, to ensure no extant network configuration), run the following:  
`VBoxManage modifyvm vmname --nictrace(N) on --nictracefile(N) outfile`

Let's break down those parameters:  
`vmname` is the name of your VM, as seen in the virtualbox console  
`outfile` is the path to the file you wish to export to, and  
`(N)` is the identifier for the network interface. Usually this will be 1 unless your virtual machine has multiple network interfaces  (ie, use `--nictrace1` and `--nictracefile1`).

Then you just start the VM and you're off! Be sure to turn nictrace off when you're done, otherwise the capture file will grow forever. This is done simply:  
`VBoxManage modifyvm vmname --nictrace1 off`

One important detail that seems more difficult to find than it should be is the location of vboxmanage under OSX. Here's where I found it on my machine, running VirtualBox 5.1.22:  
`/Applications/VirtualBox.app/Contents/Resources/VirtualBoxVM.app/Contents/MacOS`

Once this is done you get a lovely .pcap file which opens up just fine in wireshark, and check it out:

![captured packets - let them go!]({{ "/assets/images/2018-02-12-virtualbox-packet-capture-wiresharkpcap.png" | absolute_url }})

The entire four-step DHCP discover-offer-request-ack process, right there at the top!
