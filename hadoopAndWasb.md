# How to enable WASB on Hadoop

[WASB](https://blogs.msdn.microsoft.com/cindygross/2015/02/04/understanding-wasb-and-hadoop-storage-in-azure/) is automatically enabled in HDInsight clusters. But you can also mount a blob storage account manually to a Hadoop instance that lives anywhere as long as it has Internet access to the blob storage. Here are the steps:

I assume that you have a standard Apache distrition of Hadoop 2.7.1 installed in /usr/local/hadoop directory on a Linux box.

##Step 1. Verify your Hadoop version
This needs to be 2.7.1 or later.

```
/usr/local/hadoop/bin/hadoop version
```

##Step 2. Verify that you have these 2 jar files in your hadoop installation.

```
ls /usr/local/hadoop/share/hadoop/tools/lib/hadoop-azure-2.7.1.jar
ls /usr/local/hadoop/share/hadoop/tools/lib/azure-storage-2.0.0.jar
```

##Step 3. Modify hadoop-env.sh
Modify $HADOOP_HOME/etc/hadoop/hadoop-env.sh file to add these 2 jar files to Hadoop classpath at the end of the file.

```
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/usr/local/hadoop/share/hadoop/tools/lib/hadoop-azure-2.7.1.jar:/usr/local/hadoop/share/hadoop/tools/lib/azure-storage-2.0.0.jar
```

##Step 4. Modify core-site.xml
Modify $HADOOP_HOME/etc/hadoop/core-site.xml file to add these name-value pairs in the configuration to point to the blob storage.

```
<property>
  <name>fs.AbstractFileSystem.wasb.Impl</name>
  <value>org.apache.hadoop.fs.azure.Wasb</value>
</property>

<property>
  <name>fs.azure.account.key.my_blob_account_name.blob.core.windows.net</name>
  <value>my_blob_account_key</value>
</property>

<!-- optionally set the default file system to a container -->
<property>
  <name>fs.defaultFS</name>
  <value>wasb://my_container_name@my_blob_account_name.blob.core.windows.net</value>
</property>
```
If you don't want to expose your storage account key in core-site.xml. You can also encrypt it. Read more [here](https://hadoop.apache.org/docs/current/hadoop-azure/index.html). 

##Step 5. Test the connection. 

```
/usr/local/hadoop/bin/hadoop fs -ls wasb:///
/usr/local/hadoop/bin/hadoop fs -ls wasb://my_container_name@my_blob_account_name.blob.core.windows.net
/usr/local/hadoop/bin/hadoop fs -ls / # if the default file system is set to wasb

```

References:
- [Official Apache documentation](https://hadoop.apache.org/docs/current/hadoop-azure/index.html)
- [Why WASB makes Hadoop on Azure so very cool](https://blogs.msdn.microsoft.com/cindygross/2015/02/03/why-wasb-makes-hadoop-on-azure-so-very-cool/)
- [Understanding WASB and Hadoop Storage in Azure](https://blogs.msdn.microsoft.com/cindygross/2015/02/04/understanding-wasb-and-hadoop-storage-in-azure/)
- [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-use-blob-storage/)
- [Create and upload data to Azure Blob Storage for Hadoop](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-use-blob-storage/)

