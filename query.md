## 1. Selezionare tutti gli studenti nati nel 1990 (160)

select \*
from students
where YEAR(date_of_birth) = 1990;

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

select \*
from courses
where cfu
and cfu > 10;

## 3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT \*
from students
where timestampdiff(YEAR, date_of_birth, CURDATE()) > 30;

## 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT \*
from courses
where year = 1
and period = "I semestre"
