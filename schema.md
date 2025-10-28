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
- name: VARCHAR(100) NOT NULL
- last_name: VARCHAR(100) NOT NULL
- codice_fiscale: CHAR(13) NOT NULL
- phone: CHAR(10) NOT NULL
- address: VARCHAR(200) NULL


### Table: teachers

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- person_id: FK
- qualification: VARCHAR(50) NOT NULL




### Table: students

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- person_id FK
- student_number: VARCHAR(15)
- inscriptions
- graduation-course_id: FK



### Table: exams

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- teacher_id FK
- student_id FK
- course_id FK
- grade: TINYINT NOT NULL
- date: DATETIME NOT NULL


### Table: departments

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name: VARCHAR(100) NOT NULL


### Table: graduation-courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name: VARCHAR(100) NOT NULL
- department_id FK


### Table: courses

- id: INT || BIGINT AUTO_INCREMENT NOT NULL UNIQUE PK INDEX
- name: VARCHAR(100) NOT NULL
- graduation-course_id FK
- cfu: TINYINT NULL
 

### Pivot Table: student-course

- student_id
- course_id


### Pivot Table: teacher-course

- teacher_id
- course_id