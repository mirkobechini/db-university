# Db university


Ogni dipartimento + corsi laurea
ogni corso laurea + corsi
ogni corso + insegnanti
ogni corso + esami
ogni studente 1 solo corso laurea
ogni studente + esami

esame ha il voto


## Tables:
- departments (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.)
- graduation-courses (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- courses (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.)
- teachers
- exams
- students





### Table: teachers

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name
- last_name
- codice fiscale

- courses
- exams

- phone
- address


### Table: students

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name
- last_name
- codice fiscale

- student_number
- iscriptions
- graduation-course
- exams-results

- phone
- address


### Table: exams

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX


### Table: departments

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX


### Table: graduation-courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX


### Table: courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
 





### Pivot Table: 


