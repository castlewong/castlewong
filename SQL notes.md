SQL note


## 表A和表B中的guid列是相同的，想要更新表B中对应行的road_id列
可以使用以下SQL语句：

```
UPDATE table_b
SET road_id = a.road
FROM (
  SELECT guid, road
  FROM table_a
) a
WHERE table_b.guid = a.guid;
```

这个UPDATE语句会从表A中选择guid和对应的road值，并将它们与表B进行联接，然后用table_a中的road列值更新table_b中的road_id。请注意，这里假设guid在表A和表B之间是唯一的。
如果不是唯一的，则需要使用其他字段来确保正确地匹配行。

## To replace all the numbers in a string with a single number in PostgreSQL

use the `regexp_replace` function. Here's an example:

```
SELECT regexp_replace('abc123def456', '\d+', '9');
```

In this example, the string `'abc123def456'` contains numbers but we want to replace them all with the number 9. The regular expression `'\d+'` matches one or more consecutive digits, and the replacement string is `'9'`.

The result of the above query would be the string `'abc9def9'`. 

You can adjust the replacement string to whatever number you would like to use for the replacement.

## update A by matching value with B

An inner join is a type of join operation in SQL that returns only the rows from both tables that have matching values in the specified columns. In this case, the inner join is used to match the attribute IDs in both tables (table a and table b) and retrieve the corresponding object_len value from table a to update the object_len attribute in table b.

The syntax for an inner join is as follows:

```SQL
SELECT column1, column2, ...
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

## insert data to A from B

if table A exits:

insert into A(a,b,c) (select a,b,c from B) 

if table A doesn't exit:

select a,b,c into A from B 

if it's acrossing different DB:

```SQL
insert into ADB.[dbo].A(a,b,c)  (select a,b,c from BDB.[dbo].B)
```

## arrange by rank of grades

```sql
select *, rank() over (partition by subject_ID order by grade desc) as rank
from score;
```