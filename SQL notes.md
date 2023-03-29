SQL note


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