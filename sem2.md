create database seminar_2;
use seminar_2;
create table films
(
id int primary key auto_increment,
name_film varchar(100) not null,
year_of_release int not null,
duration int not null,
description_film varchar(1000)
);

INSERT into films (name_film, year_of_release, duration, description_film) values
("Гарри Поттер", 2001, 155, "кино про магию"),
("Зеленая миля", 2005, 185, "кино про казнь"),
("Форест Гамп", 1990, 210, "кино про человека");

SELECT * FROM films;

# переименовывает таблицу
rename table films TO cinema;

# добавляет новую колонку после колонки с годом выхода фильма (в конкретное место) 
ALTER TABLE cinema
ADD COLUMN Language_Film VARCHAR(30) NOT NULL AFTER year_of_release; 

# удаляет колонку из таблицы по названию
ALTER TABLE cinema 
DROP COLUMN Language_Film;

CREATE TABLE grades 
(
id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
total_marks INT NOT NULL,
grade VARCHAR(10) NOT NULL
);

ALTER TABLE grades
ADD COLUMN class VARCHAR(40);

INSERT INTO grades (total_marks, grade) VALUE 
(450, "A"),
(480, "A+"),
(490, "A++"),
(440, "B+"),
(400, "C+"),
(380, "C"),
(250, "D"),
(200, "E");

SELECT * FROM grades;

UPDATE grades SET class= 
	CASE WHEN grades.grade = "A++" THEN  "DISTINCTION"
	WHEN grades.grade = "A+" THEN  "FIRST CLASS"
	WHEN grades.grade = "A" THEN  "SECOND CLASS"
	WHEN grades.grade = "B+" THEN  "SECOND CLASS"
	WHEN grades.grade = "C+" THEN  "THIRD CLASS"
	ELSE "FAIL"
	END;
    
SELECT * FROM grades;
    
