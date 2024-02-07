CREATE DATABASE seminar_6;
USE seminar_6;

# Вывести N чисел фебоначи В ВИДЕ ПРОЦЕДУРЫ 

-- удаляет процедуру. Необходимо удалять и пересоздавать процедуру если ее необходимо изменить.
DROP PROCEDURE fibo;

# эта строка меняет символ отделения на // для того чтобы внутри процедуры действия не завершалась на ;
DELIMITER // 

#Создает процедуру с аргументом 
CREATE PROCEDURE fibo (IN N INT)

-- НАчало процедуры   
BEGIN 
-- Объявление переменных
	DECLARE n1 INT DEFAULT 0;
    DECLARE n2 INT DEFAULT 1;
    DECLARE temp INT;
    DECLARE res VARCHAR (100) DEFAULT "0, 1";
    
    IF N = 1 THEN SELECT CONCAT(n1);
    ELSEIF N = 2 THEN SELECT CONCAT(n1, ", ", n2);
    ELSE WHILE N > 2 DO
			SET res = CONCAT(res, ", ", n2+n1);
            SET temp = n2;
            SET n2 = n2 + n1;
            SET n1 = temp;
            SET N = N - 1;
        -- Конец цикла    
		END WHILE;
        SELECT res;
    -- Конец IF     
    END IF;
    
    
-- Конец процедуры с указанием символа отделения используемого в данной процедуре. (можно использовать любые символы, главное чтобы они не встречались внутри самой процедуры)    
END // 

-- Указание стандартного символа отделения (по умолчанию) для дальнейшей работы.
DELIMITER ;  

-- Вызывает процедуру, функция вызывается SELECT-ом. В () Указать аргумент если есть. 
CALL fibo(16); 



# Вывести N чисел фебоначи В ВИДЕ ФУНКЦИИ 
DROP FUNCTION fibo1;

DELIMITER // 

CREATE FUNCTION fibo1 (N INT)

-- НЕОБХОДИМО УКАЗАТЬ ВОЗВРАЩАЕМОЕ ЗНАЧЕНИЕ 
RETURNS VARCHAR (100)

-- УКАЗЫВАЕТ НА ТО ЧТО ДАННАЯ ФУНКЦИЯ НЕ РАБОТАЕТ С БД. (ЧИТАТЬ ДОК) 
DETERMINISTIC

BEGIN 

	DECLARE n1 INT DEFAULT 0;
    DECLARE n2 INT DEFAULT 1;
    DECLARE temp INT;
    DECLARE res VARCHAR (100) DEFAULT "0, 1";
    
    IF N = 1 THEN 
    -- ВМЕСТО SELECT УКАЗЫВАЕМ RETURN
		RETURN CONCAT(n1);
    ELSEIF N = 2 THEN 
		RETURN CONCAT(n1, ", ", n2);
    ELSE 
		WHILE N > 2 DO
			SET res = CONCAT(res, ", ", n2+n1);
            SET temp = n2;
            SET n2 = n2 + n1;
            SET n1 = temp;
            SET N = N - 1;   
		END WHILE;
        
	RETURN res;     
    
    END IF;
    
END // 

DELIMITER ;

 -- Вызов функции 
SELECT fibo1(16); 
