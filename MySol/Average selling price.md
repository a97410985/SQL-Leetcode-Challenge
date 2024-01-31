把資料庫建起來的SQL
現在建table會在名稱後綴題目編號，這樣避免table名稱撞名
```SQL
create table Prices_39 (
	product_id int,
    start_date date,
    end_date date,
    price int,
    PRIMARY KEY (product_id, start_date, end_date)
);

INSERT INTO Prices_39 (product_id, start_date, end_date, price) VALUES
(1, "2019-02-17", "2019-02-28", 5),
(1, "2019-03-01", "2019-03-22", 20),
(2, "2019-02-01", "2019-02-20", 15),
(2, "2019-02-21", "2019-03-31", 30);


create table UnitsSold_39 (
    product_id int,
    purchase_date date,
    units int
);

INSERT INTO UnitsSold_39 (product_id, purchase_date, units) VALUES
(1, "2019-02-25", 100),
(1, "2019-03-01", 15),
(2, "2019-02-10", 200),
(2, "2019-03-22", 30);
```

查詢的SQL
```SQL
SELECT product_id, round(SUM(temp.units * temp.price) / SUM(temp.units), 2) average_price FROM
(SELECT unitssold_39.product_id, price, units FROM unitssold_39 
LEFT JOIN prices_39 ON unitssold_39.product_id = prices_39.product_id 
AND unitssold_39.purchase_date between prices_39.start_date AND prices_39.end_date) AS temp
group by product_id;
```

先join`UnitsSold` table和`Prices` table，用left join可以確保`UnitSold`都會在，這題先把所有購買紀錄都對上對應時間區間的間隔，暫存為table temp(subquery's result)，在對temp table做query。
如果是`natural join`就不用在合併條件那邊加上product_id要相同，而且會使用一般的where clause來過濾日期不相符的rows。如下
```SQL
SELECT product_id, round(SUM(temp.units * temp.price) / SUM(temp.units), 2) average_price FROM
(SELECT unitssold_39.product_id, price, units FROM unitssold_39 
natural join prices_39 where unitssold_39.purchase_date between prices_39.start_date AND prices_39.end_date) AS temp
group by product_id;
```