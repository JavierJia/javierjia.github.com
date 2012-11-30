---
layout: post
category : code
tags: hadoop code
---

## for hadoop 0.23
Just known that the Hadoop-0.23 run on the YARN which don't need to keep the server.
Every time call the Yarn, there will be a call to open a new instance.

## Install Pig 0.10 on hadoop 0.23

The lucky thing is from this blog <http://hortonworks.com/blog/new-features-in-apache-pig-0-10/>
All we have to do is to build the pig again, using the 0.23-version option

    ant -Dhadoopversion=23

My step is following:
    
> checkout the latest source code 
>> svn co http://svn.apache.org/repos/asf/pig/trunk pig-trunk
> cd !$ && ant -Dhadoopversion=23
> mv pig*.jar $PIG_HOME

And then, it just worked. Great.


