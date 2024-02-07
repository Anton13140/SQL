CREATE DATABASE seminar_3;
USE seminar_3;

CREATE TABLE employee (id INT, name VARCHAR (100), surnname VARCHAR (100), specialty VARCHAR (100), srniority INT, salary INT, age INT);

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

-- 1. Выведите все записи, отсортированные по полю "age" по возрастанию.

SELECT * FROM employee
ORDER BY age;

-- 2. Выведите все записи, отсортированные по полю "name".

SELECT * FROM employee
ORDER BY name;

-- 3. Выведите записи полей "name", "surnname", "age" отсортированные по полю "name" в алфавитном порядке по убыванию.

SELECT name, surnname, age 
FROM employee
ORDER BY name;

-- 4. Выполните сортировку по полям "name" и "age" по убыванию.

SELECT *
FROM employee
ORDER BY name DESC, age DESC;

-- 1.	Выведите уникальные (неповторяющиеся) значения полей "name"

SELECT DISTINCT name
FROM employee;

-- 2.	Выведите первые две первые записи из таблицы

SELECT *
FROM employee
ORDER BY id
LIMIT 2;

-- 3.	Пропустите  первые 4 строки ("id" = 1, "id" = 2,"id" = 3,"id" = 4) и извлеките следующие 3 строки ("id" = 5, "id" = 6, "id" = 7)

SELECT *
FROM employee
ORDER BY id
LIMIT 4, 3;

# 4*. 	Пропустите две последнии строки (где id=12, id=11) и извлекаются следующие за ними 
#       3 строки (где id=10, id=9, id=8). Дополнительно перевернут список по порядку.
 
SELECT *
FROM(SELECT * 
FROM employee
ORDER BY id DESC
LIMIT 2, 3) AS T
ORDER BY id;

CREATE TABLE employee_tab (id INT, name VARCHAR(100), work_data TIMESTAMP, daily_typing_pages INT);

INSERT employee_tab (id, name, work_data, daily_typing_pages)VALUES
(1, "John", "2007-01-24", 250),
(2, "Ram", "2007-05-27", 220),
(3, "Jack", "2007-05-06", 170),
(3, "Jack", "2007-04-24", 100),
(4, "Jill", "2007-04-06", 220),
(5, "Zara", "2007-06-06", 300),
(5, "Zara", "2007-02-06", 350);

# 1.	Рассчитайте общее количество всех страниц dialy_typing_pages

SELECT SUM(daily_typing_pages) 
FROM employee_tab;

# 2.	Выведите общее количество напечатанных страниц каждым человеком (с помощью предложения GROUP BY)  

SELECT id, name, SUM(daily_typing_pages)
FROM employee_tab
GROUP BY id, name;

# 3.	Посчитайте количество записей в таблице

SELECT COUNT(*)
FROM employee_tab;

# 4.	Выведите количество имен, которые являются уникальными 

SELECT COUNT(DISTINCT name)
FROM employee_tab; 

# 5. 	Найдите среднее арифметическое по количеству ежедневных страниц для набора (daily_typing_pages)

SELECT AVG(daily_typing_pages)
FROM employee_tab; 

CREATE TABLE tabl (id INT, name VARCHAR(100), age INT, salary INT);

INSERT tabl (id, name, age, salary)VALUES
(1, "Дима", 23, 100),
(2, "Петя", 23, 200),
(3, "Вася", 23, 300),
(4, "Коля", 24, 1000),
(5, "Иван", 25, 2000);

# 1. Сгруппируйте поля по возрасту (будет 3 группы - 23 года, 24 года и 25 лет).
# Для каждой группы  найдите суммарную зарплату 

SELECT age, SUM(salary) 
FROM tabl
GROUP BY age;

# 2. Сгруппируйте поля по возрасту (будет 3 группы - 23 года, 24 года и 25 лет). 
# Найдите максимальную заработную плату внутри группы

SELECT age, MAX(salary) 
FROM tabl
GROUP BY age;

# 3. Сгруппируйте поля по возрасту (будет 3 группы - 23 года, 24 года и 25 лет).
# Найдите минимальную заработную плату внутри группы

SELECT age, MIN(salary) 
FROM tabl
GROUP BY age;

SELECT age, MIN(salary), MAX(salary), SUM(salary) 
FROM tabl
GROUP BY age;


# 1.	Выведите только те строки, в которых суммарная зарплата больше или равна 1000

SELECT age, SUM(salary) сумма
FROM tabl
GROUP BY age
HAVING сумма >= 1000;

# 2. 	Выведите только те группы, в которых количество строк меньше или равно двум

SELECT age, COUNT(*) count_p
FROM tabl
GROUP BY age
HAVING count_p <= 2;

# 3.	Выведите только те группы, в которых количество строк меньше или равно двум. 
#       Для решения используйте оператор “BETWEEN”

SELECT age, COUNT(*) count_p
FROM tabl
GROUP BY age
HAVING count_p BETWEEN 0 and 2;

# 4.*	Выведите только те группы, в которых количество строк меньше или равно двум.
#        Для решения используйте оператор “IN”

SELECT age, COUNT(*) count_p
FROM tabl
GROUP BY age
HAVING count_p IN (0, 1, 2);
