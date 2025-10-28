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


### Table: persons

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name
- last_name
- codice fiscale
- phone
- address


### Table: teachers

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- person_id



### Table: students

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- person_id
- student_number
- iscriptions
- graduation-course_id



### Table: exams

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- teacher_id
- student_id
- course_id
- grade


### Table: departments

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name


### Table: graduation-courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name
- department_id


### Table: courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- graduation-course_id
- teacher_id
 





### Pivot Table: 


