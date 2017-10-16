### HDFS

When a file is loaded into HDFS, it's split into chunks which called **blocks**. The default block size is 64 MB. Naming habit is **BLK, an underscore, and a large number**.

As the file is uploaded to HDFS, each block will get stored on **one node** in the cluster. There's a Damon running on each of the machines in the cluster called the **DataNode**.  The information stored on the NameNode is called **metadata**.

* **one of the nodes fails:**

To solve this problem, Hadoop **replicates each block three times**, as it's stored in HDFS. Hadoop just picks three nodes at random and puts one copy of the block on each of the three.
If a single node fails, we have two other copies of the block on other nodes, NameNode can see the blocks are now under-replicated, and it will arrange to have those blocks **re-replicated on the cluster.**

* **metadata lost**

For a long time, it is single point of failure.You still got all the blocks on the data nodes but you've not way of knowing which block belongs to which file without the metadata. 

To solve this problem, not only on its own hard drive, but also somewhere on a network file system.

These days, another alternative is NameNode is not a single point of failure. They've configured two NameNode, active node as before, standby can be configured to take over if the active one fails.


### Put file into HDFS
All of the commands which interact with Hadoop file system starts with **hadoop fs**. It closely mirror the standard UNIX file system commands.

*  See what we have in HDFS


```
hadoop fs -ls
```
returns a list of what's in the home directory on the Hadoop cluster.

*  Upload local file 


```
hadoop fs -put ***.txt
```

It takes a local file and places it into HDFS.

*  Take a look of last few lines of the file



```
hadoop fs -tail ***.txt
```

Display the last few lines on the screen.


* Display the entire contents of the file
```
hadoop fs -cat ***.txt
```


* Rename the file


```
hadoop fs -mv currentname.txt newname.txt
```


* Remove the file



```
hadoop fs -rm filename.txt
```

* Create a directory in HDFS


```
hadoop fs -mkdir directoryName
```
* Upload file in a directory


```
hadoop fs -put ***.txt directoryName
```
 * Show contents of a directory
 


```
 hadoop fs -ls directoryName
```



