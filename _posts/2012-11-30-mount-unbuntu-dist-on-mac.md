---
layout: post
category : configure
tags: mac ubuntu sshfs
---
 
I've tried some of different approach on mount the ubuntu disk on my mac.
Like samba server, macfuse. I don't know why I can not connect the machine from the Finder using Go Server.
Then macfuse, I can't even install it.

After google a little using more straightforward words just "mount dist on mac", I got this *sshfs" 
application that solved my problem.

# Install

    sudo apt-get install sshfs

# Configuration
I didn't configure anything.

# Connect

    mkdir ~/mnt/xxx
    sshfs [user]@[host]:/dir ~/mnt/xxx

Make sure mount to a exist directory. It does't creat it for u.

Then it just works.
I can read and write on my remote disk now. 

# One more thing
In order to remote it after reboot, write those sshfs command in the bashrc


