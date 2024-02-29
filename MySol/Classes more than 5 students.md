把資料庫建起來的SQL
```SQL
CREATE TABLE student_class_7(
    student varchar(10),
    class   varchar(20)
);

INSERT INTO student_class_7 (student, class) VALUES
("A", "Math"),
("B", "English"),
("C", "Math"),
("D", "Biology"),
("E", "Math"),
("F", "Computer"),
("G", "Math"),
("H", "Math"),
("I", "Math");
```

查詢的SQL
```SQL
SELECT * FROM myjdbc.student_class_7 
group by class 
having count(*) >= 5;
```
這種寫法沒有加distinct，
不太懂原作者的作法為何要加distinct
因為如果table的student和class都有綁primary key
不是不會重複