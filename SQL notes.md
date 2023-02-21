SQL note



## insert data to A from B

if table A exits:

insert into A(a,b,c) (select a,b,c from B) 

if table A doesn't exit:

select a,b,c into A from B 

if it's acrossing different DB:

insert into ADB.[dbo].A(a,b,c)  (select a,b,c from BDB.[dbo].B)

## arrange by rank of grades

```sql
select *, rank() over (partition by 课程号 order by 成绩 desc) as 排名
from score;
```