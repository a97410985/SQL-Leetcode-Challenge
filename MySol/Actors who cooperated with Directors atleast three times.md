把資料庫建起來的SQL
```SQL
create table ActorDirector (
	actor_id int,
    director_id int,
    timestamp int,
    primary key (timestamp)
);

insert into ActorDirector (actor_id, director_id, timestamp) VALUES (1,1,0), (1,1,1), (1,1,2), (1,2,3), (1,2,4), (2,1,5), (2,1,6);

```

我的解法
```SQL
SELECT actor_id, director_id FROM actordirector group by actor_id, director_id having count(*)>=3;
```

想法很簡單SQL有一部分的操作都是aggregation，aggregation的操作的前提就是要有group by，才能對那些分群的東西做操作，像是count、max、min等。
所以分群後用having過濾出有合作三次以上的演員與導演。