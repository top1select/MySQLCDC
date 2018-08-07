
java -classpath ${CUR_CLASSPATH}
 -Dspring.profiles.active=mysql.rowbase56
 -Dmysql_shard_0_server="127.0.0.1"
 -Dmysql_shard_0_ha1_server="127.0.0.1"



find / -name my.cnf
find / -name auto.cnf

nano /usr/local/etc/my.cnf
nano /usr/local/var/mysql/auto.cnf

log-bin = /Users/willw/Downloads/JavaProjects/fountain/logs/mysql
expire-logs-days = 5
max-binlog-size  = 50M
# manually configure the server_id my.cnf dependent, are likely to cause conflicts
# and automatically generate 128 bit UUID algorithm can guarantee that all MySQL UUID are not conflict.
# 配置mysql replaction需要定义，不能和canal的slaveId重复
server-id        = 1
# This option specifies whether global transaction identifiers (GTIDs) are used to identify transactions.
# Setting this option to --gtid-mode=ON requires that enforce-gtid-consistency be set to ON
enforce-gtid-consistency = ON
gtid-mode=ON

mysql.server start

mysql.server stop

mysql.server restart

mysql -u root -p
password: root

mysql> show variables like 'binlog_format';
mysql> show variables like 'log_bin';
show global variables like 'gtid_mode';
show global variables like '%gtid_executed%'\G;

SHOW VARIABLES WHERE Variable_name = 'port';


tail -f /usr/local/var/mysql/wills-mbp.lan.err