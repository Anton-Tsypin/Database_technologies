# Задание 2. SQL запросы.

## Однотабличные запросы

1. Вывести всеми возможными способами имена и фамилии студентов, средний балл которых от 4 до 4.5

```SQL
SELECT name, surname FROM student
WHERE score >= 4 AND score <= 4.5;
```

2. Познакомиться с функцией CAST. Вывести при помощи неё студентов заданного курса (использовать Like)

```SQL
SELECT * FROM student
WHERE CAST(group_num AS character) LIKE '4%';
```

3. Вывести всех студентов, отсортировать по убыванию номера группы и имени от а до я

```SQL
SELECT * FROM student
ORDER BY group_num, name;
```

4. Вывести студентов, средний балл которых больше 4 и отсортировать по баллу от большего к меньшему

```SQL
SELECT * FROM student
WHERE score >= 4
ORDER BY score DESC;
```

5. Вывести на экран название и риск футбола и хоккея

```SQL
SELECT name, risk FROM hobby
WHERE name = 'Футбол' OR name = 'Программирование';
```

6. Вывести id хобби и id студента которые начали заниматься хобби между двумя заданными датами (выбрать самим) и студенты должны до сих пор заниматься хобби

```SQL
SELECT id_hobby, n_z FROM student_hobby
WHERE date_start BETWEEN '12.10.1990' AND '01.01.2010'
AND date_finish IS null;
```

7. Вывести студентов, средний балл которых больше 4.5 и отсортировать по баллу от большего к меньшему

```SQL
SELECT * FROM student
WHERE score > 4.5
ORDER BY score DESC;
```

8. Из запроса №7 вывести несколькими способами на экран только 5 студентов с максимальным баллом

```SQL
SELECT * FROM student
WHERE score = 5;
```

9. Выведите хобби и с использованием условного оператора сделайте риск словами:
 
   \>=8 - очень высокий  
   \>=6 & <8 - высокий  
   \>=4 & <8 - средний  
   \>=2 & <4 - низкий  
   \<2 - очень низкий  

```SQL
SELECT id, name,
CASE
  WHEN risk >= 0.8 THEN 'очень высокий'
  WHEN risk >= 0.6 AND risk < 0.8 THEN 'высокий'
  WHEN risk >= 0.4 AND risk < 0.6 THEN 'средний'
  WHEN risk >= 0.2 AND risk < 0.4 THEN 'низкий'
  WHEN risk < 0.2 THEN 'очень низкий'
END AS risk
FROM hobby;
```

10. Вывести 3 хобби с максимальным риском

```SQL
SELECT * FROM hobby
ORDER BY risk DESC
LIMIT 3;
```
