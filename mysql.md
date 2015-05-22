# 学会使用简单的 MySQL 操作

<span>在前面两个章节中已经介绍过</span><span>MySQL</span><span>的安装了，但是光会安装还不够，还需要会一些基本的相关操作</span><span>。</span><span>当然了，关于</span><span>MySQL</span><span>的内容也是非常多的，只不过对于</span><span>linux</span><span>系统管理员来讲，一些基本的操作已经可以应付日常的管理工作了，至于更高深的那是</span><span>DBA</span><span>（专门管理数据库的技术人员）的事情了</span><span>。</span>

<span>【</span><span>**更改**</span><span>**mysql**</span><span>**数据库**</span><span>**root**</span><span>**的密码**</span><span>】</span>

<span>首次进入数据库是不用密码的</span>

<span>**_/usr/local/mysql/bin/mysql -u root_**</span>

<span>Welcome to the MySQL monitor. Commands end with ; or \g.</span>

<span>Your MySQL connection id is 2</span>

<span>Server version: 5.0.86 MySQL Community Server (GPL)</span>

<span>Type 'help;' or '\h' for help. Type '\c' to clear the buffer.</span>

<span>mysql></span>

<span>现在已经进入到了</span><span>mysql</span> <span>的操作界面了</span><span>。</span><span>退出的话，直接输入</span><span>exit</span><span>即可</span><span>。</span>

<span>mysql></span><span>**_exit_**</span>

<span>Bye</span>

<span>先解释一下上面的命令的含义，</span><span>-u</span> <span>用来指定要登录的用户，</span><span>root</span><span>用户是</span><span>mysql</span><span>自带的管理员账户，默认没有密码的，</span><span>**那么如何给**</span><span>**root**</span><span>**用户设定密码**</span><span>？按如下操作：</span>

<span>**_/usr/local/mysql/bin/mysqladmin -u root password ‘123456’_**</span>

<span>这样就可以设定</span><span>root</span><span>用户的密码了</span><span>。</span><span>其中</span><span>mysqladmin</span><span>就是用来设置密码的工具，</span><span>-u</span> <span>指定用户，</span><span>passwod</span> <span>后跟要定义的密码，密码需要用单引号或者双引号括起来</span><span>。</span><span>另外你也许发现了，敲命令时总在前面加</span><span>/usr/local/mysql/bin/</span> <span>这样很累</span><span>。</span><span>但是直接打</span><span>mysql</span> <span>又不能用，这是因为在系统变量</span><span>$PATH</span><span>中没有</span><span>/usr/local/mysql/bin/</span><span>这个目录，所以需要这样操作</span><span>(</span><span>如果你的</span><span>linux</span><span>可以直接打出</span><span>mysql</span><span>这个命令，则不要做这个操作</span><span>)</span><span>：</span>

<span>**_vim /etc/profile_**</span>

<span>在最后加入一行：</span>

<span>export PATH=$PATH:/usr/local/mysql/bin/</span>

<span>保存后运行</span>

<span>**_source /etc/profile_**</span>

<span>设定完密码后，再来运行最开始进入</span><span>mysql</span><span>数据库操作界面的命令：</span>

<span>**_mysql -u root_**</span>

<span>ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)</span>

<span>就报错了，这是因为</span><span>root</span><span>用户有密码</span><span>。</span>

<span>**_mysql -u root -p_**</span>

<span>Enter password:</span>

<span>Welcome to the MySQL monitor. Commands end with ; or \g.</span>

<span>Your MySQL connection id is 5</span>

<span>Server version: 5.0.86 MySQL Community Server (GPL)</span>

<span>Type 'help;' or '\h' for help. Type '\c' to clear the buffer.</span>

<span>mysql></span>

<span>需要加</span><span>-p</span><span>选项指定密码，这时就会提示你输入密码了</span><span>。</span>

<span>**当设定密码后，如果要想更改密码如何操作呢**</span><span>？</span>

<span>**_mysqladmin -u root -p password "123456789"_**</span>

<span>Enter password:</span>

<span>输入原来</span><span>root</span><span>的密码就可以更改密码了</span><span>。</span>

<span>【</span><span>**连接数据库**</span><span>】</span>

<span>刚刚讲过通过使用</span><span>**_mysql -u root -p_ **</span><span>就可以连接数据库了，但这只是连接的本地的数据库</span><span>’localhost’</span><span>，然后有很多时候都是去连接网络中的某一个主机上的</span><span>mysql。</span>

<span>**_mysql -u user1 -p –P 3306 -h 10.0.2.69_**</span>

<span>其中</span><span>-P</span><span>（大写）指定远程主机</span><span>mysql</span><span>的绑定端口，默认都是</span><span>3306</span><span>；</span><span>-h</span><span>指定远程主机的</span><span>IP</span>

<span>【</span><span>**一些基本的**</span><span>**MySQL**</span><span>**操作命令**</span><span>】</span>

<span>1\.</span> <span>查询当前所有的库</span>

<span>mysql></span> <span>**_show databases;_**</span>

<span>+--------------------+</span>

<span>| Database |</span>

<span>+--------------------+</span>

