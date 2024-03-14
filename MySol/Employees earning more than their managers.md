建立table的sql
```sql
CREATE TABLE employee_15 (
    empId            int,
    name             varchar(20),
    salary           int,
    managerId        int,
    PRIMARY KEY (empId),
    foreign KEY (managerId) REFERENCES employee_15(empId)
);

INSERT INTO employee_15 (empId, name, salary, managerId) VALUES
(3, "Brad", 60000, NULL),
(4, "Thomas", 90000, NULL),
(1, "John", 70000, 3),
(2, "Dan", 80000, 4);
```


搜尋的sql
```sql
select t1.name as Employee from employee_15 as t1 
join employee_15 as t2 
where t1.managerId = t2.empId and t1.salary > t2.salary;
```