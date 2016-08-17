Enabling WASB on Hadoop

Windows Azure Storage Account is designed with a HDFS interface. It is automatically enabled in HDInsight clusters. But you can also mount a blob storage account to a Hadoop instance that lives anywhere as long as it has Internet access to the blob storage. Here is how to do this:

Assuming that you have a standard Apache distrition of Hadoop 2.7.1 installed in /usr/local/hadoop directory. 

1. Verify your Hadoop version
2. Verify that you have these 2 jar files.
3. Modify hadoop-env.sh file to add these jars to classpath.
4. Modify core-site.xml file to 
5. Optionally, set it to default.
6. Test the connection. 
