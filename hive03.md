hive 本地MySQL安装：<br>

这种存储方式需要在本地运行一个mysql服务器，并作如下配置（下面两种使用mysql的方式，需要将**mysql的jar包拷贝到$HIVE_HOME/lib目录下**）。 <br>
vim hive-site.xml<br>
```
<?xml version="1.0"?>  
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>  
  
<configuration>  
<property>  
  <name>hive.metastore.warehouse.dir</name>  
  <value>/user/hive/warehouse</value>  <!-- 存储在hdfs的路径 -->
</property>  
   
<property>  
  <name>hive.metastore.local</name>  
  <value>true</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionURL</name>  
  <value>jdbc:mysql://localhost/hive?createDatabaseIfNotExist=true</value>  x
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionDriverName</name>  
  <value>com.mysql.jdbc.Driver</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionUserName</name>  
  <value>username</value>  
</property>  
   
<property>  
  <name>javax.jdo.option.ConnectionPassword</name>  
  <value>password</value>  
</property>  
</configuration>  
```

安装MySQL:<br>
yum -y install mysql-server<br>

service mysql restart<br>
mysql -uroot -p <br>

use mysql<br>
delete from user where user='';<br>
update user set password=PASSWORD(123456);<br>
flush privileges;<br>

select user,host user;<br>
显示：<br>
root %     表示任何人都可以访问<br>
root 127.0.0.1<br>
root master <br>


