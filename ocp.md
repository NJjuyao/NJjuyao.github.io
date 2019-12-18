### Question: 1
>A MySQL database uses all InnoDB tables and is configured as follows:  
shell>cat/ etc/ my.cnf   
[mysqld]   
log-bin server-id=1  
You will be setting up a replication slave by using mysqldump. You will need a consistent backup taken from your running production server. The process should have minimal impact to active
database connections.
Which two arguments will you pass to mysqldump to achieve this?  
A.--skip-opt  
B.--lock-all-table  
C.--create-apply-log  
D.--single-transaction  
E.--master-data    
>>Answer:     
D,E   

问：使用mysqldump设置复制从属。 您需要从正在运行的生产服务器上获取一致的备份。 关键点在备份时对服务器的影响最小.   
答：master-data 选项可以自动帮我们锁表和识别 binlog 临界文件，提高从库部署效率。和 --single-transaction 配合使用，只会在 dump 开始时一小段时间加全局读锁，可降低服务器影响

---
### Question: 2
>Consider the key buffer in a MySQL server. Which two statements are true about this feature?    
A.It caches index blocks for MyISAM tables only.    
B.It caches index blocks for all storage engine tables.    
C.It is a global buffer.    
D.It is set on a per-connection basis.    
E.It caches index blocks for InnoDB tables only.    
>>Answer:      
A,C   

问：MySQL服务器中的密钥缓冲区。哪两项陈述是正确的。    
答：     
A.它仅缓存MyISAM表的索引块    
C.这是一个全局缓冲区

---
### Question: 3
>You have a MySQL replication setup and you intentionally stop the SQL thread on the slave.   
mysql> SHOW SLAVE STATUS\G    
...    
Slave\_IO\_Running: Yes Slave\_SQL\_Running: No     
What are two reasons that you may stop the SQL thread on the slave while keeping the I/ O
thread running?    
A.to allow the remaining events to be processed on the slave while not receiving new events from the master    
B.to allow a backup to be created under reduced load     
C.to allow for point-in-time recovery on the slave      
D.to prevent schema changes from propagating to the slave before they are validated     
E.to prevent any transaction experiencing a deadlock      
>>Answer:      
C,D     

问：您可能在保持I/O线程运行的同时停止从属服务器上的SQL线程的两个原因是什么。    
答：     
C.允许从属服务器上的时间点恢复      
D.防止架构更改在验证之前传播到从属服务器


---
### Question: 4
>Which three statements correctly describe MySQL InnoDB Cluster?    
A.The cluster can be operated in multimaster mode with conflict detection for DML statements.     
B.All MySQL client programs and connectors can be used for executing queries.    
C.It provides fully synchronous replication between the nodes.     
D.There is support for automatic failover when one node fails.     
E.The data is automatically shared between the nodes.     
F.Each query will be executed in parallel across the nodes.     
>>Answer:     
A,B,D    

问：高可用集群部署MySQL InnoDB Cluster的描述；    
答：   
A.可以在具有DML语句冲突检测的多主机模式下运行群集;    
B.所有MySQL客户端程序和连接器均可用于执行查询;    
D.当一个节点发生故障时，支持自动故障转移;     


---
### Question: 5
>How does the InnoDB storage engine handle deadlocks when they are detected?      
A.Both the affected transactions will be rolled back.     
B.The affected transactions wait for innodb\_lock\_wait\_timeout seconds, and then roll back.      
C.One of the affected transactions will be rolled back, the other is allowed to proceed.      
D.The transaction isolation level determines which transaction is rolled back.     
E.The innodb\_locks\_unsafe\_for\_binlog setting determines which transaction is rolled back.     
>>Answer:       
C     

问：检测到死锁时，InnoDB存储引擎如何处理死锁；    
答：C.受影响的交互操作将被回滚，其他的将被允许继续进行。    


---
### Question: 6
>Which three allocate memory per thread in MySQL?      
A.query cache      
B.thread cache      
C.read buffer      
D.internal temporary table      
E.sort buffer      
F.InnoDB buffer pool instance      
>>Answer:        
C,D,E        

问：MySQL中，哪三个分配每个线程的内存    
答：    
C.读取缓冲区     
D.内部临时表    
E.sort缓冲区     

---
### Question: 7
>You are setting up a new installation of MySQL Server 5.7 (a GA release.) You have used a ZIP or TAR package to ensure that the mysqld binary, along with its support files, such as plug-ins and error messages, now exist on the host.      
Assume that the default datadir exists on the host. You installed the binary in the default location (the default --basedir value) for your operating system.      
Which step should you perform before defining your own databases and database tables?      
A.Execute a command with a minimal form of: mysqld --initialize      
B.Register mysqld as a service that will start automatically on this host machine.      
C.Create a configuration file containing default-storage-engine=InnoDB.      
D.Set an exception in the host machine’s firewall to allow external users to talk tomysqld.      
E.Create additional login accounts (so that everyone does not need to log in as root) and assign them appropriate privileges.       
>>Answer:        
A               

问：定义自己的数据库和数据库表之前应该执行哪个步骤      
答：A.执行以下形式的命令：mysqld --initialize


---
### Question: 8
>Which two options describe how MySQL Server allocates memory?      
A.Each connection may have its own per-thread memory allocations.      
B.Thread memory is pre-allocated up to thread\_cache\_size for performance.      
C.Each thread allocates memory from a global pool.      
D.Global memory resources are allocated at server startup.       
>>Answer:            
A,D               

问：哪两个选项描述了MySQL Server如何分配内存     
答：      
A.每个连接可能都有自己的每线程内存分配     
D.全局内存资源在服务启动时分配


---
### Question: 9
>Which two statements are true about InnoDB auto-increment locking?      
A.InnoDB never uses table\_level locks.      
B.InnoDB always protects auto-increment updates with a table-level lock      
C.InnoDB does not use locks to enforce auto-increment uniqueness.      
D.The auto-increment lock can be a table-level lock.      
E.Some settings for innodb\_autoinc\_lock\_mode can help reduce locking.       
>>Answer:          
D,E                    

问：关于InnoDB自动增量锁定，哪两个陈述是正确      
答：    
D.自动增量锁可以是表级锁     
E.innodb\_autoinc\_lock\_mode的某些设置可以帮助减少锁定     



---
### Question: 10
>You have just executed a manual backup by using this command:          
mysqlbackup -u root -p --socket=/tmp/my.sock --backup-dir=/my/backup/ backup The operation completed without error.       
What is the state of this backup and operation required before it is ready to be restored?       
A.Backup State = Compressed Backup; Operation = copy-back       
B.Backup State = Raw Backup; Operation = apply-log       
C.Backup State = Prepared Backup; Operation = validate       
D.Backup State = Prepared Backup; Operation = apply-log       
E.Backup State = Raw Backup; Operation = backup-dir-to-image        
>>Answer:           
B                     

问：mysqlbackup的备份方式，在还原之前，备份状态是什么，需要进行什么操作？    
答：B.Backup State =原始备份； 操作=apply-log；还原操作的第一步就是检测事务日志      


---
### Question: 11
>Host slave1 has ip address 192.0.2.10.    
Host slave2 has ip address 203.0.113.50     
Examine these commands:      
shell&gt;mysql\_config\_editor print --all      
[slave1] host = slave1.exampledomain.com user=robert      
[slave2] host = slave2.exampledomain.com user=karen      
shell&gt;mysql --login-path=slave1 --host= 192.0.2.10 -- user=robert -p     
Enter password:      
ERROR 1045 (28000): Access denied for user 'robert'@'192.0.2.10' (using password: YES)     
Why did this error occur?       
A.The host on the command line is not defined in the login path.       
B.The mysqld instance has not been restarted after creating the login path.       
C.There is no password defined in the login path.       
D.The DNS is not configured correctly for slave1 host.       
E.The mylogin.cnf file is not readable.       
>>Answer:            
C            

问：为什么会发生此错误       
答：C.在登录路径中没有定义密码        
mysql\_config\_editor出现在mysql5.6.6以后的版本，可以给指定的连接和密码生成一个加密文件.mylogin.cnf，默认位于当前用户家目录下。通过该文件可以使用mysql、mysqladmin等直接登录，避免明文密码出现在脚本中。      

---
### Question: 12
>You have installed MySQL Server for the first time on your system. However, the data directory along with the tables in the mysql system database are missing.        
Which step do you perform to create the contents of the data directory?       
A.Run the create\_system\_tables.sql file       
B.Run the mysql\_unpack.sql file       
C.Invoke mysqld with the --initialize option.       
D.Invoke mysql with the --initialize option.        
>>Anser:              
C              

问：第一次安装MySQL Server，但是数据目录以及mysql中的表均丢失。      
答：C.使用mysqld的--initialize选项初始化数据库。


---
### Question: 13
>A single InnoDB table has been dropped by accident. You are unable to use an additional intermediate MySQL instance to restore the table.        
Which two backup methods can be used to restore the single table without stopping the MySQL instance?       
A.a backup created with mysqldump --all-databases       
B.a backup created using FLUSH TABLES … FOR EXPORT       
C.an up-to-date replication slave       
D.a file system-level snapshot       
E.a file system copy created while MySQL was shut down.       
>>Answer:             
A,B       

问：单个InnoDB表已被意外删除，无法使用其他中间MySQL实例来还原表。可以使用哪种两种备份方法来还原单个表而不停止MySQL实例？          
答：        
A.使用mysqldump --all-databases创建的备份        
B.使用FLUSH TABLES…FOR EXPORT创建的备份         

---
### Question: 14
>You created a backup of the world database with this command:        
shell> mysqldump --opt world > dump.sql       
Which two will import the data from dump.sql?       
A.shell> mysqladmin recover test dump.sql       
B.shell> mysql test < dump.sql              
C.shell> mysqlimport test dump.sql              
D.mysql> USE test; mysql> LOAD DATA INFILE ‘dump.sql’;       
E.mysql>USE test; mysql>SOURCE dump.sql;        
>>Answer:          
B,E       

问：哪2个命令可以导入word数据库？       
答：        
B.shell> mysql test < dump.sql       
E.mysql>USE test; mysql>SOURCE dump.sql;             


---
### Question: 15
>There are multiple instances of MySQL Server running on a single OS that is backed up using the mysqlbackup command.       
The /etc/my/cnf contains default values,       
for example, datadir=/var/lib/mysql/, with extra instances having their own separate my.cnf file (for example
/etc/mysql/instanceN.cnf) overriding the defaults.       
A restore of the second instance is attempted from the mysqlbackup archive using this command:       
mysqlbackup --backup-dir=/opt/backup/mysql/instance2 copy-back       
Upon starting the second MySQL instance, you notice that the data does not match the expected backup.        
Which command-line option is required to successfully update the second instance?       
A.--restore=2       
B.--copy-back-from-log       
C.--backup-instance=/var/lib/mysql/instance2       
D.--instance=/var/lib/mysql/instance2       
E.--defaults-file=/etc/mysql/instance2.cnf        
>>Answer:              
E                     

