# Tip 1 
## How to debug hive when insert fails

- Try to run a map-reduce job to see if hadoop is working, executing a map-reduce job usually generates a better log than hive.
- Check the job processing UI from hadoop to see any logging errors.

# Tip 2
## Enabling external access to hive using spark

- Change the hive-site.xml ip's to the external DNS

- It's possible to change the metastore ip without dropping the hive database

To change 
```
hive --service metatool -updateLocation NEW-URL OLD-URL
```
To check actual url
```
hive --service metatool -listFSRoot
```

In spark add the following configuration 

In runtime
```
sparkConf.set("hive.metastore.uris","thrift://"+hostName+":"+port).set("spark.sql.catalogImplementation", "hive").set("spark.hadoop.dfs.client.use.datanode.hostname", "true")
```

In spark-default.conf
```
"hive.metastore.uris" "thrift://hostname:port"
"spark.sql.catalogImplementation" "hive"
"spark.hadoop.dfs.client.use.datanode.hostname" "true"
```
