# SQL

CREATE SCHEMA `homework_1` ;

CREATE TABLE `homework_1`.`phone_base` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `Product_name` VARCHAR(45) NOT NULL,
  `Manufacturer` VARCHAR(45) NOT NULL,
  `Product_count` VARCHAR(45) NOT NULL,
  `Price` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`));

--	Создайте таблицу с мобильными телефонами, используя графический интерфейс. Заполните БД данными.

INSERT INTO `homework_1`.`phone_base` (`Product_name`, `Manufacturer`, `Product_count`, `Price`) VALUES ('iPhone X', 'Apple', '3', '76000');
INSERT INTO `homework_1`.`phone_base` (`Product_name`, `Manufacturer`, `Product_count`, `Price`) VALUES ('iPhone 8', 'Apple', '2', '51000');
INSERT INTO `homework_1`.`phone_base` (`Product_name`, `Manufacturer`, `Product_count`, `Price`) VALUES ('Calaxy S9', 'Samsung', '2', '56000');
INSERT INTO `homework_1`.`phone_base` (`Product_name`, `Manufacturer`, `Product_count`, `Price`) VALUES ('Galaxy S8', 'Samsung', '1', '41000');
INSERT INTO `homework_1`.`phone_base` (`Product_name`, `Manufacturer`, `Product_count`, `Price`) VALUES ('P20 Pro', 'Huawei', '5', '36000');

/* Выведите название, производителя и цену для товаров, 
количество которых превышает 2 (SQL - файл, скриншот, либо сам код)
*/ 

SELECT Product_name, Manufacturer, Price
FROM phone_base
WHERE Product_count > 2;

-- Выведите весь ассортимент товаров марки “Samsung”

SELECT * FROM phone_base
WHERE Manufacturer = "Samsung";

-- Выведите информацию о телефонах, где суммарный чек больше 100 000 и меньше 145 000**

SELECT Product_name, Manufacturer, Product_count, Price, Price * Product_count AS Total_price
FROM phone_base
WHERE Price * Product_count > 100000 AND Price * Product_count < 145000;

-- С помощью регулярных выражений найти nовары, в которых есть упоминание "Iphone"

SELECT * FROM phone_base
WHERE Product_name 
LIKE "iPhone%";

-- С помощью регулярных выражений найти "Galaxy"

SELECT * FROM phone_base
WHERE Product_name 
LIKE "%Galaxy%"; 


-- С помощью регулярных выражений найти товары, в которых есть ЦИФРЫ

SELECT * FROM phone_base
WHERE Product_name 
RLIKE "[0-9]";

-- С помощью регулярных выражений найти товары, в которых есть ЦИФРА "8"  

SELECT * FROM phone_base
WHERE Product_name
RLIKE "[8]";
