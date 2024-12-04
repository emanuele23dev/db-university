## 1. Selezionare tutti gli studenti nati nel 1990 (160)

select \*
from students
where YEAR(date_of_birth) = 1990;

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

select \*
from courses
where cfu
and cfu > 10;
