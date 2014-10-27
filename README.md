# Linux MySQL
## 安装
- 使用APT Repository方式安装[A Quick Guide to Using the MySQL APT Repository](http://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/)。

## 登陆
- 登陆MySQL数据库运行
`mysql -h localhost -u root -p`
- 根据提示安装相应mysql-client后再次运行`mysql -h localhost -u root -p`输入密码

##新建数据库用户并授权
- 1：以root用户登陆。
- 2：新建数据库 `datebase_name`。
- 3：创建新用户 `CREATE USER 'user_name'@'localhost' IDENTIFIED BY 'password';`。
- 4：授权新用户 `GRANT ALL ON database_name.* TO 'user_name'@'localhost'`。
 eg:
  * GRANT ALL ON menagerie.* TO 'test'@'localhost'
  * GRANT SELECT ON menagerie.* TO 'test'@'localhost'

## 中文乱码问题
MySQL中文乱码可分为四级
1、服务器 2、数据库 3、数据表 4、客户端。可以将这四个级别的编码方式全部设置为utf8从而解决中文乱码问题。
#### 1:服务器级编码格式
- 查看
`
 show variables like "%char%";
`运行结果为
```
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | latin1                     |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | latin1                     |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
```
- 更改latin1为utf-8
```
SET character_set_database='utf8';
SET character_set_server='utf8';
```



#### 2:数据库编码
- 查看
`
show create database database_name;
`



#### 3:数据库表编码
- 查看
`
show create table table_name;
`
- 更改为UTF—8
```
ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];
```

#### 客户端编码设置（以java为例）
- 1:设置文件格式为utf-8
- 2:为数据库连接url添加编码控制
```
String url = "jdbc:mysql://localhost:3306/menagerie?useUnicode=true&&characterEncoding=utf-8";
```
