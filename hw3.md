CREATE DATABASE hw3;
USE hw3;

CREATE TABLE salespeople
(snum INT,
 sname VARCHAR (100),
 city VARCHAR (100),
 comm VARCHAR (10));
 
 INSERT salespeople (snum, sname, city, comm) VALUES
 (1001, "Peel", "London", ".12"),
 (1002, "Serres", "San Jose", ".13"),
 (1004, "Motika", "London", ".11"),
 (1007, "Rifkin", "Barcelona", ".15"),
 (1003, "Barcelona", "New York", ".10");
 
 
 CREATE TABLE customers
 (cnum INT,
 cname VARCHAR (100),
 city VARCHAR (100),
 rating INT,
 snum INT);
 
INSERT customers (cnum, cname, city, rating, snum) VALUES
(2001, "Hoffman", "London", 100, 1001),
(2002, "Giovanni", "Rome", 100, 1003),
(2003, "Liu", "SanJose", 200, 1002),
(2004, "Grass", "Berlin", 300, 1002),
(2006, "Clemens", "London", 100, 1001),
(2008, "Cisneros", "SanJose", 300, 1007),
(2007, "Pereira", "Rome", 100, 1004);


 CREATE TABLE orders 
 (onum INT,
 amt FLOAT,
 odata DATE,
 cnum INT,
 snum INT);
 
INSERT orders (onum, amt, odata, cnum, snum)VALUES
(3001, 18.69, "1990-03-10", 2008, 1007),
(3003, 767.19, "1990-03-10", 2001, 1001),
(3002, 1900.10, "1990-03-10", 2007, 1004),
(3005, 5160.45, "1990-03-10", 2003, 1002),
(3006, 1098.16, "1990-03-10", 2008, 1007),
(3009, 1713.23, "1990-04-10", 2002, 1003),
(3007, 75.75, "1990-04-10", 2004, 1002),
(3008, 4723.00, "1990-05-10", 2006, 1001),
(3010, 1309.95, "1990-06-10", 2004, 1002),
(3011, 9891.88, "1990-06-10", 2006, 1001);


# 1.	 Напишите запрос, который вывел бы таблицу со столбцами в следующем порядке: city,
# sname, snum, comm. (к первой или второй таблице, используя SELECT)

SELECT city, sname, snum, comm
FROM salespeople;

# 2.	 Напишите команду SELECT, которая вывела бы оценку(rating), сопровождаемую
# именем каждого заказчика в городе San Jose. (“заказчики”)

SELECT cname, rating
FROM customers
WHERE city = "SanJose";

# 3.	 Напишите запрос, который вывел бы значения snum всех продавцов из таблицы заказов
# без каких бы то ни было повторений. (уникальные значения в  “snum“ “Продавцы”)

SELECT DISTINCT snum
FROM orders;

# 4*. 	Напишите запрос, который бы выбирал заказчиков, чьи имена начинаются с буквы G.
# Используется оператор "LIKE": (“заказчики”) https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html

SELECT cname
FROM customers
WHERE cname RLIKE "G";

# 5. 	Напишите запрос, который может дать вам все заказы со значениями 
# суммы выше чем $1,000. (“Заказы”, “amt”  - сумма)

SELECT *
FROM orders
WHERE amt > 1000; 

# 6.	Напишите запрос который выбрал бы наименьшую сумму заказа.
# (Из поля “amt” - сумма в таблице “Заказы” выбрать наименьшее значение)

SELECT MIN(amt)
FROM orders;

# 7. 	Напишите запрос к таблице “Заказчики”, который может показать всех заказчиков,
# у которых рейтинг больше 100 и они находятся не в Риме.
 
 SELECT *
 FROM customers
 WHERE rating > 100 and city != "Rome";
 
CREATE TABLE employee 
(id INT, name VARCHAR (100), surnname VARCHAR (100), specialty VARCHAR (100), srniority INT, salary INT, age INT);
 
INSERT employee (id, name, surnname, specialty, srniority, salary, age)
VALUES (1, "Вася", "Васькин", "начальник", 40, 100000, 60),
(2, "Петя", "Петькин", "начальник", 8, 70000, 30),
(3, "Катя", "Каткина", "инженер", 2, 70000, 25),
(4, "Саша", "Сашкин", "инженер", 12, 50000, 35),
(5, "Иван", "Иванов", "рабочий", 40, 30000, 59),
(6, "Петр", "Петров", "рабочий", 20, 25000, 40),
(7, "Сидор", "Сидоров", "рабочий", 10, 20000, 35),
(8, "Антон", "Антонов", "рабочий", 8, 19000, 28),
(9, "Юра", "Юркин", "рабочий", 5, 15000, 25),
(10, "Максим", "Воронин", "рабочий", 2, 11000, 22),
(11, "Юра", "Галкин", "рабочий", 3, 12000, 24),
(12, "Люся", "Люськина", "рабочий", 10, 10000, 49);
 
# 1. Отсортируйте поле “зарплата” в порядке убывания и возрастания

SELECT  * 
FROM employee
ORDER BY salary DESC;

SELECT  * 
FROM employee
ORDER BY salary;

# 2. ** Отсортируйте по возрастанию поле “Зарплата” и выведите 5 строк с наибольшей заработной платой 
# (возможен подзапрос)

SELECT *
FROM (SELECT * FROM employee
ORDER BY salary DESC
LIMIT 5) AS T
ORDER BY salary;

# 3. Выполните группировку всех сотрудников по специальности , суммарная зарплата которых превышает 100000
 
 SELECT specialty, SUM(salary) sum_salary 
 FROM employee
 GROUP BY specialty
 HAVING sum_salary > 100000;
 