问：怎么恢复instance2数据库，需要在mysqlbackup命令后面加什么参数？                  
答：E.--defaults-file=/etc/mysql/instance2.cnf          


---
### Question: 16
>The following grants were executed:       
GRANT CREATE ROUTING ON sales.* TO ‘webadmin’@’%’;       
GRANT ALTER ON PROCEDURE sales.myproc TO ‘webadmin’@’%’;       
A user successfully connects to the database as webadmin and created a stored procedure named get\_reports.       
The next day, the user logs in again as webadmin and wants to delete the stored procedure named get\_reports, and therefore, issues the following statement:        
USE sales;           
DROP PROCEDURE IF EXISTS get\_reports;       
What is the result of executing the statement?       
A.The user will get an error because he or she did not use the ALTER statement to drop the stored procedure.       
B.The user will get an error because he or she did not put the database name in front of the stored procedure name.       
C.The stored procedure named get\_reports will be dropped.       
D.The user will get an error because he or she does not have the permission to drop stored procedures.        
>>Answer:            
C       

问：输出结果是什么       
答：C.名为getreports的存储过程将被删除        


---
### Question: 17
> A crucial database,‘db\_prod’, just disappeared from your production MySQL instance.       
In reviewing the available MySQL logs (General, Audit, or Slow) and your own applicationlevel logs,       
you identified this command from a customer facing application:         
SELECT id FROM users WHERE login=’payback!’;DROP DATABASE db\_prod;’       
Which three methods could have been used to prevent this SQL injection attack from happening?       
A.writing your client code to properly escape all user input       
B.giving limited privileges to accounts used by application servers to interact with their backing databases       
C.using SSL/TLS on your outward facing web servers (https://) to encrypt all usersessions       
D.using a hashing or encryption method to secure all user passwords in your MySQL tables       
E.removing any remaining anonymous accounts from your MySQL instance       
F.validating all user input before sending it to the database server       
G.changing all passwords for the MySQL account ‘root’@’%’ immediately after losing an employee who knew the current password        
>>Answer:               
A,B,F              

问：如何防止这种SQL注入攻击的发生        
答：              
A.给所有输入用户编写客户代码以正确避开            
B.为应用程序和数据库之间交互的帐户提供有限的特权              
F.验证所有用户发送到数据库的输入内容               



---
### Question: 18
>What is the best method for monitoring Group Replication conflict resolution?       
A.the PERFORMANCE\_SCHEMA tables       
B.the SHOW PROCESSLIST command       
C.the INNODB Lock Monitor details       
D.the SHOW STATUS command       
E.the INFORMATION\_SCHEMA tables        
>>Answer:               
A               

问：解决监视组复制冲突的最佳方法       
答：A.performance\_schema表      


---
### Question: 19
>Which statement best describes the purpose of the InnoDB buffer pool?       
A.It is amount of buffers available during a transaction.       
B.It caches only the indexes for InnoDB tables.       
C.It caches data and indexes for InnoDB tables.       
D.It holds changes made during a transaction before they are written to the log.       
E.It is a pool of memory for SQL query sort operations from within the InnoDB engine.        
>>Answer:              
C       

问：哪条陈述最能说明InnoDB缓冲池的用途        
答：C.它为InnoDB表缓存数据和索引           


---
### Question: 20
>A particular government’s security policy is to have very strict data encryption and safety settings.        
This is done by restricting access based on their own CA authority and limiting access to particular users within a department.       
Which method could be used to restrict access as required?       
A.using GRANT … REQUIRE X509 AND REQUIRE ISSUER ‘/ C=…..’ AND REQUIRE SUBJECT ‘/ C=…..’       
B.using GRANT USAGE, X509, …….ON *.* TO user@remotehost IDENTIFIED BY ‘secret\_password’       
C.using GRANT … REQUIRE SSL for a secure connection       
D.using GRANT USAGE, SSL, …..ON *.* TO user@remotehost IDENTIFIED BY ‘secret\_password’       
>>Answer:           
A                 



---
### Question: 21
>Consider that local disk files are accessible via MySQL with commands such as:               
mysql> LOAD DATA LOCAL INFILE ‘/etc/passwd’ INTO TABLE mypasswords;
What change could be made to stop any breach via this insecurity?                    
A.executing REVOKE LOAD FROM *.*             
B.setting the --local-service=0 option when starting mysqld             
C.executing REVOKE FILE FROM *\_*          
D.executing REVOKE FILE ON *\_* FROM ‘ ‘@’%’           
E.setting the --local-infile=0 option when startingmysqld             
F.setting the --open-files-limit=0 option when starting mysqld          
>>Answer:       
E             



---
### Question: 22
>Which three are key advantages of standard MySQL replication?                      
A.supports native automatic failover                 
B.enables automatic resync of databases when discrepancies are detected               
C.provides arbitrary geographic redundancy with minimal overhead tomaster               
D.synchronously guarantees identical slave copy              
E.is easy to configure and has low performance overhead               
F.can easily add slaves for read scaling             
>>Answer:           
C,E,F                  



---
### Question: 23
>Which MySQL utility program should you use to process and sort the Slow Query Log based on query time or average query time?                  
A.mysqldumpslow             
B.mysqldump             
C.mysqlaccess             
D.mysqlshow             
E.mysqlslow              
>>Answer:              
A             



---
### Question: 24
>You are using the Performance Schema to investigate replication on a slave which has a single master.         
The option slave-parallel-type is set to DATABASE.        
Assume that all instruments and consumers are enabled and all threads are instrumented.        
Which two facts can be concluded from the given output?        
A.The salve has two intermediate relay slaves connected to it.        
B.The slave is configured with slave\_parallel\_workers = 4        
C.At most, two schemas are being updates concurrently.        
D.THREAD\_ID 21 has stopped running.        
E.The slave cannot process the relay log fast enough to use all threads.        
F.The server needs more cores to use all slave threads.         
>>Answer:         
B,C        


---
### Question: 25
>A master-slave replication setup has the slave showing this error:         
What could explain this error? (Choose two.)        
A.binlog\_cache\_size=1024 is too small and transactions are lost.        
B.binlog\_format=STATEMENT and a non-deterministic query was executed.        
C.enforce\_gtid\_consistency=ON and consistency is broken between the master and the slave.        
D.The sync\_relay\_log=1000 setting on the slave is too small.        
E.sync\_binlog=0 and the master server crashed.         
>>Answer:         
C,E        
如果是单选，只选 E        


---
### Question: 26
>What two statements are true regarding FLUSH TABLES FOR EXPORT?        
A.It can be used to export TEMPORARY tables.        
B.Table only exports when the table has its own tablespace.        
C.The InnoDB Storage engine must be used for the table being exported.        
D.It is the safest way to extract tables from the shared tablespace.        
E.Partitioned tables are not supported.         
>>Answer:         
B,C        


---
### Question: 27
>Consider the two partial outputs of the SHOW GLOBAL, VARIABLES command from a master and salve server;         
Master :         
Variable\_name	name         
Connect\_timeout	5         
Log\_bin	ON         
Max\_connections	100         
Shared\_memory\_base\_name	MYSQL Server _id	2         
Tmp\_table\_size	5242000         
Version	5,6,10         
>         
>Slave :         
Variable\_name	value         
Connect\_timeout	5         
Log\_bin	OFF         
Max\_connections	10         
Shared\_memory\_base\_name	MYSQL5         
Server\_id	2         
Tmp\_table\_size	4266336         
Version	5,6,13         
>         
>There is a problem with the slave replicating from the master. Which statement describes the cause of the problem?                  
A.The log_bin variable is set to OFF on the slave.         
B.server\_id is not unique.         
C.The max\_connections variable on the slave needs to be increased.         
D.The shared\_memory\_base_name variable must match the master.         
E.The version of the slave is newer that the version of the master.          
>>Answer:          
B         


---
### Question: 28
>The MySQL error log shows:                  
InnoDB: Warning: a long semaphore wait:         
The relevant parts of the InnoDB monitor output shows:         
Which two options would help avoid the long wait in the future?         
A.Increase the value of the innodb\_lock\_wait\_timeout option.         
B.Increase the value of the innodb\_read\_io\_threads option.         
C.Change the table to use HASH indexes instead of BTREE indexes.         
D.Set the value of innodb\_adaptive\_hash\_index to zero.         
E.Deactivate the query cache.         
F.Increase the size of the InnoDB buffer pool.          
>>Answer:          
D,E         


---
### Question: 29
>Examine the mydata table and SELECT statements:         
You issue:         
mysql> begin;         
mysql> update mydata set a=0 where b=3;         
How many rows are now protected by locks with the default InnoDB configuration?         
A.one         
B.one row and a next-key lock for supremum         
C.one row and a gap-lock         
D.five          
>>Answer:          
D         


---
### Question: 30
>You have a consistent InnoDB backup created with mysqldump, the largest table is 50 GB in size.         
You start to restore your backup with this command;          
shell> mysql –u root –p < backup.sql         
>         
>After 30 minutes, you notice that the rate of restore seems to have slowed down.         
No other processes or external factors are affecting server performance.          
Which is the most likely explanation for this slowdown?         
A.The MySQL server has stopped inserting data to check index consistency.         
B.InnoDB is doing CRC32 checks over the tablespace data as it grows.         
C.The MySQL server is taking a periodical snapshot of data so it can resume the restore if it is interrupted mid-way.         
D.InnoDB has filled the redo log and now must flush the pages.         
E.Secondary indexes no longer fit into the buffer pool.          
>>Answer:          
D         



---
### Question: 31
>A simple master-to-slave replication is currently being used.          
>This information is extracted from the SHOW SLAVE STATUS output:         
Last\_SQL\_Error: Error 'Duplicate entry '8' for key 'PRIMARY' ' on query. Default database: 'mydb'.         
Query: 'insert into mytable VALUES ('8', 'George') ' Skip\_Counter: 0         
Retrieved\_Gtid\_Set: 5da6b4f5-6f60-11e8-b2d6-0010e05f3e06: 1-8         
Executed\_Gtid\_Set: 0 25da6b4f5-6f60-11e8-b2d6-0010e05f3e06: 0 21-7         
62706329-6f60-11e8-b64f-0010e05f3e06: 1         
Auto-Position: 1         
You execute a ‘SHOW CREATE TABLE mytable” on the slave:          
CREATE TABLE 'mytable' (         
'ID' int (11) NOT NULL DEFAULT '0' ,         
'name' char (10) DEFAULT NULL, PRIMARY KEY ('ID')         
)         
The table mytable on the slave contains:         
You have issued a STOP SLAVE command.          
You have determined that it is safe to skip the transaction in this case.          
One or more statements are required before you can issue a START SLAVE command to resolve the duplicate key error.         
Which statement should be used?         
A.SET GTID\_NEXT=”CONSISTENCY”; BEGIN; COMMIT; SET GTID\_NEXT=”AUTOMATIC”;         
B.SET GTID\_NEXT=”5da6b4f5-6f60-11e8-b2d6-0010e05f3e06:8”; BEGIN; COMMIT; SET GTID\_NEXT=”AUTOMATIC”;         
C.SET GLOBALSQL\_SKIP\_SLAVE\_COUNTER=1         
D.SET GLOBAL enforce\_gtid\_consistency=ON         
E. SET GTID\_EXECUTED=”5da6b4f5-6f60-11e8-b2d6-0010e05f3e06:8”;         
>>Answer:          
B          


Question: 32

The MySQL installation includes the mysql\_config\_editor utility for managing login paths stored
in a .mylogin.cnf file.
Which two are true about the login path feature?
A.mysql\_config\_editor is the only MySQL-provided utility that can print the values stored
in .mylogin.cnf.
B.A .mylogin.cnf file can store at most one login path.
C.It provides a FIPS-compliant keyring for storing MySQL login details.
D.A .mylogin.cnf file can be edited using a text editor, such as vim or Notepad++.
E.It is an alternative to storing the MySQL login details in a my.cnffile.
F.It provides means to help avoid accidentally exposing the MySQL login details. 答案：EF
Question: 33
What does the possible\_keys column in this output denote?
A.if it is possible for you to include any indexes in your query
B.whether there are any indexes on the tables that you are querying
C.if there are any indexes that may be used to solve this query
D.whether there are any indexes in your query 答案: C

Question: 34
Which two statements are true regarding the creating of new MySQL physical and logical
backups?
A.Physical backups can be used to recover from data corruption.
B.Logical backups are human-readable whereas physical backups are not.
C.Logical backups are always larger than physical backups.
D.Physical backups are usually slower than text backups.
E.Physical backups are usually faster than text backups. 答案: BE
Question: 35
Is it true that binary backups always take less space than text backups?
A.Yes, because binary backups only contain data, and not statements required to insert data into
the tables.
B.No, because text backups can have optimizations, which make them smaller, such as updating
many rows at once.
C.No, because if InnoDB tables contain many empty pages, they could take more space than the
INSERT statements.
D.Yes, because even if InnoDB tables contain many empty pages, text backups have empty

INSERT statements for them. 答案: C
Question: 36
MySQL is installed on a Linux server and has this configuration: [mysqld]
user=mysql datadir=/data/mysql/
As the ‘root’ user, you change the datadir location by executing: shell> cp –R /var/lib/mysql /data/mysql/
shell> chown –R mysql /data/mysql
What is the purpose of changing ownership of datadir to the ‘mysql’ user?
A.MySQL needs to be run as the root user, but files cannot be owned by it.
B.The mysqld process requires all permissions within datadir to be the same.
C.MySQL cannot be run as the root user.
D.MySQL requires correct file ownership while remaining secure. 答案: D
Question: 37
You have the following in your my.cnf configuration file: [mysqld]
default\_authentication\_plugin=sha256\_password
You want to create a new user who will be connecting from the IP address 192.0.2.10, and you
want to use the authentication plug-in that implements SHA-256 hashing for user account
passwords.
Which two statements would create a user named webdesign for this IP address with the
password of imbatman using a SHA\_256 password hash?
A.CREATE USER 'webdesign'@'192.0.2.10' IDENTIFIED AS sha256\_user WITH sha256\_password
'imbatman';
B.CREATE USER 'webdesign'@'192.0.2.10' IDENTIFIED BY 'iambatman';
C.CREATE USER 'webdesign'@'192.0.2.10' IDENTIFIED WITH sha256\_password BY 'imbatman';
D.CREATE USER WITH sha256\_password 'sha256\_user'@'192.0.2.10' IDENTIFIED AS 'webdesign' USING 'imbatman';
E.CREATE USER 'webdesign'@'192.0.2.10' WITH mysql\_native\_password USING SHA265 BY
'imbatman';
F.CREATE USER 'webdesign'@'192.0.2.10' IDENTIFIED BY SHA265 AS 'imbatman'; 答案: BC
Question: 38
You have created a new user with this statement:
CREATE USER ‘erika’@’localhost’ IDENTIFIED BY ‘first#1Pass’ PASSWORD EXPIRE;

What is the outcome?
A.When ‘erika’@’localhost’ tries to log in with the MySQL command-line client, the user will
have to change the password before seeing the mysql> prompt.
B.When ‘erika’@’localhost’ tries to log in with the MySQL command-line client, theuser will not
be permitted to log in because the password is expired.
C.When ‘erika’@’localhost’ tries to log in with the MySQL command-line client, the user will be
permitted to log in but will not be able to issue ant statements until the user changes the
password.
D.You receive a syntax error that indicates that you cannot set a password and expire it at the
same time. 答 案 : C Question: 39
What is the order of tables shown in an EXPLAIN output?
A.It lists tables from the smallest to the largest.
B.It lists tables in the order in which their data will be read.
C.It lists tables from the most optimized to the least optimized.
D.It lists tables in the order in which they are specified in the statement that is being explained.
答案: B
Question: 40
Which three tasks are handled by the optimizer?
A.Decide which indexes to use.
B.Rewrite the WHERE clause.
C.Parse the query.
D.Change the order in which the tables are joined.
E.Validate the query.
F.Execute the query.
G.Verify that the user is allowed to execute the query. 答案: ABD
Question: 41
Suppose you are adding rows to a MyISAM table and the --datadir location runs out of disk space.
What will happen when this occurs?
A.The server will crash.
B.The server suspends that INSERT operation until space becinstallmes available.
C.An error message will be returned to the client .Server Error: ER\_IO
D.The server suspends operations for all storage engines until space becomes available.
答案: B

Question: 42
Consider the table people with the definition:
CREATE TABLE 'people' (
'id' int (10) unsigned NOT NULL AUTO\_INCREMENT, 'FirstName' varchar (40) NOT NULL,
'Surname' Varchar (40) NOT NULL, 'Birthday' date NOT NULL, PRIMARY KEY ('id'),
KEY 'Surname' ('Surname', 'FirstName'), KEY 'FirstName' ('FirstName'),
KEY 'Birthday' ('Birthday')
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4
The application uses a query such as:
SELECT * FROM people WHERE YEAR(Birthday) = 1980; The query is not using an index.
Which two methods can be used to allow the query to use an index?
A.Change the WHERE clause to Birthday BETWEEN 1980-01-01 AND 1980-12-31.
B.Add a functional index for YEAR(Birthday).
C.Execute ANALYZE TABLE to update the index statistics.
D.Add a generated column calculating YEAR(Birthday) and index that column.
E.Add FORCE INDEX (Birthday) to the query. 答案: AD
Question: 43
You back up by using mysqldump.
Which configuration is required on the MySQL Server to allow point-in-time recovery?
A.binlog\_format=STATEMENT
B.log-bin
C.apply-log
D.bonlog\_format=ROW
E.gtid\_enable 答 案 : B Question: 44
Consider the index information for the dept\_emp table in the employee’s schema: Which two conclusions can be made based on the output of the query?
A.There are three indexes on the table.
B.There is a redundant index on the dept\_no column.
C.The secondary indexes are optimized for unique key look-ups.
D.The values on the emp\_no column must be unique.
E.The selectivity of the dept\_no column is the best of the indexed columns.
F.There is a redundant index on the emp\_no column. 答案: AF
Question: 45
old\_alter\_table is disabled as shown.

mysql> SELECT @@old\_alter\_table;
Consider this statement on a RANGE-partitioned table:
mysql> ALTER TABLE orders DROP PARTITION p1, p3; What is the outcome of executing this statement?
A.All data in p1 and p3 partitions is removed and the table definition is changed.
B.All data in p1 and p3 partitions is removed, but the table definition remains unchanged.
C.Only the first partition (p1) will be dropped because only one partition can be dropped at any
time.
D.It results in a syntax error because you cannot specify more than one partition in the same
statement. 答案: A
******* Question: 46
Consider:
Which statement best describes the meaning of the value for the key\_len column?
A.It shows how many bytes will be used from each index row.
B.It shows the number of characters indexed in the key.
C.It shows the total size of the index row.
D.It shows how many columns in the index are examined. 答案: A
Question: 47
Force Majeure is a catastrophic failure on a major level of the database operation.
Regular
backups are key to helping avoid data loss in such situations.
Which two other steps can help avoid data loss in a major catastrophe?
A.Implement a failover strategy to another geographic location.
B.Create a master-master pair for each service.
C.Have a second data centre in a different region or country.
D.Keep software updated to the latest version.
E.Use RAID 10 storage for datA.
F.Use on-site network-attached storage to separate service from datA. 答案: AC
Question: 48
To satisfy a security requirement, you have created or altered some user accounts to include
REQUIRE X509.
Which additional task needs to be performed for those user accounts to fulfill the requirement to
use X509?
A.Install the X509 plug-in on the server.

B.Set the X509 option in the [client] section of the MySQL server’s configuration file.
C.Restart the server with the --require-x509 option.
D.Distribute client digital certificates to the client computers being used to log in by the user
accounts.
E.Provide users access to the server’s private key. 答案: D
Question: 49
Examine the mysqldumpslow output:
Which two options could explain the slow query?
A.There is network congestion between client and server.
B.No index has been defined on the filtered column.
C.There are 108 queries still being executed.
D.A table lock is causing delays.
E.A full table scan is being used. 答案: B,E
Question: 50
Group Replication uses global transaction identifiers to track executed transactions and are
fundamental in avoiding transaction conflict. Which additional three steps help in avoiding
conflicts in group replication?
A.Set isolation level to be SERIALIZABLE.
B.Use the binary log row format.
C.Set isolation level to be READ COMMITTED.
D.Configure IPv6 network for hosts.
E.Guarantee a secondary index on every table. F.Guarantee a primary key on every table.
G. Set multiple slave parallel worker threads. 答案:BFG
Question: 51
You inherited a busy InnoDB OLTP Instance with 100 schemas and 100 active users per schema.
. Total dataset size is 200G with an average schema size of 2G.
. The data is transient and is not backed up and can be repopulated easily.
. Performance and responsiveness of the DB is paramount.
. The query pattern for the DB instance is split 90/ 10 read/ write.
. DB host is dedicated server with 256G RAM and 64 cores.
One of your colleagues made some recent changes to the system and users are now complaining
of performance impacts.
Which four configuration file edits might your colleague have performed to cause the negative

DB performance?
A.table\_open\_cache = 64
B.innodb\_buffer\_pool\_instances=64; innodb\_buffer\_pool\_size=200G
C.log\_bin=mysql-bin; Innodb\_flush\_log\_at\_trx\_commit=1
D.sync\_binlog=10
E.innodb\_flush\_method=O\_DIRECT F.max\_heap\_table\_size = 2G; tmp\_table\_size=2G
G.query\_cache\_size = 2G; query\_cache\_enabled=1
H.innodb\_flush\_log\_at\_trx\_commit=0 答案:ACFG
Question: 52
A MySQL Server has been running an existing application successfully for six months.
The my.cnf
is adjusted to contain this additional configuration:
The MySQL Server is restarted without error.
What effect will the new configuration have on existing account? [mysqld]
default-authentication-plgin=sha256\_password
A.They are not affected by this configuration change.
B.They all connect via the secure sha256\_password algorithm without any configuration change.
C.They will have their passwords updated on start-up to sha256\_password format.
D.They will have to change their password the next time they login to the server. 答案: A
Question: 53
You want to create a temporary table named OLD\_INVENTORY in the OLD\_INVENTORY database
on the master server. This table is not to be replicated to the slave server. Which two changes would ensure that the temporary table does not propagate to the slave?
A.Set binlog\_format=MIXED with the --replicate-ignore-temp-table option.
B.Use the --replicate-do-db, --replicate-do-table, or --replicate-wild-do-table option with the
value equal to OLD\_INVENTORY.
C.Change the binlog\_format option to ROW and restart mysqld before you create the OLD\_INVENTORY table.
D.Stop SQL\_THREAD on the slave until you have finished using the OLD\_INVENTORY temporary
table.
E.Use the --replicate-ignore-table option with the value equal to OLD\_INVENTORY.OLD\_INVENTORY and restart mysqld before creating the temporary table.
答 案 : CE Question: 54

A MySQL replication slave is set up as follows:
. Uses all InnoDB tables
. Receives ROW-based binary logs
. Has the read-only option
The replication slave has been found in an error state. You check the MySQL error log file and find these entries:
2013-08-27 13:55:44 9056 [EROR] Slave SQL: Cloud not execute Write rows event on table test.t1;
Duplicate entry '3' for key 'PRIMARY', Error\_code: 1062; handler error HA\_ERR\_FOUND\_DUPP\_KEY; the event's master log 56\_master-bin.000003, end\_log\_pos 653,
Error\_code: 1062
2013-08-27 13:55:44 9056 [Warning] Slave: Duplicate entry '3' for key 'PRIMARY' Error code:
1062
2013-08-27 13:55:44 9056 [ERROR] Error running query, slave SQL thread aborted.
Fix the
problem, and restart the slave SQL thread with 'SLAVE START'. We stopped at log '56\_master-bin.000003' position 496
What are two possible causes for this error to occur?
A.The applications have the SUPER privilege, which allows them to update rows.
B.The root user on the slave has executed FLUSH LOGS, causing the relay-log to doublewrite.
C.For tables with UNIQUE keys, statement-based replication must be used to maintain integrity.
D.The slave was created with mysqldump –u root -p --skip-lock-tables
-all-databases >/data/data.sql
E.The slave user does not have INSERT, UPDATE, or DELETE permission and cannot execute the
Write\_rows function. 答案: AD
Question: 55
You are no longer able to log in to an existing MySQL Server because the root password credentials not working. You need to reset the root password to complete various administrative
tasks. What are the two major methods that will achieve this?
A.Start the MySQL Server in --safe-mode, which only loads the privilege system for changes as
data is inaccessible.
B.Start the MySQL Server with reset-root-password in my.cnf, which will prompt you to enter a
new root user password.
C.Start the MySQL Server with --init-file pointing to SQL that executes an ALTER USER statement

to change the root user password.
D.Start the MySQL Server with --skip-grant-tables and execute SQL, which will update the root
password.
E.Start the MySQL Server with –initialize-insecure to force a password reset procedure on the
command line. 答 案 : CD Question: 56
You are contacted by a user who does not have permission to access a database table.
You
determine after investigation that this user should be permitted to have access and so you
execute a GRANT statement to enable the user to access the table. Which statement describes the activation of that access for the user?
A.The access does not take effect until the user logs out and back in.
B.The access does not take effect until the next time the server is started.
C.The access is available immediately.
D.The access does not take effect until you issue the FLUSH PRIVILEGES statement. 答案: C
Question: 57
An existing master-slave setup is currently using a delayed replication of one hour.
The master
has crashed and the slave must be "rolled forward" to provide all the latest dats. The SHOW SLAVE STATUS indicates these values:
*RELAY\_LOG\_FILE=hostname-relay-bin.00004
*RELAY\_LOG\_POS=1383
Which command set would make the slave current?
A.STOP SLAVE; CHANGE MASTER TO MASTER\_DELAY=0; RELAY\_LOG\_FILE 'hostname-relay-bin.00004', RELAY\_LOG\_POS = 1383;
B.STOP SLAVE; CHANGE MASTER TO RELAY\_LOG\_FILE = 'hostname-relay-bin.00004',RELAY\_LOG\_POS = 1383;
C.STOP SLAVE; CHANGE MASTER TO MASTER\_DELAY=0; START SLAVE;
D.STOP SLAVE; SET GLOBAL master\_delay=0; START SLAVE; 答案: C
Question: 58
You enable binary logging on MySQL Server with the configuration: binlog-format=STATEMENT
log-bin
Which database updates are logged on the master server to the binary log by default?
A.all updates except to the TEMPDB database
B.all updates except to the PERFORMANCE\_SCHEMA database
C.all updates not involving temporary tables
D.all updates to the default database, except temporary tables

E.all updates to all databases 答案: B
Question: 59
An admin attempts to enforce stronger security by using these commands:
The admin then leaves the system running with the specified changes. What are two remaining
security concerns?
A.validate\_password\_policy cannot be set without restarting the MySQL instance.
B.The name of the dictionary file is too obvious.
C.The dictionary file word list is too short.
D.validate\_password\_dictionary\_file cannot be set without restarting the MySQL instance.
E.The validate\_password plug-in has not been loaded.
F.The dictionary file is an insecure location. 答案：CF
Question: 60
One of your colleagues is trying to make a change using the mysql command-line client for his or her application session.
The colleague instant messages you this command:
mysql> SET SESSION max\_connections = 200; Why does the command fail?
A.max\_connections requires the GLOBAL scope.
B.Its current user does not have the SUPER privilege.
C.max\_connections is not a dynamic variable. You need to change the config file and
restart the database.
D.Users can control only the max\_user\_connections variable. 答案: A
Question: 61
A MySQL server was initialized with separate UNDO tablespaces. Users complain that when they
roll back large transactions, the time to process the request takes too long. The DBA would like to
move the MySQL InnoDB UNDO tablespace to a solid-state drive (SSD) for better performance.
Is this possible and how?
A.Yes. Shut down the mysqld process, enable the transportable\_tablespace option, and move
the UNDO directory to the SSD.
B.Yes. Shut down, copy the UNDO tablespaces to the new location, and change the innodb\_undo\_directory value in your my.cnf.
C.No. The UNDO tablespaces must remain on the same file system as the system tablespaces.

D.No. The sequential write pattern of the UNDO tablespaces is not supported on modern SSD
block devices. 答 案 : B Question: 62
Which two conclusions can be made from the output?
A.There are 140 Performance Schema threads at the time of the output.
B.There are 510 connections to MySQL at the time of the output.
C.The thread cache has been configured with thread\_cache\_size set to at least 6.
D.There are more connections being idle than executing queries.
E.All max\_connections were in use at 2018-03-22 14:54:06 答案: CD
Question: 63
You have a MySQL instance with the following variables in the /etc/my.cnf file: You issue these statements:
USE prices;
UPDATE sales.january SET amount=amount+1000;
An hour after excluding the statements, you realize that you made a mistake and you want to go
to the binary log and look at the statements again. Which statement is true? (Choose one.)
A.You would receive an error on the statement because you cannot update a different database
that what is specified with the USE statement.
B.The changes caused by the UPDATE statement are logged to the binary log because the
instance is using --binlog-format = ROW
C.The statement would fail because you cannot update more than one row at a time when using
–binlogformat = ROW.
D.Nothing is logged because you are executing an UPDATE statement that will cause changes to
more than one row, and you do not have the --binlog-format value set to STATEMENT.
E.Nothing was written to the binary log because you cannot perform a calculation in a query
without enclosing the statement in single quotation marks. 答案: d
Question: 64
Which two statements describe how InnoDB recovery works?
A.InnoDB handles most crash recoveries automatically.
B.InnoDB blocks some operations when innodb\_force\_recovery is set to greater than 0.
C.There will in general be lost committed transactions after a crash using the defaultsettings.

D.It is required to enable binlog\_gtid\_simple\_recovery to perform a crash recovery.
E.It is recommended to set innodb\_force\_recovery = 1 as part of normal operations.
F.It is always required to enable innodb\_force\_recovery to perform a crash recovery.
答 案 : AB Question: 65
Which are three facts about backups with mysqldump?
A.will lock all storage engines for duration(期间) of backup
B.can back up a remote database server
C.allow a consistent backup to be taken
D.are able to back up specific items within a database
E.create automatically compressed backups
F.are always faster to restore than binary backups 答案: BCD
Question: 66
Consider the join\_buffer\_size parameter in MySQL Server. Which two statements are true about the join buffer?
A.The value should be increased if the client performs several SELECT operations.
B.The join buffer is set per connection.
C.The join buffer is used to process sorts when complex joins are being performed.
D.The value should be increased from the default if the query joins large rows without using an
index.
E.The join buffer is global and can be changed only by restarting the server. 答案: BD
Question: 67
After analysis on the slow query log on a high-end OLTP service, the table identified in the slow
queries is:
What are the two most likely reasons for the slowness given this output?
A.Date should be a TIMESTAMP field for better performance.
B.The User field is too long for most names.
C.The engine type is not appropriate to the application use.
D.Using default values for DATETIME causes table scans.
E.No indexes are defined. 答案: CE
Question: 68
Due to an authentication plug-in that is used on the server, passwords are required to be sent as
clear text as opposed to the usual encrypted format.
Which two methods would allow the mysql client to connect to the server and send clear text
passwords?

A.mysql --protocol=PLAIN –uroot –p –h dbhost.example.com
B.INSTALL PLUGIN mysql\_cleartext\_password SONAME ‘mysql\_cleartext\_password.so’;
C.export LIBMYSQL\_ENABLE\_CLEARTEXT\_PLUGIN=’Y’
D.SET GLOBAL mysql\_cleartext\_passwords=1;
E.mysql --enable-cleartext-plugin –uroot –p –h dbhost.example.com 答案: CE
Question: 69
Which three options are most likely to be changed for production form their default values?
A.innodb\_buffer\_pool\_size
B.max\_connections
C.join\_buffer\_size
D.character\_set\_system
E.innodb\_log\_file\_size
F.max\_user\_connections
G.port 答案: AEG
(如果没有 port，选 max\_connections) Question: 70
These details are shown when logged in to an account:
Which set of statements would match the accounts shown?
A.mysql> CREATE USER ‘employee’@’localhost’ IDENTIFIED BY ‘more\_secrets’; mysql> CREATE USER ’’@’’ IDENTIFIED BY ‘valid\_password’ WITH PROXY ‘employee’@’localhost’;
B.mysql> CREATE USER ‘employee’@’localhost’ IDENTIFIED BY ‘more\_secrets’; mysql> GRANT PROXY ON ‘employee’@’localhost’ TO ‘robert’@’localhost’;
C.mysql> CREATE USER ‘robert’@’localhost’ IDENTIFIED BY ‘secret\_password’; mysql>CREATE USER ‘employee’@’localhost’ IDENTIFIED BY ‘more\_secrets’;
D.mysql> CREATE\_USER ’’@’’ IDENTIFIED WITH authentication\_pam ACCOUNT LOCK; mysql> CREATE USER ‘employee’@’localhost’ IDENTIFIED BY ‘more\_secrets’; mysql> GRANT PROXY ON ‘employee’@’localhost’ TO ’’@’’;
答 案 : D Question: 71
After rebooting the host, you attempt to start the mysqld service. You get the following error:
Can’t start the server: Bind on TCP/ IP port: Address already in use What is the most likely cause of this error?
A.The mysql service has already been started on the same port.
B.The network service process in the server is frozen, so all TCP/ IP connections are paused and
cannot be reused.
C.You failed to specify the port number 3306 to the command to start the server, so it is
defaulting to port 80, which is in use by the built-in web server.

D.The /etc/hosts file does not have a valid IP entry for mysqld localhost, so it is binding to
127.0.0.1, which is already in use.
E.The mysql.sock file in the MySQL /tmp directory was not removed after the reboot, so mysqld
still thinks there is an active server running. 答案: A
Question: 72
The /myfolder/my.cnf file has option set:
[mysqld] skip-log-bin
/myfolder2/my.cnf has this option set:
[mysqld]
log-bin = /valid/path/to/mysqlbinlog
All mentioned paths are accessible to the account that you are currently using.
Assume that any
other options mentioned in either file are valid and legal option definitions. You start an instance by using this command line:
mysqld --defaults-file=/myfolder/my.cnf --defaults-extra-file=/ myfolder2/my.cnf
What is the outcome?
A.MySQL starts and Binary Logging is enabled.
B.MySQL fails to start due to the conflicting options in the configuration files.
C.MySQL fails to start due to conflicting options on the command line.
D.MySQL starts but Binary Logging is disabled. 答案: D
Question: 73
You will configure a MySQL Server to act as a replication master. Which two options must
be configured
correctly to allow this?
A.log-master-updates
B.rpl-recovery-rank
C.server-id
D.enable-master-start
E.log\_bin
F.master-logging 答 案 : CE Question: 74
When you examine a new MySQL installation with default configuration, you find a file called
ibdata1 in the database directory. Which two statements are true about this file?
A.it contains the binary log.
B.it contains a general tablespace.

C.it is the default location for all new tables that you create.
D.it contains the system tablespace.
E.it contains the redo log.
F.it contains the undo log. 答案: DF
Question: 75
Which two methods accurately monitor the size of your total database size over time?
A.monitoring the Innodb\_rows\_inserted status variable
B.monitoring the innodb\_redo\_log\_size variable
C.monitoring the information\_schemA.TABLES table
D.monitoring datadir size in the operating system
E.monitoring cumulative Innodb\_page\_size increase
F.monitoring the performance\_schema\_hosts\_size variable 答案: CD
Question: 76
You attempt to connect to a MySQL Server by using the mysql client program. However, you
receive this notice:
What would you run to fix the issue?
A.the mysql\_upgrade script
B.the mysql client with the --ignore-password-hashing option
C.the mysql\_secure\_installation script to update server security settings
D.the mysql client with the --enable-cleartext-plugin option
E.the install plugin command for the mysql\_cleartext\_password plugin 答案: D
Question: 77
On a master server that is using statement-based replication, a table of log data has become very
large. You decide to delete 100.000 rows.
Which two methods can be independently invoked to ensure that the delete is properly propagated to the slave? (Choose two.)
A.Change the replication mode to mixed before issuing any delete statements when the limit
clause is used.
B.If the data modification is non-deterministic, the query optimizer will resolve any potential
issues.
C.Use the limit clause to limit the deletion to 100.000 rows.
D.Use the limit clause in conjunction with the order by clause. 答案: AD
Question: 78
An administrator installs MySQL to run under a mysql OS account. The administrator decides to

disable logins to the mysql account by using /nologin or /bin/false as the user's shell setting.
Which statement is true?
A.The mysql user needs a login and its home directory must be the base directory of the
installation.
B.The OS needs to allow logging in as mysql so that administrative tasks can be performed.
C.This prevents mysqld from starting when standard startup scripts are used.
D.This prevents creation of a command shell with the mysql account, while allowing mysqld to
run.  答案: D
Question: 79
You have a server that has very limited memory but has a very large table. You will use mysqldump to backup this table.
Which option will ensure mysqldump will process a row at a time instead of buffering a set of
rows?
A.--tab
B.--single-transaction
C.--quick
D.--skip-buffer 答 案 : C Question: 80
Which statement is true about using Microsoft Windows Cluster as a platform for MySQL?
A.It relies on the shared disk architecture being visible to both servers.
B.It is provided by means of IP-level disk replication.
C.It implements High Availability by using the NET Connector's load balancing capabilities.
D.It is a shared-nothing architecture. 答案: A
Question: 81
Consider the CHECK TABLE command.
In which two situations should this command be used? (Choose two.)
A.to find out why a query takes a long time to execute on a given table
B.to make sure a table has no structural problems
C.to improve performance by updating index distributing statistics on InnoDB tables
D.to repair table structure problem
E.to make sure that no table indexes are corrupted 答案: BE
Question: 82

You are using replication and the binary log files on your master server consume a lot of disk
space.
Which two steps should you perform to safely remove some of the older binary log files? (Choose
two.)
A.Execute the PURGE BINARY LOGS NOT USED command.
B.Edit the .index file to remove the files you want to delete.
C.Ensure that none of the attached slaves are using any of the binary logs you want to delete.
D.Remove all of the binary log files that have a modification date earlier than today.
E.Use the command PURGE BINARY LOGS and specify a binary log file name or a date and time
to remove unused files. 答案: CE
Question: 83
What are three methods to reduce MySQL server exposure to remote connections?
A.Setting --skip-networking when remote connections are not required
B.Using the sql\_mode=STRICT\_SECURE after connections are established for encrypted
communications
C.Setting specific GRANT privilege to limit remote authentication
D.Setting --mysql\_secure\_configuration to enable paranoid mode
E.Using SSL when transporting data over remote networks 答案: ACE
Question: 84
Which two are considered good security practices when using passwords? (Choose two.)
A.Use one-way encryption for storage of passwords.
B.Store passwords external to the database.
C.Choose short passwords to save on storage space.
D.Use simple keyboard actions that give mixed letters.
E.Do not use dictionary-based words. 答案: AE
2019 年 2 月份新题
Question: 85
This output is from a SHOW SLAVE STATUS:
What would cause the SQL\_Delay variable to have a value of 360? 答案为 B
B) the slave was configured for delayed replication with a delay of six minutes 答案: B
Question: 86

Which MySQL utility copies the master instance to a slave instance on the same host?
A) Mysqlserverclone 答案: A
Question: 87
SQL injection is a common security threat.
Which two methods would help protect against this risk?
A) using prepared statements to handle unsecured values D）Using stored procedures to validate values that are input 答案 AD
答 案 : AD Question: 88
Given the result of this query:
Mysql>select host, user from mysql.user;
......
A client connection is established with the username mike from the host db.example.com.
However, when trying to execute queries, it is found that the privileges are insufficient.
D) ‘mike’#’%’ 答案: D
Question: 89
Which two methods will provide the total number of partitions on a table?
C) use the command: show create table
E) Query the INFORMATION\_SCHEMA.PARTITIONS table 答案: CE
Question: 90
You want to dump only data from the userdata table.
which mysqldump command argument is required to accomplish this?
A) --no-create-info to skip writing CREATE TABLE statements 答案: A ， 实际答案跟图片不一样。
Question: 91
While attemping to set up a new replication slave on host ‘192.168.0.25’ with user ‘replication’
ERROR 1218 (0BS01): error connetcing to master...not allowed What shoud you do to resolve this error?
C) add the user r eplication@192.168.0.25 with the correct password to the master 答案: C
Question: 92
A master-slave replication setup has the slave showing this error: [ERROR] slave I/O: got fatal error 1236 ... ERROR\_code: 1236
Mysql-bin.000033 position 4621679 What could explain this error?
B) sync\_binlog=0 and the master server crashed 答案: B

