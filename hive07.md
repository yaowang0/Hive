##### HWI
HWI是Hive Web Interface的简称，是hive cli的一个web替换方案。<br>
需要下载Hive的源码文件，然后将hwi/web目录下的文件用 jar cvf hive-hwi-0.13.1.war ./* <br>
其实war包也是zip包，可以通过<br>
cd hwi/web<br>
zip hive-hwi-1.2.1.zip ./*     //打包成.zip文件。<br>
将zip包后缀改成war<br>
mv hive-hwi-1.2.1.zip hive-hwi-1.2.1.war<br>
cp hive-hwi-1.2.1.war  /opt/sxt/soft/apache-hive-1.2.1-bin/lib/<br>
命令来打包成一个war包，然后放到Hive的lib目录下即可<br>
配置conf/hive-site.xml<br>
```
<property>
<name>hive.hwi.war.file</name>
<value>lib/hive-hwi-1.2.1.war</value>
</property>

<property>
<name>hive.hwi.listen.host</name>
<value>0.0.0.0</value>
</property>

<property>
<name>hive.hwi.listen.port</name>
<value>9999</value>
</property>

执行命令hive --service hwi
访问http://192.168.17.4:9999/hwi
```
