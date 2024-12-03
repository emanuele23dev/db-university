# DB_STRUCTURE

Modellare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Dipartimenti

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- name | VARCHAR(50) NOT NULL
- description | TEXT NOT NULL

## Corsi_di_laurea

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- dipartiemnto_id | BIGINT (UNSIGNED)
- name | VARCHAR(50) NOT NULL
- description | TEXT NOT NULL
- years | TINYINT NOT NULL

## Corsi

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- corsi_di_laurea_id | BIGINT (UNSIGNED)
- name | VARCHAR(50) NOT NULL
- description | TEXT NOT NULL
- year | TINYINT NOT NULL

## Insegnanti

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- name | VARCHAR(20) - NOT NULL
- lastname | VARCHAR(20) - NOT NULL
- email | VARCHAR(50) - NOT NULL, UNIQUE
- phone | VARCHAR(20) - NULL

## Esami

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- corsi_id | BIGINT - (UNSIGNED)
- data | DATE - NOT NULL
- orario | TIME - NOT NULL
- numero_studenti | INT - NULL
- place | VARCHAR(50) - NOT NULL

## Studenti

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- corsi_di_laurea_id | BIGINT - (UNSIGNED)
- name | VARCHAR(50) - NOT NULL
- lastname | VARCHAR(50) - NOT NULL
- email | VARCHAR(100) - NOT NULL, UNIQUE
- date_of_birth | DATE - NOT NULL
- codice_fiscale | CHAR(16) - NOT NULL, UNIQUE
- numero_matricola | VARCHAR(10) - NOT NULL, UNIQUE

## Esame_studente

- ID | BIGINT - AUTO_INCREMENT - PRIMARY_KEY (UNIQUE, NOT NULL)
- esami_id | BIGINT - (UNSIGNED)
- studenti_id | BIGINT - (UNSIGNED)
- exam_grade (voto esame) | TINYINT - NOT NULL
- outcome (esito) | BOOLEAN - DEFAULT FALSE