Question: 93 Consider:
Mysql>explain select name from country where population between 1 and 10000\c
......type: range....
What does the range value in the type column mean?
A) you can use an index and return rows that fall with a range of values 答案: A
Question: 94
Your developer have created a highly normalized schema that requires complex queries with
many join operations to retrieve data.
What information will you use to determine an optimum value for --join-buffer-size?
C) the size of the largest table in any JOIN query 答案: C
Question: 95
You have a mysql instance with the following variables in the /etc/my.cnf file: Binlog-format=ROW
Binlog-ignore-db=sales
You issue these statements:
Use prices;
Update sales.january set amount=amount+1000;
...
E) nothing is ignored because you are executing an UPDATE statement......
答 案 : E Question: 96
Why should you be selective when granting the PROCESS privilege to an account?
C) it allows a client to see another user’s queries with the SHOW PROCESSLIST command 答案: C
Question: 97
In which two situations would you use unencrypted data transfers from the MySQL service?
C)when highest possible speed of transfer is required regardless of security
D)when the service is using socket-only connections and the host is secure 答案: CD
Question: 98
Which two statements are true regarding MYSQL security?
D)the mysqld process owner should own all files and directories to which the server writes
E)the mysqld process should not be run as root or administrator 答案: DE
Question: 99
You have created a backup of the ‘sales’ database with the command: Mysqldump -u root -p --tab=/backup sales
Which two procedures can be used to restore the ‘orders’ table from the backup?

