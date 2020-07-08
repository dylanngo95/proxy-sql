# BenchMark

sysbench --test=oltp --oltp-table-size=1000000 --db-driver=mysql --mysql-db=test --mysql-user=root --mysql-password=123456 prepare

# Ip demo

172.28.1.4

# Login ProxySQL

mysql -u admin -padmin -h 127.0.0.1 -P6032 --prompt='Admin> '

# Select configuration

SELECT * FROM mysql_servers;

SELECT * from mysql_replication_hostgroups;

SELECT * from mysql_query_rules;

# Add mysql to ProxySQL

INSERT INTO mysql_servers(hostgroup_id,hostname,port) VALUES (1,'172.28.1.1',3306);

# Config user for monitor

UPDATE global_variables SET variable_value='admin' WHERE variable_name='mysql-monitor_username';

UPDATE global_variables SET variable_value='admin@123' WHERE variable_name='mysql-monitor_password';

UPDATE global_variables SET variable_value='2000' WHERE variable_name IN ('mysql-monitor_connect_interval','mysql-monitor_ping_interval','mysql-monitor_read_only_interval');

SELECT * FROM global_variables WHERE variable_name LIKE 'mysql-monitor_%';

# Load config

LOAD MYSQL VARIABLES TO RUNTIME;

SAVE MYSQL VARIABLES TO DISK;

# Check log

SHOW TABLES FROM monitor;

SELECT * FROM monitor.mysql_server_connect_log ORDER BY time_start_us DESC LIMIT 10;

SELECT * FROM monitor.mysql_server_ping_log ORDER BY time_start_us DESC LIMIT 10;

# Runtime

LOAD MYSQL SERVERS TO RUNTIME;

# Create

INSERT INTO mysql_users (username,password) VALUES ('tinhngo','admin@123');

LOAD MYSQL USERS TO RUNTIME;

SAVE MYSQL USERS TO DISK;

# mysql_replication_hostgroups

INSERT INTO mysql_replication_hostgroups VALUES (1,2,'cluster1');