把資料庫建起來的SQL
```SQL
CREATE TABLE my_numbers(
    num int
);

INSERT INTO my_numbers (num) VALUES
(8),
(8),
(3),
(3),
(1),
(4),
(5),
(6);
```

查詢的SQL
```SQL
SELECT * FROM myjdbc.my_numbers 
group by num 
HAVING count(*) = 1 
order by num desc 
LIMIT 1;
```
感覺利用max function會讓程式更簡潔。