A) shell$ mysql -u root -p sales < /backup/orders.sql Shell$mysqlimport -u root -p --local sales /backup/orders.txt
D)mysql> use sales Mysql>source /backup/orders.sql
Mysql>load data local infile ‘/backup/orders.txt’ into table orders 答案: AD
Question: 100
An employee cannot access the company database. You check the connection ... Mysql> Show global variable like ‘%connect%’;
Connect\_timeout... Init\_connect...
Max\_connect\_errors...
What is a valid explanation for why one of ...
E)key is already connected elsewhere ... 答案: E
Question: 101
What are two benefits of using the --tab option with mysqldump?
A) the schema and data are automatically dumped to separate files
C) it is possible to restore the data in parallel 答案: AC
Question: 102
You want to create the first configuration file for a new installation of MYSQL Start mysqld manually
Stop mysqld using mysqladmin
Interact with mysqld by using only the command-line client mysql
Which option identifies a maximal set of sections where you can put the “max\_allowed\_packed=16M” parameter without creating a problem?
B) [mysql] and [mysqld] and [mysqladmin] 答案: B
Question: 103
Which statement is correct about how InnoDB storage engine uses disk space?
B) It stores data, index and undo information in tablespace file(s). 答案: B
Question: 104
The MySQL user ‘adam’ currently has USAGE permissions to the database.
The football database is transactional and has non-stop updates from	by using
the
--single-transaction option.
Which extra GRANT permissions are required for adam to take mysqldump backups?
A)the ‘adam’ user must also have SELECT on the football database for backups to work
答 案 : A Question: 105

