Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

-sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);

-ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)

-ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);

-ogni Corso può essere tenuto da diversi Insegnanti;

-ogni Corso prevede più appelli d’Esame;

-ogni Studente è iscritto ad un solo Corso di Laurea;

-ogni Studente può iscriversi a più appelli di Esame;

-per ogni appello d’Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.


# University_DB

## Model

- Department

## Table name

- departments

## Table columns

- id | PK, UNIQUE, NOT_NULL, AI <ONETOMANY>
- name | VARCHAR(50), NOT_NULL, UNIQUE, INDEX

-----------------------

## Model

- Major

## Table name

- majors(CDL)

## Table columns

- id | PK, UNIQUE, NOT_NULL, AI
- department_id | UNIQUE, NOT_NULL, VARCHAR(10)
- name | NOT_NULL, UNIQUE, INDEX, VARCHAR(50)
- type | VARCHAR(13), NOT_NULL, INDEX
- code/cl | VARCHAR(8), UNIQUE, NOT_NULL
- teacher_id | FK, UNIQUE, NOT_NULL
- student_id | FK, UNIQUE, NOT NULL
- limited_enrollment | TINYINT(2), DEFAULT(0), NOT_NULL //Sets true or false to identify if a major has a max number of students
- max_students | TINYINT(100), DEFAULT(0), NULL

-----------------------

## Model

- Course(materia)

## Table name

- courses

## Table columns

- id | PK, UNIQUE, NOT_NULL, AI
- code | NOT_NULL, UNIQUE, TINYINT(6)
- name | VARCHAR(50), UNIQUE, NOT_NULL, INDEX
- teacher_id | FK
- student_id | FK
- classroom | VARCHAR(15), UNIQUE, NOT_NULL
- department_id | FK
- mandatory | TINYINT(2), DEFAULT(0), NOT_NULL //Sets true or false to identify if a course has a mandatory attendance

---------------------


## Model

- Teacher

## Table name

- teachers

## Table columns

- id | PK
- teacher_matricolation VARCHAR(10), UNIQUE, NOT_NULL
- name | VARCHAR(50), NOT_NULL
- department_id | FK
- courses_id | FK 



----------------------

## Model

- Round(appelli)

## Table name

- rounds

## Table columns

- id | PK
- courses_id | FK
- teachers_id | FK
- classroom | VARCHAR(15), UNIQUE, NOT_NULL
- student_id | FK
- start_enrollment_date(finestra d'iscrizione) | NOT_NULL, DATE
- end_enrollment_date | NOT_NULL, DATE
- exam_date(data dell'appello)
- vote
- accepted


----------------

## Model

- Student

## Table name

- students

## Table columns

- id
- student_id
- name
- rounds


------------------------

## Model

- Grade

## Table name

- grades

## Table columns

- id | PK
- student_id
- round_id
- grade | SMALLINT(30)







