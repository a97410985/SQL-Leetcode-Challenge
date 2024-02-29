把資料庫建起來的SQL
```SQL
create table emails_32(
    Id int auto_increment,
    Email varchar(20),
    PRIMARY KEY (Id)
);

INSERT INTO emails_32
(Id, Email)
VALUES
(1, "john@example.com"),
(2, "bob@example.com"),
(3, "john@example.com");
```

查詢的SQL
```SQL
SELECT * FROM myjdbc.emails_32 group by email;
```
因為group by預設會取一個group的第一個作為projection的代表，
所以這種作法可以說是一種trick，但是要確保Id在插入的時候是由小到大的順序的嗎?還是沒差。

原作者的作法就是正規的做法，先用CTE(commom table expression)，先把重複的email根據id的順序給予rank編號，
之後在把rank編號>1的全部刪掉，就可以去重。

## Syntax
The following are the basic syntax to use ROW_NUMBER() in MySQL:
`ROW_NUMBER() OVER (<partition_definition> <order_definition>)`