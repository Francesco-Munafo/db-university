
1. Selezionare tutti gli studenti nati nel 1990 (160)

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

3. Selezionare tutti gli studenti che hanno più di 30 anni

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

6. Selezionare tutti i corsi di laurea magistrale (38)

7. Da quanti dipartimenti è composta l'università? (12)

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)


/* LIVE CODING 18/10/2023 */


9. Selezionare tutti i corsi del Corso di Laurea in Informatica (22)

10. Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame

11. Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto
dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)

12. Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del
primo anno

13. Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21)

14. Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)



1. SELECT * FROM `students` WHERE `date_of_birth` LIKE '1990-%';

2. SELECT * FROM `courses` WHERE `cfu` > 10;

3. SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

4. SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

5. SELECT * FROM `exams` WHERE TIME(`hour`) >= '14:00' AND `date` LIKE '2020-06-20';

6. SELECT * FROM `degrees` WHERE `level` = 'magistrale';

7. SELECT COUNT(*) AS 'total_departments' FROM `departments`;

8. SELECT COUNT(*) AS 'no_phone_teacher' FROM `teachers` WHERE `phone` IS NULL;



/* LIVE CODING 18/10/2023 */



9. SELECT `courses`.`id`, `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `courses`.`website`, `degrees`.`name` AS `degree_name`
    FROM `courses`
    JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
    WHERE `degrees`.`name` = 'Corso di Laurea in Informatica';


10. SELECT `courses`.`id` AS `course_id`, `courses`.`name`, `courses`.`description`, `courses`.`period`, `courses`.`cfu`, `courses`.`year`, `courses`.`website`, `exams`.`id` AS `exam_id`, `exams`.`date`, `exams`.`hour`, `exams`.`location`, `exams`.`address`
FROM `courses`
JOIN `exams` ON `courses`.`id` = `exams`.`course_id`
WHERE `courses`.`id` = 144;

11. SELECT `departments`.*
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE`degrees`.`name` = 'Corso di Laurea in Diritto dell\'Economia';

12. SELECT `courses`.`name`, `courses`.`period`, `courses`.`cfu`, `exams`.`date`, `exams`.`hour`, `exams`.`location`, `exams`.`address` 
FROM `degrees` 
JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` 
JOIN `exams` ON `exams`.`course_id` = `courses`.`id`
WHERE `courses`.`year` = 1 AND `degrees`.`name` = 'Corso di Laurea Magistrale in Fisica';

13. SELECT DISTINCT `teachers`.*
FROM `teachers`     
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Lettere'
ORDER BY `teachers`.`surname` ASC;

14. SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `courses`.`id`, `courses`.`name`, `courses`.`date`, `exams_student`.`vote`
FROM `exam_student`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
WHERE `students`.`name` = 'Mirco Messina' AND `exams_student`.`vote` >= 18