You need to dump the data from the master server and import it into a new slave server.
Which mysqldump option can be used when dumping data from the master server in order to
include the information?
B)master-data 答 案 : B Question: 106
Which statement describes how the relay log works?
D) when a slave receives a change from the master, it is recorded in the relay log first and
processed later 答 案 : D Question: 107
The stored function year\_to\_date is created in the money database by the ‘root’ @’localhost’
account as:
Create function year\_to\_date()
...
What is the outcome if a client connects with the account ‘joe’@’localhost’ and calls the
year\_to\_date function?
B) the function does not execute because the account ‘joe’@’localhost’ does not have the
EXECUTE privileges on the year\_to\_date function 答案: B
Question: 108
You have just created a replication slave from a backup of the master made with mysqldump:
Mysqldump -u backup -p --all-databases > /backups/mysql.sql
...
ERROR 1045 (28000): access denied for user ‘application’@’localhost’
...
Which two changes to the process can fix the issue? B)use the --flush-privileges with mysqldump
D)after the restore, log in to the database and execute FLUSH PRIVILEGES. 答案: BD
Question: 109
You are receiving complaints from your application administrators that they are seeing periodic
stalls...
Which 2 things should you investigate?
A) check the rate of change in the status value Qcache\_hits and compare that to the rate of

