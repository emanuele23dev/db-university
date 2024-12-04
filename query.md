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

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT \*
from exams
where date = '2020-06-20'
and hour > '14:00:00';

## 6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT \*
from degrees
where level = 'magistrale';

## 7. Da quanti dipartimenti è composta l'università? (12)

SELECT \*
from departments

## 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT \*
from teachers
where phone;

## 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

insert into students (degree_id, name, surname, date_of_birth, fiscal_code, enrolment_date, registration_number, email)

value (23, 'Emanuele', 'Meggiarin', '1988-06-23', 'XYZABC12D34E567F', '2021-09-01', '620037', 'emanuele@gmail.it')

<!-- Numero totale di record con 👇
SELECT COUNT(*) FROM students; -->

## 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

update teachers
set office_number = 126
where id = 58

## 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

<!-- disabilito temporaneamente la modalità di safe update con 👇
SET SQL_SAFE_UPDATES = 0; -->

delete from students
where surname = 'Meggiarin';

<!-- abilito nuovamente la modalità di safe update con 👇
SET SQL_SAFE_UPDATES = 1; -->
