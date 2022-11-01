# SQL

## How to get the MySQL table columns data type?

[original source](https://stackoverflow.com/a/31830486/3652726)

### First option

The first option has 4 different aliases, some of which are quite short :

```sql
EXPLAIN db_name.table_name;
DESCRIBE db_name.table_name;
SHOW FIELDS FROM db_name.table_name;
SHOW COLUMNS FROM db_name.table_name;
```

NB: In each case, you can also write `FROM` two times instead of `db_name.table_name`, example:

```sql
SHOW FIELDS FROM table_name FROM db_name
```

This gives something like :

```
+------------------+--------------+------+-----+---------+-------+
| Field            | Type         | Null | Key | Default | Extra |
+------------------+--------------+------+-----+---------+-------+
| product_id       | int(11)      | NO   | PRI | NULL    |       |
| name             | varchar(255) | NO   | MUL | NULL    |       |
| description      | text         | NO   |     | NULL    |       |
| meta_title       | varchar(255) | NO   |     | NULL    |       |
+------------------+--------------+------+-----+---------+-------+
```

### Second option

The second option is a bit longer :

```sql
SELECT
  COLUMN_NAME, DATA_TYPE 
FROM
  INFORMATION_SCHEMA.COLUMNS 
WHERE
  TABLE_SCHEMA = 'db_name'
AND
  TABLE_NAME = 'table_name';
```

It is also less talkative :

```
+------------------+-----------+
| column_name      | DATA_TYPE |
+------------------+-----------+
| product_id       | int       |
| name             | varchar   |
| description      | text      |
| meta_title       | varchar   |
+------------------+-----------+
```

It has the advantage of allowing selection per column, though, using `AND COLUMN_NAME = 'column_name'` (or `like`).