change of Qcache\_not\_cached
E) check the rate of change in the status value select\_scan and compare to the rate of change in
com\_select 答案: AE
Question: 110
Examine the ouput below:
Mysql > SELECT FILE\_NAME, TOTAL\_EXTENTS * EXTENT\_SIZE AS `size`
-> FROM INFORMATION\_SCHEMA.FILES
-> WHERE FILE\_NAME LIKE ‘%employees%’;
Which statement is true?
A)The salaries table is getting the largest number of changes to the data.
B)The departments and dept\_manager tablespace storage is small.
C)The departments and dept\_manager tables do not need to be backup up.
D)The departments and dept\_manager tables are empty (D)
Question: 111
You have a scheduled tash on Linux that executes mysqldump against the localhost server
periodically.
When checking the logs of this event to ensure that things are working and that backups will
restore, you notice an output that is concerning.
The command the scheduled task is executing as follows:
$ mysqldump –u backupuser –h 127.0.0.1 –pt100043va living –protocol=TCP >
/backups/latest.sql
Warning: Using a password on the command-line interface can be insecure. Which two methods are available to avoid the warning?
A)Connect through the –socket rather than the default –protocol=TCP for the local connection.
B)User mysql\_config\_editor,Which allows you to store encrypted login credentials in your home
directory.
C)Store your password in an option file eg:~/.my.cnf and use –defaults-file so that it is read and
used. [client]
password = t100043va
D)Use the password validation plugin available to improve user name and password strength
(B,C)
Question: 112
What are three facts about backups with mysqldump?
A)can back up a remote database server

B)allow a consistent backup to be taken
C)are always faster to restore than binary backups
D)create automatically compressed backups
E)are able to back up specific items within a database
F)will lock all storage engines for duration of backup (A,B,E)
Question: 113
Consider these global status variables： mysql> SELECT *
FROM performance\_schema.global\_status WHERE VARIABLE\_NAME LIKE ‘%connection%’ OR VARIABLE\_NAME LIKE ‘%thread%’;
Which tow conclusions can be made from the output?
A)There are 140 Performance Schema threads at the time of the output.
B)The thread cache has been configured with thread\_cache\_size set to at least 6.
C)There are more connectionsbeing idle than executing queries.
D)There are 510 connections to MySQL at the time of the outpu.
E)All max\_connections connections were in use at 2018-03-22 14:54:06. (C,E)
\_i n s t anc e' s : l a st

connections t
Consider these global s ta tus , variables:
mysql> s 正 西
Performance\_sch ema—t hr ead\_cl asses· l os,t Performance\_schema\_t hr ead · , 一
Slow\_launch\_threads

Threads\_cached
Thr eads—c onn ec t ed Threads created
Which two conclusions can be made f rom the output?
A) There are 140 Perf ormance Schema th 口 B) The thread cache has been reads clt th, e time of 廿
C) There are more configured wfth thiead\_cache connections
D) There are 510 eing idl'e than executing querie ,
E) All max\_connect·

O MySQL at the t·1i1m e of th e , outpu
0 5 45 4 oo6111 工 on,s conflections were i,n u se , at 2 o18 -03-22
Question: 114
A MySQL 5.6 replicatoin master is set up by using global transaction identifiers (GTIDs). You
execute this statement:
Mysql> CREATE TABLE datatarget SELECT * FROM datasource; ERROR 1786 (HY000): CREATE TABLE ... SELECT is forbidden when @@GLOBAL.ENFORCE\_GTID\_CONSISTENCY = 1.
Why is this statement forbidden?
A)GTIDs have detected that a slave is inconsistent and therefore, disallow updates until the
problem is resolved.
B)The datasource table is using an older InnoDB tablespace format, which is not compatible
with GTIDs.
C)The datasource table is using the MyISAM engine, which is not compatible withGTIDs.
D)GTIDs require START TRANSACTION before each statement.
E)The statement cannot be logged in a transactionally safe manner. (E)
Question: 115
You notice in your MySQL error log that there are frequent sort aborted client errors.Which two
are potential causes of this error?
A)Atransaction was rolled back.
B)A client was killed during a sort operation.
C)The sort was too large for sort\_buffer\_size, causing an error.
D)The host server has run out of memory for sort operations. 答案: BC
Question: 116
The InnoDB tablespace is corrupted and you start the server with option – innodb\_force\_recover=4

Which backup method would you use to reload the corrupted InnoDB tables?
A) A text backup. A binary backup will still contain the corrupted segments. 答案: A
Question: 117
While reviewing the MySQL error log, you see occasions where MySQL has reached the number
of file handles allowed to it by the operating system. Which method will reduce the number of file handles in use?
D) disconnecting idle localhost client sessions 答案: D
Question: 118
Question: 119
You have forgotten the root user account password. You decide to reset the password and
execute:
shell> /etc/init.d/mysql stop
shell> /etc/init.d/mysql start –skip-grant-tables Which additional argument makes this operation safer?
B) –skip-networking, to probibit access from remote locations 答案: B
Question: 120
You created a backup of the world database with this command： shell> mysqldump –opt world > dump.sql
Which two will import the data from dump.sql?
A)mysql> USE test; mysql> SOURCE dump.sql;
B)shell> mysqlimport test dump.sql
C)shell>mysql test < dump.sql
D)mysql> USE test;
mysql> LOAD DATA INFILE ‘dump.sql'
E)shell> mysqladmin recover test dump.sql 答案: BD
Question: 121
The ‘applicationdb’ is using InnoDB and consuming a large amount of the system space.
D) Take a backup, stop the server,remove the data files, and restore the backup: 答案: D
The'applicationdb'is using InnoDB and consuming a large amount of file system space. You havea
/backup part
You investigate and gather this information:
[mysqld]
dat adi r=/ var / l i b / mys ql / innodb_file_per_table=O
Three tables are stored in the InnoDB shared tablespace _and the details are as follows:
•The table data_cu.rrent has 1,000,000 rows.

•The table data_reports has 1,500,000rows .
•The table data_archive has 4,500,000 rows.
shell> ls -1 /var/lib/mysql/
- rw- 工 w- - - - 1 mysql mysql 744G Aug 26 14:34 ibdatal
-rw-rw---- 1 mysql mysql 480M Aug 26 14:34 ib_logfileO
-rw-rw---- 1 mysql mysql 480M Aug 26 13:47 ib_logfilel
You attempt to free space from ibdatal by taking a mysqldump 0 f the data_archive table and storing it on your
shell> mysqldump -u root -p applicationdb data_archive mysql> DROP TABLE data_archive;
> / bac kup/ da t a_ar chi ve .s ql
Unfortunately, this action does not free any actual disk space back to the file system and the server disk space is
Which set of actions will allow you to free disk space back to the filesystem?
2019 年 10 月新增题： Question:122.
You have taken a Logical Volume Manager (LVM) snapshot backup of a volume that contain the MySQL
data directory. 73 / 87
Why is it important to remove snapshots after completing a raw backup in this way?
A)The snapshots take a significant amount of disk space because they are a duplicate
copy of the data.
B)The system keeps a copy of changes in memory and can cause an out-of-memory event.
C)The snapshot size will continue to grow as changes to the volume are made.
D)The system can only support one snapshot per volume, and you need to remove itto be
able to take your next backup. 答案：：A
Question:123.
What are three methods to attempt SQL injection?
A)Resend form data submitted using the POST method.
B)Include single and double quotes in the submitted data.
c) Enter non-numeric values in numeric fields.
D)Modify the URL using percent encoding.
E)Enter falsified values of the correct data type.
F)Enter numeric values into text fields.
答案：：ABD，（There's no answer at the moment. Free play.） Question:124.
Which two statements are true about MySQL when it has been started using the
--skip-grant-tables option?

