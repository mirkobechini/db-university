## Group by
# Contare quanti iscritti ci sono stati ogni anno
SELECT YEAR(enrolment_date) as `year`, COUNT(*)
FROM students
GROUP BY `year`

# Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT office_address as building, COUNT(*)
FROM teachers
GROUP BY building

# Calcolare la media dei voti di ogni appello d'esame
SELECT exam_student.exam_id as exam , AVG(vote) as vote
FROM exam_student
GROUP BY exam

# Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT department_id as department, COUNT(*)
FROM degrees
GROUP BY department


## Joins:
# Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT students.id as `id`, students.name as `name`, degrees.name as Corso
FROM students
JOIN degrees ON degrees.id = students.degree_id
WHERE degrees.name = "Corso di Laurea in Economia"

# Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT degrees.name as `Corso laurea`, courses.name as `corsi`
FROM departments
JOIN degrees ON departments.id = degrees.department_id
JOIN courses ON courses.degree_id = degrees.id
WHERE departments.name = "Dipartimento di Neuroscienze" AND degrees.name LIKE "Corso di Laurea Magistrale%"

# Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT teachers.name as teacher, courses.name as corsi
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id = 44

# Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT *
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON departments.id = degrees.department_id
ORDER BY students.surname, students.name ASC

# Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT degrees.name as lauree, courses.name as corsi, teachers.name as insegnanti
FROM degrees
JOIN courses ON degrees.id = courses.degree_id
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON teachers.id = course_teacher.teacher_id

# Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT teachers.*
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON courses.id = course_teacher.course_id
JOIN degrees ON degrees.id = courses.degree_id
JOIN departments ON departments.id = degrees.department_id
WHERE departments.name = "Dipartimento di Matematica"

## BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
SELECT students.name as nome, students.surname as cognome, students.registration_number as matricola, exams.course_id as esame, COUNT(exams.course_id) as tentativi, MAX(vote) as `voto`
FROM students
JOIN exam_student ON students.id = exam_student.student_id
JOIN exams ON exams.id = exam_student.exam_id
GROUP BY students.id, esame
HAVING voto >=18
