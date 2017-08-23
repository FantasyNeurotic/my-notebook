the way on postgresql
# how to install postgresql
1. install by brew, `brew install postgresql`;

# how to use postgresql
## start postgresql
```
brew services start postgres
# pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
```
## stop postgresql
```
brew services stop postgres
# pg_ctl -D /usr/local/var/postgres stop -s -m fast
```
## change the port (todo: I have a question about it)
* Lookup the file 'postgresq;.conf', the path `/usr/local/var/postgresql`,and change the port '6432'(I do it but it is failed)
* You can also change the port when starting `pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log  - o '-F -p 6432 ' start` or `postgres -p 6432`
then you must set the PGPORT because the default port is 5432, `export PGPORT=6432`,and you can use the psql.[message](https://www.postgresql.org/docs/9.5/static/app-postgres.html)
## connect the postgresql
* createuser bart -P
* createdb test  -O bart  -E UTF8 -e
* psql -U bart  -d test  -h 127.0.0.1

## use the part of postgresql about nosql
* `CREATE EXTENSION hstore;` 
* postgresql的nosql方式主要体现在jsonb的处理
>
>
| operator| Right Operand Type | Description | Example|
| ---: | :----: | :---------- | ---- |
|   =  | jsonb | 两个JSON值是否相等? | '[1,2,3]'::jsonb = '[1,2,3]'::jsonb |
|   @>  | 	jsonb | 左侧JSON值是否包含正确的值？ | '{"a":1, "b":2}'::jsonb @> '{"b":2}'::jsonb |
|   <@  | sysdba | 数据库表模型汇总 |  |

## question
* 删除数据库时，有其他连接占用
```cmd
postgres=# DROP DATABASE testdb;
 
ERROR:  database "testdb" is being accessed by other users
DETAIL:  There are 3 other sessions using the database.
```

```cmd
// 检索出死锁进程的ID 杀掉解锁进程
postgres-# SELECT pg_terminate_backend(pid) FROM pg_stat_activity
postgres-# WHERE datname='testdb' AND pid<>pg_backend_pid();
 
 pg_terminate_backend 
----------------------
 t
 t
 t
(3 rows)
```
