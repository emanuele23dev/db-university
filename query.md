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

```sql
select count(*) as courses_numb, name as every_department
from courses
group by every_department
```

# Joins:

# Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
select students.id as student_id,
students.name as student_name,
students.surname as student_surname
from students
join degrees
on students.degree_id = degrees.id
where degrees.name = 'Corso di Laurea in Economia'
```

# Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
select degrees.id as degree_id,
degrees.level as degree_level
from degrees
join departments
on degrees.department_id = departments.id
where departments.name = 'Dipartimento di Neuroscienze'
and degrees.level = 'magistrale'
```

# Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
select courses.id as course_id,
courses.name as course_name,
courses.period,
courses.year,
courses.cfu
from courses
join course_teacher on courses.id = course_teacher.course_id
join teachers on course_teacher.teacher_id = teachers.id
where teachers.id = 44
```

# Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
select students.id as student_id,
students.name as student_name,
students.surname as student_surname,
degrees.id as degree_id,
degrees.name as degree_name,
departments.id as department_id,
departments.name as department_name
from students
join degrees on students.degree_id = degrees.id
join departments on degrees.department_id = departments.id
order by students.surname, students.name
```

# Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
select degrees.id as degree_id,
degrees.name AS degree_name,
courses.id AS course_id,
courses.name AS course_name,
teachers.id AS teacher_id,
teachers.name AS teacher_name,
teachers.surname AS teacher_surname
from degrees
join courses on degrees.id = courses.degree_id
join course_teacher on courses.id = course_teacher.course_id
join teachers on course_teacher.teacher_id = teachers.id
```

# Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
select distinct teachers.id as teacher_id,
teachers.name as teacher_name,
teachers.surname as teacher_surname
from teachers
join course_teacher on teachers.id = course_teacher.teacher_id
join courses on course_teacher.course_id = courses.id
join degrees on courses.degree_id = degrees.id
join departments on degrees.department_id = departments.id
where departments.name = 'Dipartimento di Matematica'
```

# BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame,

# stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