<span>| information_schema |</span>

<span>| mysql |</span>

<span>| test |</span>

<span>+--------------------+</span>

<span>2\.</span> <span>查询某个库的表</span>

<span>mysql></span> <span>**_use mysql;_**</span>

<span>Database changed</span>

<span>mysql></span><span>**_show tables;_**</span>

<span>+---------------------------+</span>

<span>| Tables_in_mysql |</span>

<span>+---------------------------+</span>

<span>| columns_priv |</span>

<span>| db |</span>

<span>| func |</span>

<span>| help_category |</span>

<span>| help_keyword |</span>

<span>| help_relation |</span>

<span>| help_topic |</span>

<span>| host |</span>

<span>| proc |</span>

<span>| procs_priv |</span>

<span>| tables_priv |</span>

<span>| time_zone |</span>

<span>| time_zone_leap_second |</span>

<span>| time_zone_name |</span>

<span>| time_zone_transition |</span>

<span>| time_zone_transition_type |</span>

<span>| user |</span>

<span>+---------------------------+</span>

<span>3\.</span> <span>查看某个表的字段</span>

<span>mysql></span> <span>**_desc func;_ **</span><span>//func</span> <span>是表名</span>

<span>+-------+------------------------------+------+-----+---------+-------+</span>

<span>| Field | Type | Null | Key | Default | Extra |</span>

<span>+-------+------------------------------+------+-----+---------+-------+</span>

<span>| name | char(64) | NO | PRI | | |</span>

<span>| ret | tinyint(1) | NO | | 0 | |</span>

<span>| dl | char(128) | NO | | | |</span>

<span>| type | enum('function','aggregate') | NO | | NULL | |</span>

<span>+-------+------------------------------+------+-----+---------+-------+</span>

<span>4\.</span> <span>查看某个表的表结构（创建表时的详细结构）</span>

<span>mysql></span> <span>**_show create table func;_**</span>

<span>|Table | CreateTable |</span>

<span>| func | CREATE TABLE `func` (</span>

<span>`name` char(64) collate utf8_bin NOT NULL default '',</span>

<span>`ret` tinyint(1) NOT NULL default '0',</span>

<span>`dl` char(128) collate utf8_bin NOT NULL default '',</span>

<span>`type` enum('function','aggregate') character set utf8 NOT NULL,</span>

<span>PRIMARY KEY (`name`)</span>

<span>) ENGINE=MyISAM DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='User defined functions' |</span>

<span>+-------+----------------------------------------------------------------------------------------------------------------------</span>

<span>5\.</span> <span>查看当前是哪个用户</span>

<span>mysql></span> <span>**_select user();_**</span>

<span>+----------------+</span>

<span>| user() |</span>

<span>+----------------+</span>

<span>| root@localhost |</span>

<span>+----------------+</span>

<span>6\.</span> <span>查看当前所在数据库</span>

<span>mysql></span> <span>**_select database();_**</span>

<span>+------------+</span>

<span>| database() |</span>

<span>+------------+</span>

<span>| mysql |</span>

<span>+------------+</span>

<span>7\.</span> <span>创建一个新库</span>

<span>mysql></span> <span>**_create database db1;_**</span>

<span>Query OK, 1 row affected (0.04 sec)</span>

<span>8\.</span> <span>创建一个表</span>

<span>mysql></span> <span>**_create table t1 ( `id` int(4), `name` char(40));_**</span>

<span>Query OK, 0 rows affected (0.02 sec)</span>

<span>mysql></span> <span>**_desc t1;_**</span>

<span>+-------+----------+------+-----+---------+-------+</span>

<span>| Field | Type | Null | Key | Default | Extra |</span>

<span>+-------+----------+------+-----+---------+-------+</span>

<span>| id | int(4) | YES | | NULL | |</span>

<span>| name | char(40) | YES | | NULL | |</span>

<span>+-------+----------+------+-----+---------+-------+</span>

<span>9\.</span> <span>查看当前数据库版本</span>

<span>mysql></span> <span>**_select version();_**</span>

<span>+-----------+</span>

<span>| version() |</span>

<span>+-----------+</span>

<span>| 5.0.86 |</span>

<span>+-----------+</span>

<span>10\.</span> <span>查看当前系统时间</span>

<span>mysql></span> <span>**_select current_date, current_time;_**</span>

<span>+--------------+--------------+</span>

<span>| current_date | current_time |</span>

<span>+--------------+--------------+</span>

<span>| 2011-05-31 | 08:52:50 |</span>

<span>+--------------+--------------+</span>

<span>11\.</span> <span>查看当前</span><span>mysql</span><span>的状态</span>

<span>**_mysql> show status;_**</span>

<span>+-----------------------------------+----------+</span>

<span>| Variable_name | Value |</span>

<span>+-----------------------------------+----------+</span>

<span>| Aborted_clients | 0 |</span>

<span>| Aborted_connects | 1 |</span>

<span>| Binlog_cache_disk_use | 0 |</span>

<span>| Binlog_cache_use | 0 |</span>

<span>| Bytes_received | 664 |</span>

<span>| Bytes_sent | 6703 |</span>

