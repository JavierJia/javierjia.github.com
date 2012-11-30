---
layout: post
category : code
tags: hadoop code
---

The release of Hadoop 0.23 changed some directories and bash script.
The /conf/ dir and some of start-all.sh is not easy to find any more

The instruction I learned and successfully installed is almost from the 
<http://www.crobak.org/2011/12/getting-started-with-apache-hadoop-0-23-0/>

## Download
I download from this address: <http://mirror.nexcess.net/apache/hadoop/common/hadoop-0.23.5/>

## Install prerequisite package

    $ sudo apt-get install ssh 
    $ sudo apt-get install rsync

## Setup passphraseless ssh
Now check that you can ssh to the localhost without a passphrase:

    $ ssh localhost

If you cannot ssh to localhost without a passphrase, execute the following commands:

    $ ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa 
    $ cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys

## Configure HDFS
The new 0.23 do not using the /conf/ folder again. All the configuration included into etc/hadoop/ folder.

### core-site.xml

    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    <configuration>
      <property>
        <name>fs.default.name</name>
        <value>hdfs://localhost:9000</value>
      </property>
    </configuration>

### NameNode and DataNode

    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>1</value>
        </property>
        <property>
            <name>dfs.namenode.name.dir</name>
            <value>file:/home/jianfeng/software/hadoop/hadoop-0.23.5/data/hdfs/namenode</value>
        </property>
        <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/jianfeng/software/hadoop/hadoop-0.23.5/data/hdfs/datanode</value>
        </property>
    </configuration>

### hadoop-env.sh
This file in 0.23 did not appear in the /conf/ since there is no longer that directory anymore. 
But it also not appear in the new configuration dir etc/hadoop.

From the reference blog I copy that one from below dir:

    $ cp ./share/hadoop/common/templates/conf/hadoop-env.sh etc/hadoop

#### Write several environment variant 
JAVA_HOME to bashrc
    
    $ export JAVA_HOME="$(readlink -f /usr/bin/javac | sed "s:/bin/javac::")"

Change some bogus value

    $ export HADOOP_PREFIX="/home/jianfeng/software/hadoop/hadoop-0.23.5"
    $ #export HADOOP_CONF_DIR=${HADOOP_CONF_DIR:-"/etc/hadoop"}
    $ export HADOOP_CONF_DIR="${HADOOP_PREFIX}/etc/hadoop" 

    $ #export HADOOP_LOG_DIR=${HADOOP_LOG_DIR}/$USER
    $ export HADOOP_LOG_DIR="${HADOOP_PREFIX}/logs"

## Start HDFS
Run scripts as below

    sbin/hadoop-daemon.sh start namenode
    sbin/hadoop-daemon.sh start datanode

## Check localhost
Browse the web interface for the NameNode and the JobTracker; by default they are available at:

    NameNode - http://localhost:50070/
    JobTracker - http://localhost:50030/
    
At this time, NameNode should success, Not yet the JobTracker


