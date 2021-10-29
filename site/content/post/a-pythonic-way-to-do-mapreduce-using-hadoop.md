---
title: A Pythonic way to do MapReduce using hadoop
date: 2019-08-04T18:49:14.959Z
description: A Pythonic way to do MapReduce using hadoop
---
Hadoop is a collection of sub-projects from ASF to do hardcore distributed computing written in Java. If you have a look on their powered by page you will find most of the big boys are there. If you are from technology field you must be heard couple of these tools which are sub-projects of Hadoop: We will be using these three in throughout the post:



Hadoop Common: The common utilities that support the other Hadoop subprojects.

HDFS: A distributed file system that provides high throughput access to application data.

MapReduce: A software framework for distributed processing of large data sets on compute clusters.

Some other hadoop sub-projects:



Avro: A data serialization system.

Chukwa: A data collection system for managing large distributed systems.

HBase: A scalable, distributed database that supports structured data storage for large tables.

Hive: A data warehouse infrastructure that provides data summarization and ad hoc querying.

Mahout: A Scalable machine learning and data mining library.

Pig: A high-level data-flow language and execution framework for parallel computation.

ZooKeeper: A high-performance coordination service for distributed applications.

I have been using these tools for last one year. ASF has got a strong and healthy community which will guide you through if you really are a passionate programmer. Still I will be writing some posts here to share some common problems solving. My posts will be focused on Ubuntu/Debian based OS. OS-X is also pretty similar. So, if you are from windows and wished to try these on windows as well, then this is NOT the right place. Ok I am in, now what? Let’s get ourselves introduced with MapReduce first. It is popular programming model invented by Jeffrey Dean and Sanjay Ghemawat from Google. I am quoting exactly as it appears in their paper: “MapReduce is a programming model and an associated implementation for processing and generating large data sets. Users specify a map function that processes a key/value pair to generate a set of intermediate key/value pairs, and a reduce function that merges all intermediate values associated with the same intermediate key. Many real world tasks are expressible in this model, as shown in the paper.” Download MapReduce paper in: PDF Version MapReduce paper in Slides: HTML SlidesWe will be writing a MapReduce job which will be run via hadoop cluster. Let’s dive into the specs now. What we want from here is to aggregate individual marks for a student from different subjects. Let’s break down it into tasks:



Preparing the environment

Installing hadoop 0.20.2 on Ubuntu 10.10

Collecting all CSV files which contains students’ marks

Writing a mapper in Python for MapReduce

Writing a reducer in Python for MapReduce

Test the output using shell and pipe

Run MapReduce with hadoop

Fetch the hadoop output

by the way no war/jar business!

Preparing the environment:



Install Java 1.6.x, preferably open-jdk, must be installed. Here is the command to install it via aptitude:

sudo apt-get install openjdk-6-jre

Edit your bash profile <vim ~/.bashrc>  and append the following line to set JAVA_HOME.

export JAVA_HOME=/usr/lib/jvm/java-6-openjdk

Install ssh and rsync if don’t have it. You can install it from these two lines of commands via apt-get

sudo apt-get install ssh

sudo apt-get install rsync

Installing hadoop 0.20.2 on Ubuntu 10.10



Go get a stable release from here (I used 0.20.2)

Extract the tarball in your machine. In my case I extracted it in /media/raid/tools/hadoop-0.20.2

By default hadoop is set as a stand alone mode. We can test hadoop by the following commands:

cd /media/raid/tools/hadoop-0.20.2 #change the path as yours

mkdir input

cp conf/*.xml input

bin/hadoop jar hadoop-*-examples.jar grep input output ‘dfs\[a-z.]+’

cat output/*

Okay, now we are ready to run a MapReduce in stand alone mode

Collecting all CSV files which contains students’ marks Download sample data with mapper.py and reducer.py Writing a mapper in Python for MapReduceWe will be writing mapper in python which will read from stdout and print it with proper format. Here is the content:



\#!/usr/bin/env python

\##mapper.py

\_\_author\_\_ = 'Nurul Ferdous '

\_\_version\_\_ = '0.2.20'



import sys



for line in sys.stdin:

\    ln = line.strip()

\    data = ln.split(' ')

\    print '%s\t%s' % (data\[0], data\[1])

Writing a reducer in Python for MapReduce



\#!/usr/bin/env python

\##reducer.py



\_\_author\_\_ = 'Nurul Ferdous '

\_\_version\_\_ = '0.2.20'



from operator import itemgetter

import sys



agregatedmarks = {}



for line in sys.stdin:

\    name, marks = line.rstrip().split('\t')

\    try:

\    if agregatedmarks.get(name):

\    agregatedmarks.get(name).append(marks)

\    else:

\    agregatedmarks\[name] = \[marks]

\    except ValueError:

\    pass



sortedmarksheet = sorted(agregatedmarks.items(), key=itemgetter(0))

for name, marks in sortedmarksheet:

\    print '%s\t%s'% (name, marks)

Test the output using shell and pipeNow it’s time to test the result using pipe in shell:



cd /media/raid/sandbox/mapreduce #change the path as yours

cat data/math.txt | ./mapper.py | sort | ./reducer.py

The above command should give an output similar to this:

waters  \['46']

watkins \['69']

watson  \['44']

watts   \['69']

weaver  \['94']

webb    \['59']

webber  \['97']

weber   \['51']

webster \['42']

weeks   \['56']

weir    \['95']

weiss   \['63']

welch   \['85']

wells   \['58']

welsh   \['72']

werner  \['32']

wesley  \['89']

west    \['32']

Okay it’s time for invoking hadoop itself:



cd /media/raid/tools/hadoop-0.20.2

bin/hadoop jar contrib/streaming/hadoop-0.20.2-streaming.jar -file /media/raid/sandbox/mapreduce/mapper.py -mapper /media/raid/sandbox/mapreduce/mapper.py -file /media/raid/sandbox/mapreduce/reducer.py -reducer /media/raid/sandbox/mapreduce/reducer.py -input /media/raid/sandbox/mapreduce/data/*.txt -output marksheet

cat marksheet/*

The cat command above should show you something similar to this:



woody   \['82', '49', '21']

wooten  \['52', '29', '50']

workman \['27', '47', '92']

worley  \['29', '23', '58']

wray    \['37', '97', '61']

wright  \['84', '34', '69']

wu      \['30', '31', '83']

wyatt   \['37', '31', '83']

wynn    \['91', '90', '40']

xiong   \['64', '50', '33']

yang    \['78', '76', '62']

and here is the final version. download it
