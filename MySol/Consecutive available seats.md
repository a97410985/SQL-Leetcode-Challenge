把資料庫建起來的SQL
```SQL
CREATE table available_seats_37 (
    seat_id int auto_increment, 
    free    bool,
    PRIMARY KEY (seat_id)
);

INSERT INTO available_seats_37
(free)
VALUES
(1),(0),(1),(1),(1);
```

查詢的SQL
```SQL
select distinct a.seat_id from available_seats_37 as a 
join available_seats_37 as b 
where b.seat_id = a.seat_id + 1 and b.free = 1 and a.free = 1 or
      b.seat_id = a.seat_id - 1 and b.free = 1 and a.free = 1 
order by seat_id;
```
這是一個很醜，而且效能應該非常差的寫法。
畢竟where的條件判定會每一個row都做一次，條件判定的重複性太多，多了一個`or`