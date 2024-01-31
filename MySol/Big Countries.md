把資料庫建起來的SQL
現在建table會在名稱後綴題目編號，這樣避免table名稱撞名
這裡建table只是為了方便，型別其實用的不是很恰當，並且有些
應該還要劃分出其他table，再fk reference過來
```SQL
CREATE TABLE country_5 (
    name varchar(30),
    continent varchar(30),
    area int,
    population int,
    gdp int,
    PRIMARY KEY (name)
);

INSERT INTO country_5 (name, continent, area, population, gdp) VALUES
("Afghanistan", "Asia", 652230, 25500100, 20343000),
("Albania", "Europe", 28748 , 2831741 , 12960000),
("Algeria", "Africa", 2381741 , 37100000 , 188681000),
("Andorra", "Europe", 468 , 78115 , 3712000),
("Angola", "Africa", 1246700 , 20609294 , 100990000);
```

查詢的SQL
```SQL
SELECT name, population, area FROM country_5 
where area >= 3000000 OR population >= 25000000;
```
感覺是真正的easy等級題目。