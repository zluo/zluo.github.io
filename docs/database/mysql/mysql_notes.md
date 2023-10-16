---
layout: default
title: mysql note
parent: Database
permalink: /docs/database/mysql
---

# Mysql Notes

# 1. Frequently Usage

## 1.1 Connect to server

```bash
$> mysql -h localhost -u root -p
```

### 1.2. Show Databases

```sql
mysql> show databases;
```

### 1.3 show current database

    select Database();

### 1.4. Change database

    use database

### 1.5. Create Database

    create database test

### 1.6. Show Tables
```sql
    mysql  > show tables;
    mysql> CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20), -> species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);

    mysql > describe pet;
```

### 1.7. show character set of a table
```sql
  SHOW FULL COLUMNS FROM table_name;
```

### 1.8. set character set of a table
```sql
ALTER TABLE etape_prospection CONVERT TO CHARACTER SET utf8;
```

### 1.9. Show Columns
```sql
show columns in TEST_TABLE;
```
### 1.10. Show Engines
```sql
mysql> show engines\G
```
 
### 1.11. Change default engine to MYISAM

```sql
set default_storage_engine#MYISAM;
```

### 1.12. Show row size

```sql
SELECT TABLE_ROWS FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_NAME # 'line_items';
```

## 2. User Configuration

### 2.1. Add User And Grant All Privileges
```sql
  CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
```
## 3. Run mysql from file

## 3.1. Load data
```sql
Fluffy Harold cat f  1993-02-04
Claws Gwen cat m 1994-03-17  
Buffy Harold dog f 1989-05-13  
Fang Benny dog m 1990-08-27   
Bowser Diane dog m 1998-09-11   
Chirpy Gwen bird f 1997-12-09   
Whistler Gwen bird 1996-04-29   
Slim Benny snake m 1979-08-31  
```

```sql
mysql> load data local infile '/path/pet.txt' into table pet lines terminated by '\r\n'.
```

### 3.2. Executing sql statements from a text file

```bash
$> mysql db_name < text_file
```
```bash
shell> mysql < text_file (put use db_name as the first line of the in the file)
```

### 3.3 Inside mysql
```sql
mysql> source file_name 
```
```sql
mysql> \. file_name
```

example:
```sql
 source /src/build_/server/gen/sql/MYSQL_SCHEMA.sql;
```



## 4. Export and Import
```sql
 mysqldump -u username -ppassword database_name > FILE.sql
```
```sql
 mysql -u username -ppassword database_name < FILE.sql
```


## 5. MySQL Stored Procedure
```sql
-- specify delimiter as //

DELIMITER //
drop table if exists tmplog//
drop table if exists tmpresult//

create temporary table if not exists tmplog (msg varchar(512)) engine # memory//
create temporary table if not exists tmpresult (pn varchar(40), ps_id int, 
ps_guid varchar(40), ps_start_date dateTime, ps_expiry_period int, Email_Sent int, Valid int, Documents int) engine # memory//


DROP PROCEDURE IF EXISTS vp//

CREATE PROCEDURE vp ()

BEGIN

-- declare variables

DECLARE v_ps_id INT;
DECLARE v_docs INT;
DECLARE v_send_email INT;
DECLARE v_att_value varchar(40);
DECLARE v_ps_guid varchar(40);
DECLARE v_ps_start_date dateTime;
DECLARE v_ps_expiry_period INT;
DECLARE v_render_count INT;


DECLARE done BOOLEAN DEFAULT 0;

DECLARE ps_id_cs CURSOR
  FOR select ATT_VALUE, P.PS_ID, P.PS_GUID,P.PS_START_DATE, P.PS_EXPIRY_PERIOD from AWS_ATTRIBUTE AS A 
  inner join AWS_PROCESS_SESSION AS P on A.PS_ID#P.PS_ID where ATT_NAME#'PlcyN';
  -- LIMIT 1000  OFFSET 0;
  
-- Declare continue handler for '02000'
DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done#1;

   OPEN ps_id_cs;

    REPEAT
    FETCH ps_id_cs INTO v_att_value,v_ps_id,v_ps_guid,v_ps_start_date,v_ps_expiry_period;

    IF NOT done THEN 
        
      select count(*) into v_render_count from AWS_DOCUMENT as d inner join AWS_DOCUMENT_GROUP  as g on 
      d.docg_id#g.docg_id where g.ps_id#v_ps_id and RENS_ID#10;
       
        IF NOT v_render_count THEN
 
 --       insert into tmplog values(CONCAT("find PlcyN: ", v_att_value,   " in Process: " , v_ps_id , " with " ,v_render_count ," rendered documents."));
 
        select count(*) into v_docs from AWS_DOCUMENT as d inner join AWS_DOCUMENT_GROUP  as g on 
        d.docg_id#g.docg_id where g.ps_id#v_ps_id;
        
        select count(*) into v_send_email from PipAuditEvent where targetCtx#v_ps_guid and eventType #'AWS_INVITATION_SENT';
        
        insert into tmpresult values(v_att_value,v_ps_id,v_ps_guid,v_ps_start_date,v_ps_expiry_period,v_send_email,v_render_count,v_docs);
        
--        IF v_send_email THEN
       
--          insert into tmplog values(CONCAT("find PlcyN: ", v_att_value,   " in Process: " , v_ps_id , " with " ,v_render_count ," rendered documents and Invitation sended"));
--        END IF; 
        
        END IF;
        
        
    END IF;
    UNTIL done END REPEAT;
   CLOSE ps_id_cs;

END//


DELIMITER ;

CALL vp();

select * from tmpresult

Cursor Looping 

```

## Java JDBC Connection

```java
  jdbc:mysql://db1:3306/aws?autoReconnect=true&amp;useSSL=False&amp;useUnicode=true&amp;characterEncoding=UTF-8
```

### start mysql database service

```sql
   sudo service mysqld start
```





---
## References

1. [MySQL Reference Manul](http://dev.mysql.com/doc/refman/8.0/en/index.html)

