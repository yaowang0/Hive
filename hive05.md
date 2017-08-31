##### hiveserver2

启动hiveserver2:<br>
$HIVE_HOME/bin/hiveserver2<br>
OR<br>
$HIVE_HOME/bin/hive --service hiveserver2<br>

默认端口：10000<br>
telnet localhost 10000<br>

连接hiveserver2:<br>
% bin/beeline 
!connect jdbc:hive2://localhost:10000 root  org.apache.hive.jdbc.HiveDriver<br>

show tables;<br>

如何连接JDBC：<br>
