CREATE DATABASE hw2;
USE hw2;

-- 1. Используя операторы языка SQL, создайте табличку “sales”. Заполните ее данными

CREATE TABLE sales
(
	id INT,
    order_data DATE,
    bucket VARCHAR (25)
);

INSERT sales (id, order_data, bucket) VALUES
(1, "2021-01-01", "100 to 300"),
(1, "2021-01-02", "100 to 300"),
(1, "2021-01-03", "less then equal to 100"),
(1, "2021-01-04", "100 to 300"),
(1, "2021-01-05", "greater then 300");

SELECT * FROM sales;

-- 2. Сгруппируйте значений количества в 3 сегмента — меньше 100, 100-300 и больше 300.

ALTER TABLE sales
ADD COLUMN size VARCHAR (10);

UPDATE sales SET size=
CASE
	WHEN sales.bucket = "100 to 300" THEN "average"
    WHEN sales.bucket = "less then equal to 100" THEN "small"
    WHEN sales.bucket ="greater then 300" THEN "big"
    ELSE "not_size"
END;

SELECT id, order_data FROM sales
WHERE size = "small";

SELECT id, order_data FROM sales
WHERE size = "average";

SELECT id, order_data FROM sales
WHERE size = "big";

-- 3. Создайте таблицу “orders”, заполните ее значениями. Покажите “полный” статус заказа, используя оператор CASE

CREATE TABLE orders
(
	orderid INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    employeeid VARCHAR (5) NOT NULL,
    amount FLOAT, 
    orderstatus VARCHAR (30)    
);
SELECT * FROM orders;

INSERT INTO orders (employeeid, amount, orderstatus) VALUES
("e03", 15.00, "OPEN"), 
("e01", 25.50, "OPEN"),
("e05", 100.70, "CLOSED"),
("e02", 22.18, "OPEN"),
("e04", 9.50, "CANSELLED"),
("e04", 99.99, "OPEN"); 

-- 4. Чем NULL отличается от 0?
/*
NULL - отсутствие данных.
0 - это уже что то). 
*/
