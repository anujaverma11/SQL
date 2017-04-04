# T-SQL

T-SQL stands for Transact Structure Query Language which is a Microsoft product and is an extension of SQL Language.

To START SQL SERVER using Termianl
```
mysql.server start
```

To STOP SQL SERVER using Termianl
```
mysql.server stop
```

The default root password is blank (i.e. empty string) not root. So you can just login as:
```
mysql -u root
```
To change password:
```
mysql -u root -h 127.0.0.1 -p
```