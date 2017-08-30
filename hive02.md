Hive三种方式区别与搭建<br>
Hive中metastore元数据存储的三种方式：<br>
- Derby方式
- Local方式
- Remote方式

##### 本地Derby
cp hive-default.xml.template hive-site.xml<br>
vim hive-site.xml<br>
```
<?xml version="1.0"?>  
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>  
  
<configuration>  
<property>  
  <name>javax.jdo.option.ConnectionURL</name>  
  <value>jdbc:derby:;databaseName=metastore_db;create=true</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionDriverName</name>  
  <value>org.apache.derby.jdbc.EmbeddedDriver</value>  
</property>  
   
<property>  
  <name>hive.metastore.local</name>  
  <value>true</value>  
</property>  
   
<property>  
  <name>hive.metastore.warehouse.dir</name>  
  <value>/user/hive/warehouse</value>  <!-- 存储在hdfs的路径 -->
</property>  
</configuration>
```

注：使用derby存储方式时，运行hive会在当前目录生成一个derby文件和一个metastore_db目录。这种存储方式的弊端是在同一个目录下同时只能有一个hive客户端能使用数据库，否则会提示如下错误<br>
[html] view plaincopyprint?<br>
hive> show tables;  <br>
FAILED: Error in metadata: javax.jdo.JDOFatalDataStoreException: Failed to start database 'metastore_db', see the next exception for details.  <br>
NestedThrowables:  <br>
java.sql.SQLException: Failed to start database 'metastore_db', see the next exception for details.  <br>
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask  <br>
hive> show tables;<br>
FAILED: Error in metadata: javax.jdo.JDOFatalDataStoreException: Failed to start database 'metastore_db', see the next exception for details.<br>
NestedThrowables:<br>
java.sql.SQLException: Failed to start database 'metastore_db', see the next exception for details.<br>
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask<br>

**修改HADOOP_HOME\lib目录下的jline-*.jar变成HIVE_HOME\lib下的jline-2.12.jar**<br>
这个包就是用来连接hive的。<br>

启动：<br>
hive<br>
