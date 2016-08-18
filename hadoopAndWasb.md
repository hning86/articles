# How to enable WASB on Hadoop

WASB is automatically enabled in HDInsight clusters. But you can also mount a blob storage account manually to a Hadoop instance that lives anywhere as long as it has Internet access to the blob storage. Here are the steps:

I assume that you have a standard Apache distrition of Hadoop 2.7.1 installed in /usr/local/hadoop directory on a Linux box. So your HADOOP_HOME is /usr/local/hadoop.

Step 1. Verify your Hadoop version

```
/usr/local/hadoop/bin/hadoop version
```

Step 2. Verify that you have these 2 jar files.

```
ls /usr/local/hadoop/share/hadoop/tools/lib/hadoop-azure-2.7.1.jar
ls /usr/local/hadoop/share/hadoop/tools/lib/azure-storage-2.0.0.jar
```

Step 3. Modify $HADOOP_HOME/etc/hadoop/hadoop-env.sh file to add these 2 jar files to Hadoop classpath.

```
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$HADOOP_HOME/share/hadoop/tools/lib/hadoop-azure-2.7.1.jar:$HADOOP_HOME/share/hadoop/tools/lib/azure-storage-2.0.0.jar
```

Step 4. Modify $HADOOP_HOME/etc/hadoop/core-site.xml file to add these name-value pairs in the configuration to point to the blob storage.

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

Step 5. Test the connection. 

```
/usr/local/hadoop/bin/hadoop fs -ls wasb:///
/usr/local/hadoop/bin/hadoop fs -ls wasb://my_container_name@my_blob_account_name.blob.core.windows.net
/usr/local/hadoop/bin/hadoop fs -ls wasb://another_container_on_the_same_blob@my_blob_account_name.blob.core.windows.net
/usr/local/hadoop/bin/hadoop fs -ls / # if the default file system is set to wasb

```
