###### hive的UDF
自定义函数包括三种UDF、UDAF、UDTF<br>
UDF(User-Defined-Function) 一进一出<br>
UDAF(User- Defined Aggregation Funcation) 聚集函数，多进一出。Count/max/min<br>
UDTF(User-Defined Table-Generating Functions)&#160; 一进多出，如lateral view explore()<br>
使用方式 ：在HIVE会话中add 自定义函数的jar文件，然后创建function继而使用函数<br>

UDF开发<br>
1、UDF函数可以直接应用于select语句，对查询结构做格式化处理后，再输出内容。<br>
2、编写UDF函数的时候需要注意一下几点：<br>
a）自定义UDF需要继承org.apache.hadoop.hive.ql.UDF。<br>
b）需要实现evaluate函数，evaluate函数支持重载。<br>
3、步骤<br>
a）把程序打包放到目标机器上去；<br>
b）进入hive客户端，添加jar包：hive>add jar /run/jar/udf_test.jar;<br>
c）创建临时函数：hive>CREATE TEMPORARY FUNCTION add_example AS 'hive.udf.Add';<br>
d）查询HQL语句：<br>
    SELECT add_example(8, 9) FROM scores;<br>
    SELECT add_example(scores.math, scores.art) FROM scores;<br>
    SELECT add_example(6, 7, 8, 6.8) FROM scores;<br>
e）销毁临时函数：hive> DROP TEMPORARY FUNCTION add_example;<br>