A)All users have unrestricted acess.
B)Only the password for active account can be changed.
c) All connections succeed regardless of the username and password
D)User authentication is based on the operating system usemame
E)MySQL becomes read-only except for setting passwords. 答案：：AC （There's no answer at the moment. Free play.） Question:125.
You have intalled the validato password plug in and set the validato_ password policy variable.Which validation is aff
ected by the validate passvord policy etting?
A)whether a new password is rejected if it contains the current user’s username
B)whether a new password is rejected if it contains a word found in a dictionary file
c) the length of time before a newly created password expires
D) the amount of delay after an icorrect password is entered 答 案 ：：B（There's no answer at the moment. Free play.） Question:126.
You have issued this statement:
GRANT PROXY ON ‘a’ FOR ‘b’;
When user account ‘b’ issues a query, the query returns an access denied error. What could have caused that error?
A)User account ‘b’ has not been granted permission to access the data being queried.
B)User account ‘a’ has not been granted permission to access the data being queried.
c) You have not set the proxy. user variable in the configuration file.
D) When conecting, user account ‘b’ is not entering the correct password for user account ‘a’;
答案：：B（There's no answer at the moment. Free play.） Question:127.
A MySQL instance ls running on a
dedicated server .Developers access the server from the same network subnet.Users access the datebase through an
application that is running on a separate server in a DMZ. Which two wl optmze the secuty of this setp
A)enabling and using SsL for conetions to the MysQL datbs
B)disabling connections from named pipes or socket files( depending on the operating system of the server)
c) running the server with --skip -networking speified
D)starting the server with --bind-addross=o.ooo specifled
E)installing MySQL on the application server, and running the database and appiation on the
same server

F)limiting logins to originate from the appliation server or the server’s subnet
答 案 ：A B Question:128.
Which two methods provide a consistent backup of InnoDB tables?
A)mysqldumpslow
B)mysqlhotcopy
c) file system snapshots
D)MySQL Enterprise Backup
E)mysqldump with --binary-data option 答案： D, 多选则为 CD
Question:129.
Which two actions can you take to stop any access from the user?
A)Use DROP USER ’mike‘@’ client.example.com‘;
B)Use ALTER USER ’mike‘@’client . example.com‘ PASSWORD EXPIRE;
c) Use GRANT USAGE ON *.* TO ’mike‘@’ client . example.com‘ MAX_ USER_ CONNECTIONS=0;
D)Use REVOKE ALL PRIVILEGES FROM ’mike‘@’client .example.com‘;
E)Use ALTER USER ’mike‘@’client.example. com‘ ACCOUNT LOCK;
F)Execute the mysql_ secure_ installat ion command. 答案： A E
Question:130.
For tables using persistent statistics, what is the outcome of this change?
A)InnoDB no longer automaticall updates index statistics after a CREATE TABLE statement.
B)InnoDB no longer automatically updates index statstics after the table structure is altered.
c)InnoDB no longer automatically updates index statistics after 10% of the rows in a table changeD) InnoDB no longer
automatically updates index statstics after an ANALYZE TABLE statement. 答案： B
Question:131.
Which ALTER TABLE statement will improve the performance of the query?
A)ALTER TABLE ’CountryLanquago‘ ADD INDEX ’idx_OffLang’ (‘Official’, ‘Language’)
B)ALTER TABLE ‘countryLanquago’ ADD INDEX ’idx_ Lang’; (‘ Language’) ; c)AITER TABLE ‘Country’ ADD INDEX ‘idx_ Code’ (‘Code’);
D) AITER TABLE ‘country’ ADD INDEX ‘idx_ NamoCont’ ( ‘Name’,’CountryCode’);答案：B
Question:132.
A)Normalize the data, for example, into a linked table and filter on that table instead.
B)Create prefix indexes of differing lengths. This avoids rewriting the query.

c) Extract the data queried using generated columns, index these, and use the generated column for filtering. I
D)Add a full-text index on the val column and use the MATCH 0 function for the filtering.
E)Add an R-TREE index on the val column and use the MBRContains 0function for the filtering.
F)Convert the data typento binary and add a normal index. This avoids rewriting the query.
答案： A E F Question:133.
At which stage during query processing does MySQL create a query‘s execution plan?
A)Authorizingo
B)Executing
C)Parsingo
D)Optimizing 答 案 ： D Question:134.
In which order does MySQL process an incoming INSERT statement?
A)It writes the query to the binary log, optimizes it, and then checks whether the user is
Authorized to perform the query.
B)It checks whether the user is authorized to perform the query, writes to the blnary log,
and then optimizes it.
c) It optmizes the query, checks whether the user is auhorzed to perform it, and then wrtes to the binary log.
D) it checks whether the user is auhorzed to perfom the query, optimzes it, and then wites to
the binary log. 答 案 ： D Question:135.
The MySQL instance is a default RPM installation on a Linux server. Where are the errors written?
A)in the /var/lib/mysql/ hostname . log fileo
B)in the /var/log/mysqld. err file Io
c) in the syslog daemon on the servero
D) no logging enabled by default 答案： B
Question:136.
You have a config file for a running DB with this excerpt: [mysqld]
tmp_ table_ size= 16M sort_ buffer_ size= 256k

To adre a query, pefomance problem of coneting to the DB from an apiation an another host,
you log in and make these changes to the DB:
mysql> SET GLOBAL tmp_ table_ size= 200000mysql> SET sort_ ,buffer. size= 200000 This solves the problem with your queries. However, later the DB instance is restarted and theperformance problem
retumns.
Which three best describe this scenario?
A)Global variables are not persistent across server restarts.
B)sort_ buffer_ size should match tmp_ table. size to be optimal.
c) The query benefited from sort. buffer_size and tmp. table size increases.
D)Session variables are not persistent across server restarts.
E)The query benefited from tmp_ table. size increaseo
F)The query benefited from sort_ buffer_sizeincrease 答案： ACD
Question:137. table: City Itype: ALL
possible_ keys: NULL key: NULL
key_ len: NULL ref: NULL IOMS: 4079
Extra:Using temporary;Using filesort id: 1
select_ type: SIMPLE table:  Country type: eq_ ref
possible_ keys: PRIMARY key: PRIMARY
key_ len: 3
ref: world.City.Countrycoderows: 1 Extra: Using where;
Distinct
Which statement best describes the meaning of the values in the rof columns?
A)world.City.CountryCode is used as the primary key for the Country table.
B)No indexed columns are used to select rows from the Country table. The world.City.CountryCode column is used to select rows in the city table.
C)No indexed columns are used to select rows from the City table. The world.City.
CountryCodo
column is used to select rows in the Country table.
D)world. city. CountryCode is used to sort the rows in the city table. 答案： C
Question:138.

You need to dump the data from the master server and import it into a new slave server.
Which mysqldump option can be used when dumping data from the master server in order to include themaster s
erver's binary log information?
A)master –binlog
B)include-log-file
C)include-master-info
D)master –data 答 案 ：D Question:139.
Which statement is true about tablespaces?
A)All tables must be in either the system tablespace or a general tablespace.
B)All tablespace files must be in the directory specified by the -- datadir option.
c) The system tablespace can be configured to span multiple files.
D) General tablespaces can be configured to span multiple files. 答案： D
Question:140.
Which two changes to the process can fix the issue?
A)After the restore, log in to the database and execute FLUSH PRIVILEGES.
B)Use the --flush-privileges with mysqldump.
c) Add a second dump for the mysql' database; -all-databases does not include it.
D) Use the --grants option to include GRANT statements in the dump. 答案： A B
Question:141
A)The slave thread is waiting for another event to finish in another slave thread.
B)The binary log on the master is not being updated.
c) The slave is waiting for an event to come into the relay log. 79 / 87
D) The Event Scheduler is not enabled on the slave host. 答案：A
Question:142.
MySQL Server has been intall and the /etc/my.cnf file has been edited.
The server does not start when you attempt to use the start script of the os, but starts only when youprovide all the o
ptions on the command line.You check the /etc/my .cnf file permissions: shells ls -l /etc/my. cnf
- rw-w-rw-.1 root root 345 Nov 18 2016 /etc/my.cnf What is the reason?
A)MySQL is starting via a non-root user when using the init script.

B)MySQL was intalled in a non-default loation, and does not look in
/etc/my.cnf..
c) MySQL ignores world-readable confiuration files as a security measure.
D) MySQL must be started as xoot with this setup. 答案： C
Question:143.
You have successfully provisioned the latest MySQL 5.7 database instance on a physical host, to beadded to an existin
g farm for use in a modern, high volume, ACID
compliant, OLTP website, whichserves hundreds of DML transactions per second. The default values of which two key variables do you change to ensure seamless operation of thedatabase?
A)Binary Log Size
B)InnoDB Redo Log Size
c) Query Cache Size
D)Sort Buffer sizeo
E)Key Buffer Size
F)Buffer Pool Size 答 案 ： D F Question:144.
Which storage option for MySQL data directory typically offers the worst performance in a
Highly concurrent, OLTP-heavy, I0-bound workload?
A)iSCSI Lun
B)battery-backed locally attached RAID 5 arrayo
C)NFS (Networked File System) mounto
D)SAN (Fibre Channel) Lun 答案：A
Question:145.
You are creating a strategy for backing up MySQL using a cold binary backup.
The MySQL Instance is areplication mast
er with global transaction identifiers (GTIDs) enabled and it uses Transparent DataEncryption (TDE). Other than the co
nfiguration required to make the instance a
replication master andenabled GTIDs and TDE, the instance is using all default settings.The requirements for the back
up are:
It must be possible to rebuild the instance using the backup. It must be verified.
It must allow for a catastrophic hardware failure.
Which four steps must be included in the backup strategy?
A)Include the MySQL PID file in the backup.
B)Include the relay logs in the backup.
C)Copy the backup to a remote host.

D)Include the binary logs in the backup:
E)Include the keyring data and/or cofiguation in the backup.
F)Include the ibtmp1 file in the backup.
G)Include the MySQL socket file in the backup.
H)Include the operating system disk encrption key in the backup. I ) Restore the backup to a clean MySQL intane.
答 案 ：CEHI Question:146.
As the root user, you atettemt to stat Mysql and and find this error in the error log:
mysqld: Can’t chang dir to‘/var/1ib/mysql/’(Errcode:13 –Permission denied) The user option is set to mysql in /etc/my.cnf.
What is the reason for this error and how do you fix it?
. A) The owner of /var/lib/myaq1 is root. Change the ownership to myeql and retry the command.B) You forgot to add
datadir/var/1ib/mysql to the cofiguaton
C)You forgot to add password variables to the configuration so it cannot change the user.
D)You should not run the command as root. Running the command as the mysqladmin user will solve the problem.
E)You cannot start MySQL wlthout reating servico values first. Check the pemissions for service
values in /etc/ inet.d to see if the lderet sernce daemons working and try agaln. 答案： A
Question:147.
Which two capabililiese are granted with the SUPER prvlege? A) allowing a client to shut down the server
B) allowing client accounts to take over the account of another user
c) allowing change of the server runtime configuration
D) allowing a client to kill other client connections 答案： A D
Question:147.
Examine this portion of the my.cnf configuration file located in the parent foleder of the mysqld binary,and presume
that remainder of the file is correct. [mysqld]
: port .3306
port - 3307 # 3308
You start a mysqld instance by using this command line: mysqld --defaults- file-../my.cnfWhat is the outcome?
A)MySQL starts and listens for connections only on port 3308.
B)MySQL starts and listens for connections only on ports 3307 and 3308.
c) MySQL refuses to start because relative paths are no allowed.
D)MySQL starts and listens for connections on ports 3306, 3307, and 3308.

