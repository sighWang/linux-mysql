# Linux MySQL

## 中文乱码问题

### 数据库设置

#### 1:数据库服务器编码
- 查看
```
show variables like "%char%";
```

- 更改为utf-8
```
SET character_set_client='utf8';
SET character_set_connection='utf8';
SET character_set_results='utf8'
```



#### 2:数据库编码
- 查看
```
show create database database_name;
```



#### 3:数据库表编码
- 查看
```
show create table table_name;
```
- 更改为UTF—8
```
ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];
```


### 编辑器设置

#### 1:设置文件格式为utf-8
#### 2:为数据库连接url添加编码控制
- 
```
String url = "jdbc:mysql://localhost:3306/menagerie?useUnicode=true&&characterEncoding=utf-8";
```
