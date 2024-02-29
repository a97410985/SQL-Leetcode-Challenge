把資料庫建起來的SQL
```SQL
create table orders_8 (
    order_number    int,
    customer_number int,
    order_date      date,
    required_date   date,
    shipped_date    date,
    status          varchar(15),
    comment         varchar(200),
    PRIMARY KEY (order_number)
);

INSERT INTO orders_8
VALUES
(1, 1, "2017-04-09", "2017-04-13", "2017-04-12", "Closed", ""),
(2, 2, "2017-04-15", "2017-04-20", "2017-04-18", "Closed", ""),
(3, 3, "2017-04-16", "2017-04-25", "2017-04-20", "Closed", ""),
(4, 3, "2017-04-18", "2017-04-28", "2017-04-25", "Closed", "");
```

查詢的SQL
```SQL
SELECT customer_number from
(SELECT customer_number, count(*) as count FROM myjdbc.orders_8 
group by customer_number 
order by count 
desc 
limit 1) as t;
```
subquery是否真的有必要? 感覺對效能減損應該很少，因為子query只有一個row，只是做一個row
的projection應該還好