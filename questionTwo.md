### GROUP BY

# 1. Contare quanti iscritti ci sono stati ogni anno

````
SELECT YEAR(`enrolment_date`) AS anno_iscrizione, COUNT(*) AS numero_iscritti
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY `anno_iscrizione`;
````

# 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

````
SELECT `office_address`, COUNT(*) AS 'numero_insegnanti'
FROM `teachers`
GROUP BY `office_address`
````

# 3. Calcolare la media dei voti di ogni appello d'esame

````
SELECT `exam_id`, AVG(`vote`) AS 'media_voti'
FROM `exam_student`
GROUP BY `exam_id`
````

# 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

````
SELECT `departments`.`name`, COUNT(`department_id`) AS 'numero_dipartimenti'
FROM `degrees`
INNER JOIN `departments` ON `departments`.`id` = `department_id`
GROUP BY `departments`.`name`	
````

### JOIN

# 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

````
SELECT `students`.`name`,`students`.`surname`, `degrees`.`name`
FROM `students`
INNER JOIN `degrees` ON `degrees`.`id` = `degree_id`
WHERE `degrees`.`name` LIKE '%Economia%'
````

# 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

````
SELECT *
FROM `degrees`
INNER JOIN `departments` ON `departments`.`id` = `department_id`
WHERE `departments`.`name` LIKE '%Neuroscienze%' AND `degrees`.`level` = 'magistrale'

````

# 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

````
SELECT *
FROM `courses`, `course_teacher`
INNER JOIN `teachers` ON `teachers`.`id` = `teacher_id`
WHERE `teachers`.`id` = 44
````

# 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

````
SELECT *
FROM `students`
INNER JOIN `degrees` ON `students`.`id` = `degree_id`
INNER JOIN `departments` ON `departments`.`id` =  `department_id`
ORDER BY `students`.`surname`, `students`.`name`  
````

# 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

````
SELECT `degrees`.`name` AS corso_laurea,`courses`.`name` AS corso, `teachers`.`surname` AS cognome_insegnante, `teachers`.`name` AS nome_insegnante
FROM `degrees`
INNER JOIN `courses` ON `courses`.`id` = `degree_id`
INNER JOIN `course_teacher` ON `courses`.`id` = `course_id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
````

# 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

````
SELECT `teachers`.*
FROM `teachers`
INNER JOIN `course_teacher` ON `teachers`.`id` = `teacher_id`
INNER JOIN `courses` ON `course_id` = `courses`.`id`
INNER JOIN `degrees` ON `degree_id` = `degrees`.`id`
INNER JOIN `departments` ON `department_id` = `departments`.`id`
WHERE `departments`.`name` LIKE '%Matematica%';
````
