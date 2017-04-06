# T-SQL

T-SQL stands for Transact Structure Query Language which is a Microsoft product and is an extension of SQL Language.

#### To START SQL SERVER using Termianl
```
mysql.server start
```

#### To STOP SQL SERVER using Termianl
```
mysql.server stop
```

#### The default root password is blank (i.e. empty string) not root. So you can just login as:
```
mysql -u root
```
#### To change password:
```
mysql -u root -h 127.0.0.1 -p
```

#### Difference between drop and truncate table.
- Both are DDL Commands
Drop table: Removes one or more table definitions and all data, indexes, triggers, constraints, and permission specifications for those tables.

TRUNCATE table: Removes all rows from a table without logging the individual row deletions. TRUNCATE TABLE is similar to the DELETE statement with no WHERE clause; however, TRUNCATE TABLE is faster and uses fewer system and transaction log resources.

