hive 远端MySQL(即多用户模式)安装：<br>

在远端机器执行：<br>
hive --service metastore<br>

##### remote一体
这种存储方式需要在远端服务器运行一个mysql服务器，并且需要在Hive服务器启动meta服务。<br>
这里用mysql的测试服务器，ip为192.168.1.214，新建hive_remote数据库，字符集为latine1<br>
```
<?xml version="1.0"?>  
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>  
   
<configuration>  
  
<property>  
  <name>hive.metastore.warehouse.dir</name>  
  <value>/user/hive/warehouse</value>  <!-- 存储在hdfs的路径 -->
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionURL</name>  
  <value>jdbc:mysql://192.168.57.6:3306/hive?createDatabaseIfNotExist=true</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionDriverName</name>  
  <value>com.mysql.jdbc.Driver</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionUserName</name>  
  <value>hive</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionPassword</name>  
  <value>password</value>  
</property>  
  
<property>  
  <name>hive.metastore.local</name>  
  <value>false</value>  
</property>  
  
<property>  
  <name>hive.metastore.uris</name>  
  <value>thrift://192.168.1.188:9083</value>  
</property>  
  
</configuration>
```
注：这里把hive的服务端和客户端都放在同一台服务器上了。服务端和客户端可以拆开.<br>

##### remote分开
将hive-site.xml配置文件拆为如下两部分<br>
1）、服务端配置文件<br>
```
<?xml version="1.0"?>  
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>  
   
<configuration>  
  
<property>  
  <name>hive.metastore.warehouse.dir</name>  
  <value>/user/hive/warehouse</value>  <!-- 存储在hdfs的路径 -->
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionURL</name>  
  <value>jdbc:mysql://192.168.57.6:3306/hive?createDatabaseIfNotExist=true</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionDriverName</name>  
  <value>com.mysql.jdbc.Driver</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionUserName</name>  
  <value>root</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionPassword</name>  
  <value>123456</value>  
</property>  
</configuration>  
```

2）、客户端配置文件<br>
```
<?xml version="1.0"?>  
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>  
   
<configuration>  
  
<property>  
  <name>hive.metastore.warehouse.dir</name>  
  <value>/user/hive/warehouse</value>  
</property>  
   
<property>  
  <name>hive.metastore.local</name>  
  <value>false</value>  
</property>  
  
<property>  
  <name>hive.metastore.uris</name>  
  <value>thrift://192.168.57.5:9083</value>  
</property>  
  
</configuration>  
```

启动hive服务端程序<br>
hive --service metastore  <br>


客户端直接使用hive命令即可<br>
root@my188:~$ hive   <br>
Hive history file=/tmp/root/hive_job_log_root_201301301416_955801255.txt  <br>
hive> show tables;  <br>
OK  <br>
test_hive  <br>
Time taken: 0.736 seconds  <br>
hive>  <br>