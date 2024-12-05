## 1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
select *
from students
where YEAR(date_of_birth) = 1990;
```

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
select *
from courses
where cfu > 10;
```

## 3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT *
from students
where timestampdiff(YEAR, date_of_birth, CURDATE()) > 30;
```

## 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql
SELECT *
from courses
where year = 1
and period = "I semestre"
```

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT *
from exams
where date = '2020-06-20'
and hour > '14:00:00';
```

## 6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT *
from degrees
where level = 'magistrale';
```

## 7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT *
from departments
```

## 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT *
from teachers
where phone;
```

## 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

```sql
insert into students (degree_id, name, surname, date_of_birth, fiscal_code, enrolment_date, registration_number, email)

value (23, 'Emanuele', 'Meggiarin', '1988-06-23', 'XYZABC12D34E567F', '2021-09-01', '620037', 'emanuele@gmail.it')
```

<!-- Numero totale di record con 👇
SELECT COUNT(*) FROM students; -->

## 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```sql
update teachers
set office_number = 126
where id = 58
```

## 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

<!-- disabilito temporaneamente la modalità di safe update con 👇
SET SQL_SAFE_UPDATES = 0; -->

```sql
delete from students
where surname = 'Meggiarin';
```

<!-- abilito nuovamente la modalità di safe update con 👇
SET SQL_SAFE_UPDATES = 1; -->

# Group by:

# Contare quanti iscritti ci sono stati ogni anno

```sql
select count(*) as enrolments_numb, year(enrolment_date) as year_of_enrolment
from students
group by year_of_enrolment
```

# Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
select count(*) as numb_of_teachers, office_address as same_place_office
from teachers
group by same_place_office
```

# Calcolare la media dei voti di ogni appello d'esame

```sql
select exam_id, avg(vote) as avg_vote
from exam_student
group by exam_id
```

# Contare quanti corsi di laurea ci sono per ogni dipartimento

# Joins:

Selezionare tut# ti gli studenti iscritti al Corso di Laurea in Economia
Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