E)MySQL starts and listens for connections only on port 3306.
F)MySQL starts and listens for connections only on port 3307.
G)MySQL refuses to start because both lines contain syntax errs. 答案：F
Question:149.
Recently, users on mostly write MySQL database have been cmplanling of slowdowns or stal in theirapplications.
Which option is most likely to have a positive effect on the server’s health and performance?
A)Lower innodb max_ dirty pages pct to flush more often.
B)Move redo logs to /dev/ shm to improve their speed.
c) Reduce the size of redo logs to improve storage eficiency.
D) Increase the size of redo logs. 答案： D
Question:150.
A)The replication slave uses multisource replication with eight sources.
B)The sydney channel is keeping up with the recelved events.
c) The melbourne channel is keeping up with the received events.
D)The last event received from the sydney channel was at 2018-05-08 14:501.
E)The melbourne channel is resolving a GTID conflict. 答案： A
Question:151
A)GRANT SELECT ON world.* TO janeexample. com;
B)GRANT DELETE ON world.* TO jane@example. com;
c) GRANT SELECT ON world.* TO joe@example. com;
D)GRANT SELECT ON world.* To marylexample. com IDENTIFIED BY ‘^jkK2@9bqIm4!jlaN’;
E)GRANT SELECT ON audit.* TO janeexample. com;
F)GRANT INSERT ON audit.* TO jane@example. com;
G)CREATE USER marylexample.com IDENTIFIED BY ‘^jkK2@9bqIm4!jlaN’; 答案：A B C
Question:152.
A)Normalize the data, for example, into a linked table and filter on that table instead.
B)Create prefix indexes of iffering lengths. This avoids rewriting the query.
c) Extract the data queried using generated columns, index these, and use the generated column for filtering.
D)Add a ulltext index on the val column and use the MATCH() function for the filtering.
E)Add an R-TREE index on the val column and use the MBRContains 0 function for the fitein8
f) Convert the data type to binary and add a normal index. This avoids rewriting the query.
答案： A E F

Question:153.
What are three methods to attempt SQL injection?
A)Resend form data submitted using the POST method.
B)Include single and double quotes in the submitted data.
c) Enter non-numeric values in numeric fields.
D)Modify the URL using percent encoding
E)Enter falsified values of the correct data type.
F)Enter numeric values into text fields. 答案：A B D
Question:154.
What are three measures to maintain a stable MySQL system?
A)Ensure all replicas are in the same data center.
B)Ensure redundancy of all parts of the system,
c) Monitor with data collection every second.
D)Take the whole stack into account.
E)Establish a performance baseline.
F)Set configuration options to as large a value as possible. 答案：B C E
Q155
The Mysql user ‘adam’ currently has usage permissions to the database The football database is transactional and has not-stop updates from application users.the
‘adam’ user needs to be able to take consistent backups of the football database by using
the –single-transaction option
Which extra GRANT permissions are required for adam to take mysql dump backups?
A.THE ‘adam’ user must also have select on the football database for backups to work.
B.THE ‘adam’ user must have the super privilege in order to take data backups.
C.HE ‘adam’ user needs the process privilege to be able to take a consistent backup while
other users are connected.
D.HE ‘adam’ user must also have single ppansact on global grant to take a consistent backup.
Answer::A Q156
Which statement best describes a’warm” backup?
A.It only backs up “warm” data,that is,data that has been recently modified.
B.It is similar to a “hot” backup,but differs in that it does not permit write operations.
c. It is similar to a “cold” backup,but differs in that it perits write operations.
D. IT backs up the binary log,which cortains the mos recent “warm” changes. Answer::D

Q157
You have created a backup of the ‘sales’ database with the command: Mysqldump –u root –p –tab=/backup sales
Which two procedures can be used to restore the ‘orders’ table from the backup? A.shell$ mysqldump –u root –p –tab=/backup –restore sales –tables orders
B.shell$ mysql –u root –p sales < /backup/orders.sql shell$ mysql –u root –p sales < /backup/orders.txt
C.mysql>use  sales mysql>SOURCE /backup/orders.sql
mysql>LOAD DATA LOCAL INFILE ‘/backup/orders.txt’ INTO TABLE orders;
D.shell$ mysql –u root –p sales</backup/orders.sql
shell$ mysqlimport –u root –p –local sales /backup/orders.txt Answer::C,D
Q158
What are three typical causes of mysql becoming suddenly slow or unavailable?
A.Monitoring has not enabled all Performance schema instuments.
B.A configuration change was made
C.OPTMIZE TABLE is not executed for the innoDB tables.
D.The hardware includes a single point of failure. E. The application executes a new untested query.
F. The Mysql Query Cache is disabled. Answer::BDF
Q159
You have installed mysql on oracle linux 7 using the official PRM distribution,and
SELinux is set to permissive.
Examine this extract of the my.cnf file. Mysql
Port=3301 Mysqld Port=3303 Replica Port=3304
You issue this command to start mysql server Systemct1 start mysqld@repica
On which port is the server listening? A.3301
B.3303 C.3304 D.3302
Answer::B Q160

Your mysql database is running on linux,and you have the following variable in you're
my.cnf file. Mysqld
Log –error=/var/log/host_name.err
Your mysql error log is very large,and you want to save it and create a new log.
Which set of commands would accomplish this task?
A.From a linux command line;
#mv /var/log/host_name.err /var/log host name.err-old; #mysqladmin flush-logs
B.FROM a mysql command line Mysql>SET SESSION log_syslog=’on’
Mysql>set session log_syslog)fatility=nonate; Mysql>Flus /var log host_name.err;
Mysql>set session log_syslog=’off’
C.From a linux command line #mysqladmin –rorate-log=var log host_name2.err
D.From a mysql command line; Mysql>ROTATE LOSS WITH TI….. MYSQL>FLUSR LOGS;
E.From a mysql command line 85 / 87
Mysql>set gloral ex..logs_days=0l
Mysql>set old_log_file= var log/host_name.err-old’; Mysql>Flush old error logs
MYSQL>reset error logs; Answer::A
Q161
The mysql database includes an innodb table with data stored in strings in the val
column;
Create table ‘t1’
(‘id’ int unsigned not null auto_increment, ‘Val’ varchar(255) default null,
Primary key(‘id’) ) engine=innodb; Some example values are:
Val
/abc/2018-05-21/123/def/
/hfw/2018-05-22/532/faa/inis/ai
/gfd/2018-05-23/5334/gds.hcsd/ab
A typical query using the val column for is  Mysql >select * from t1 where val like ‘%def/%’
Which three changes will alow the use of an index to perform this kind of filtering?

A.Normalize the data,for example,into a liked table and filter on that table instead.
B.Create prefix indexes of diffeng lengths,this avoids rewriting the query.
C.Convert the data type to binary and add a nonal index.this avoids rewiting the query
D.Add an R-TREE index on the val column and use the MBRcontains() function for the
filtering.
E.Add a full-text-index on the val column and use the match Answer::B D E
Q162
WHRER DOES Mysql linux RPM install the mysqld binary? A./USR/BIN/
B./USR/LIBEXEC/ C./OPT/MYSQL/SERVER/BIN/ D./USR/SBIN/ E./USR/LOCAL/MYSQL/BIN/
Answer::D Q163
You are using gtids in replication.You need to skip a transaction with the GTID of aaa
bbb-ccc-ddd-eee :3 on a slave
Which procedure would you execute from a mysql prompt?
A.STOP SLAVE;
SET GLOBAL SQL_SLAE_SKIP_COUNTER=1 START SLAVE;
B.STOP SLAVE; RESET SLAVE BEGIN
SKIP NENT RPID COMMIT;
START SLATE;
C.STOP SLAVE
SET GTID_NEXT ‘aaa-bbb-ccc-ddd-eee:3’ Begin
Commit
Set gttd_nexp=’ACENATIC’ START SLAVE
D.STOP SLAVE BEGIN;
SET GTID_TGNERP=’aaa-bbb-ccc-ddd-eee:3’; Commit;
Start slave; Answer::A

Q164
You are using the mysqldumpslow utility to view the contents of the slow query log
You notice the letter N and the character string ‘s’ in a number of locations in the output.
What does the N indicate?
A an abbreviation for null in a statement
B the name of the user issuing the statement
C an abstracted substitution for numbers induded in where clauses D the number of times the statement was executed.
Answer::D Q165
you want to dump only data from the userdata table
Which mysqldump command argument is required to accomplish this A.—data— only as this specifies that only data is
to be dumped
B.—table=userdata in order to dump only the data from the userdata table C.—NO-CREATE-INFO TO skip writing CREATE TABLE statements
D.—single-transaction as this obtains a consistent view of data only Answer::C
Q166
You want to create the first configuration file for a new installation of mysql You will start mysqld manually(not automate it to start when the host machine starts or
execute as a service)
You will stop mysqld using mysqladmin
You will interact with mysqld by using only the command-line client mysql. Which option identifies a maximal set of sections where you can put the “max_allowed_packet=16m” parameter without creating a problem?
a.mysqld and mysqladmin
b.mysql and mysqld and mysqladmin
c.mysql and mysqladmin
d.mysqld
e.mysql
f.mysql and mysqld
g.mysqladmin Answer::B Q167
What are there typical causes of MySQL becoming suddenly slow or unavailable? A）Monitoring has not enabled all Performance Schema instruments
B）A configuration change was made
C）OPTIMIZE TABLE is not executed for the InnoDB tables D）The hardware includes a single point of failure E）The application executes a new untested query

F）The MySQL Qurey Cache is disabled Answer::B,D,E
Q168
Which statement is true abort the output?
A)The query read data from the data file rather than directly from the buffer pool
B)the time the query too it the … timar_wait values
C)the query did not find its table in the table definition cache
D)the event with event_id=8945 is a child of the event with event_id=8944 Answer::A（There's no answer at the moment. Free play.）
