## Query fatte in classe durante la lezione sulle join

1. Selezionare tutti i corsi che non hanno un sito web (676)
SELECT *
FROM courses
WHERE website IS NULL


2. Selezionare tutti gli insegnanti che hanno un numero di telefono (50)
SELECT *
FROM teachers
WHERE phone IS NOT NULL


3. Selezionare tutti gli appelli d'esame dei mesi di giugno e luglio 2020 (2634)
SELECT *
FROM exams
WHERE YEAR(`date`) = 2020 AND MONTH(`date`) = 06 OR MONTH(`date`) = 07


SELECT *
FROM exams
WHERE `date` LIKE '2020-06-%' OR `date` LIKE '2020-07-%'


SELECT *
FROM exams
WHERE YEAR(`date`) = 2020 AND MONTH(`date`) BETWEEN 06 AND 07


4. Qual è il numero totale degli studenti iscritti? (5000)
SELECT COUNT(*) AS student_number
FROM students
WHERE enrolment_date <= CURDATE()


5. Contare i corsi raggruppati per cfu
SELECT cfu, COUNT(*) as total_courses
FROM courses
GROUP BY cfu


6. Contare gli studenti raggruppati per anno di nascita
SELECT YEAR(date_of_birth) as year_of_birth , COUNT(*) as total_students
FROM students
GROUP BY year_of_birth


7. Selezionare il voto più basso dato ad ogni appello d'esame
SELECT exam_id, MIN(vote) as worst_vote
FROM exam_student
GROUP BY exam_id


8. Contare gli appelli d'esame del mese di luglio raggruppati per giorno
SELECT DAY(`date`) AS `day`, COUNT(*) as total
FROM exams
WHERE MONTH(`date`) = 07
GROUP BY `day`
ORDER BY `day` ASC


9. Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame
SELECT courses.id, degree_id, name, description, period, year, cfu, website, date, hour, location, address
FROM courses
JOIN exams
ON courses.id = exams.course_id
WHERE courses.id = 144


10. Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)
SELECT departments.*
FROM degrees
JOIN departments ON degrees.department_id = departments.id
WHERE degrees.name = "Corso di Laurea in Diritto dell'Economia"


11. Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno
SELECT exams.*
FROM degrees
JOIN courses ON degrees.id = courses.degree_id
JOIN exams ON exams.course_id = courses.id
WHERE degrees.name = "Corso di Laurea Magistrale in Fisica" AND courses.year = 1


12. Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21)
SELECT DISTINCT teachers.*
FROM teachers
JOIN course_teacher ON teachers.id = course_teacher.teacher_id
JOIN courses ON courses.id = course_teacher.course_id
JOIN degrees ON degrees.id = courses.degree_id
WHERE degrees.name = "Corso di Laurea in Lettere"


13. Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)

(nome, cognome, numero registrazione, nomi corsi, id corsi, date esami, voti esami)

SELECT students.name as nome, students.surname as cognome, students.registration_number as n,
courses.id as course_id, courses.name as corso, exams.date as data_esame, exam_student.vote as voto
FROM students
JOIN exam_student ON students.id = exam_student.student_id
JOIN exams ON exams.id = exam_student.exam_id
JOIN courses ON courses.id = exams.course_id
WHERE students.registration_number = 620320 AND  exam_student.vote >= 18
ORDER BY courses.id ASC


14. Selezionare il voto medio di superamento d'esame per ogni corso, con anche i dati del corso di laurea associato, ordinati per media voto decrescente

SELECT courses.name as corso, AVG(exam_student.vote) as voto
FROM exam_student
JOIN exams ON exams.id = exam_student.exam_id
JOIN courses ON courses.id = exams.course_id
JOIN degrees ON degrees.id = courses.degree_id
GROUP BY courses.name
ORDER BY voto DESC