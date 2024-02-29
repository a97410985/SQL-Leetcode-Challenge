把資料庫建起來的SQL
```SQL
create table customers_13 (
    Id    int auto_increment,
    Name  varchar(20),
    PRIMARY KEY (Id)
);

INSERT INTO customers_13
(Name)
VALUES
("Joe"),
("Henry"),
("Sam"),
("Max");

create table orders_13 (
    Id    int,
    CustomerId  int,
    PRIMARY KEY (Id),
    foreign KEY (CustomerId) REFERENCES customers_13(Id)
);

INSERT INTO orders_13
(Id, CustomerId)
VALUES
(1, 3),
(2, 1);
```

查詢的SQL
```SQL
Select Name
FROM customers_13 as c where not exists
(Select null as Id FROM orders_13 where c.Id = CustomerId);
```
這種寫法會用到`full table scan`，是否有更好的做法。