<span>这个命令打出很多东西，显示你的</span><span>mysql</span><span>状态</span><span>。</span>

<span>12\.</span> <span>查看</span><span>mysql</span><span>的参数</span>

<span>mysql></span> <span>**_show variables;_**</span>

<span>很多参数都是可以在</span><span>/etc/my.cnf</span><span>中定义的</span><span>。</span>

<span>13\.</span> <span>创建一个普通用户并授权</span>

<span>mysql></span><span>** _grant all on *.* to user1 identified by '123456';_**</span>

<span>Query OK, 0 rows affected (0.01 sec)</span>

<span>all</span> <span>表示所有的权限（读</span><span>、</span><span>写</span><span>、</span><span>查询</span><span>、</span><span>删除等等操作），</span><span>*.*</span><span>前面的</span><span>*</span><span>表示所有的数据库，后面的</span><span>*</span><span>表示所有的表，</span><span>identified by</span> <span>后面跟密码，用单引号括起来</span><span>。</span><span>这里的</span><span>user1</span><span>指的是</span><span>localhost</span><span>上的</span><span>user1</span><span>，如果是给网络上的其他机器上的某个用户授权则这样：</span>

<span>mysql></span> <span>**_grant all on db1.* to 'user2'@'10.0.2.100' identified by '123456';_**</span>

<span>Query OK, 0 rows affected (0.00 sec)</span>

<span>用户和主机的</span><span>IP</span><span>之间有一个</span><span>@</span><span>，另外主机</span><span>IP</span><span>那里可以用</span><span>%</span><span>替代，表示所有主机</span><span>。</span><span>例如：</span>

<span>mysql></span><span>** _grant all on db1.* to 'user3'@'%' identified by '123456';_**</span>

<span>Query OK, 0 rows affected (0.00 sec)</span>

<span>【</span><span>**一些常用的**</span><span>**sql**</span><span>】</span>

<span>1\.</span> <span>查询语句</span>

<span>mysql></span> <span>**_select count(*) from mysql.user;_**</span>

<span>mysql.user</span><span>表示</span><span>mysql</span><span>库的</span><span>user</span><span>表；</span><span>count(*)</span><span>表示表中共有多少行</span><span>。</span>

<span>mysql></span><span>** _select * from mysql.db;_**</span>

<span>查询</span><span>mysql</span><span>库的</span><span>db</span><span>表中的所有数据</span>

<span>mysql></span> <span>**_select db from mysql.db;_**</span>

<span>查询</span><span>mysql</span><span>库</span><span>db</span><span>表的</span><span>db</span><span>段</span><span>。</span>

<span>mysql></span> <span>**_select * from mysql.db where host like '10.0.%';_**</span>

<span>查询</span><span>mysql</span><span>库</span><span>db</span><span>表</span><span>host</span><span>字段</span><span>like 10.0.%</span> <span>的行，这里的</span><span>%</span><span>表示匹配所有，类似于前面介绍的通配符</span><span>。</span>

<span>2\.</span> <span>插入一行</span>

<span>mysql></span><span>** _insert into db1.t1 values (1, 'abc');_**</span>

<span>Query OK, 1 row affected (0.00 sec)</span>

<span>t1</span><span>表在前面已经创建过</span><span>。</span>

<span>mysql></span> <span>**_select * from db1.t1;_**</span>

<span>+------+------+</span>

<span>| id | name |</span>

<span>+------+------+</span>

<span>| 1 | abc |</span>

<span>+------+------+</span>

<span>3\.</span> <span>更改某一行</span>

<span>mysql></span> <span>**_update db1.t1 set name='aaa' where id=1;_**</span>

<span>Query OK, 1 row affected (0.02 sec)</span>

<span>Rows matched: 1 Changed: 1 Warnings: 0</span>

<span>这样就把原来</span><span>id</span><span>为</span><span>1</span><span>的那行中的</span><span>name</span><span>改成</span><span>’aaa’</span>

<span>4\.</span> <span>删除表</span>

<span>mysql></span><span>** _drop table db1.t1;_**</span>

<span>Query OK, 0 rows affected (0.01 sec)</span>

<span>5\.</span> <span>删除数据库</span>

<span>mysql></span> <span>**_drop database db1;_**</span>

<span>Query OK, 0 rows affected (0.07 sec)</span>

<span>6\.</span> <span>备份与恢复库</span>

<span>mysqldump -uroot -p mysql >mysql.sql</span>

这里的mysqldump 就是备份的工具了，-p后面的mysql指的是mysql库,把备份的文件重定向到mysql.sql。如果恢复的话，只要：

<span>mysql -uroot -p mysql < mysql.sql</span>

<span>关于</span><span>MySQL</span><span>的基本操作笔者就介绍这么多，当然学会了这些还远远不够，希望你能够在你的工作中学习到更多的知识，如果你对</span><span>MySQL</span><span>有很大兴趣，不妨深入研究一下，毕竟多学点总没有坏处</span><span>。</span><span>如果想学跟多的东西请去查看<a>MySQL官方中文参考手册</a></span><span>（</span><span>5.1</span><span>）</span><span>。</span>

