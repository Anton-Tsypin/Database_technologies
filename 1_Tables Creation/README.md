# Задание 1. Создание таблиц.

## Таблица student
| Атрибут       | Тип и размер    | Смысл         | Ключ      |
| :------------ | :-------------  | :------------ | :-------- |
| n_z           | integer         | Номер зачётки | Первичный |
| name          | character(255)  | Имя           |           |
| surname       | character(255)  | Фамилия       |           |
| group_num     | integer         | Номер группы  |           |
| score         | numeric(3, 2)   | Средний балл  |           |
| adress        | character(1024) | Адрес         |           |
| date_birth    | date            | Дата рождения |           |

### SQL код:  
```SQL
CREATE TABLE student (
	n_z INTEGER PRIMARY KEY,
	name VARCHAR(255),
	surname VARCHAR(255),
	group_num INTEGER,
	score NUMERIC(3,2),
	address VARCHAR(2000),
	date_birth DATE,
	CONSTRAINT valid_group_num CHECK ((group_num >= 1000) AND (group_num <= 9999)),
	CONSTRAINT valid_score CHECK ((score >= (2)::numeric) AND (score <= (5)::numeric))
);
```
  
## Таблица hobby
| Атрибут | Тип и размер   | Смысл     | Ключ      |
| :------ | :------------- | :-------- | :-------- |
| id      | serial         | Номер     | Первичный |
| name    | character(255) | Название  |           |
| risk    | numeric(3,2)   | Опасность |           |

### SQL код:  
```SQL
CREATE TABLE hobby (
	id SERIAL PRIMARY KEY,
	name VARCHAR(255),
	risk NUMERIC(3,2),
	CONSTRAINT valid_risk CHECK ((((risk >= (0)::numeric) AND (risk <= (1)::numeric))))
);
```
  
## Таблица student_hobby
| Атрибут       | Тип и размер | Смысл          | Ключ      |
| :------------ | :----------- | :------------- | :-------- |
| id            | serial       | Номер          | Первичный |
| n_z           | integer      | Номер зачётки  | Внешний   |
| id_hobby      | integer      | Номер хобби    | Внешний   |
| date_start    | date         | Дата начала    |           |
| date_finish   | date         | Дата окончания |           |

### SQL код:  
```SQL
CREATE TABLE student_hobby (
	id SERIAL PRIMARY KEY,
	n_z INTEGER,
	id_hobby INTEGER,
	date_start DATE,
	date_finish DATE,
	CONSTRAINT fk_id_hobby FOREIGN KEY (id_hobby) REFERENCES hobby (id),
	CONSTRAINT fk_n_z FOREIGN KEY (n_z) REFERENCES students (n_z)
);
```

# Заполнение таблиц данными

### Внесение данных о студентах
```SQL
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (123123, 'Иван', 'Иванов', 2222, '09-09-1990', 'город Дубна', 4.02);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (234234, 'Михаил', 'Михайлов', 4032, '03-12-1997', 'город Ялта', 3.25);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (345345, 'Виктория', 'Николаева', 4011, '11-23-1994', 'город Дубна', 4.23);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (456456, 'Нуль', 'Нулёвый', 2222, '04-05-1998', 'город Омск', 4.23);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (567567, 'Евгения', 'Сидорова', 2222, '04-05-1996', null, 4.59);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (678678, 'Сергей', 'Иванцов', 3011, '12-24-1995', 'город Москва', 3.85);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (789789, 'Николай', 'Борисов', 3011, '12-08-1999', 'город Челябинск', 4.22);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (890890, 'Виктория', 'Воронцов', 3011, null, 'город Дубна', 4.63);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (321321, 'Марина', 'Кузнецов', 3011, '01-25-1996', 'город Дубна', 4.11);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (432432, 'Джон', 'Уик', 3011, null, 'город Челябинск', 3.45);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (534543, 'Виктор', 'Корнеплод', 3011, '11-23-1994', 'город Дубна', 2.98);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (654654, 'Артём', 'Иван', 2222, '05-28-1999', 'город Дубна', 4.03);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (765765, 'Шарлотта', 'Калла', 2222, '05-23-1996', null, 4.67);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (867867, 'Юлия', 'Белорукова', 4011, '11-28-1996', 'город Дубна', 3.58);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (987987, 'Татьяна', 'Акимова', 4011, '01-23-1995', 'город Ялта', 4.98);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (123234, 'Ульяна', 'Кайшева', 4011, '03-03-1999', 'город Дубна', 4.47);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (234345, 'Никита', 'Крюков', 4011, '08-04-1999', 'город Омск', 2.55);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (345456, 'Иван', 'Шаповалов', 4032, '04-29-2001', 'город Ялта', 2.1);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (456567, 'Анастасия', 'Овсянникова', 4032, '12-31-1998', 'город Дубна', 4.25);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (567678, 'Людмила', 'Иванова', 4032, '05-02-1993', 'город Ялта', 3.75);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (678789, 'Валентина', 'Сидорова', 4032, null, 'город Дубна', 3.78);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (789890, 'Помор', 'Поморов', 4222, '04-22-1981', 'город Архангельск', 4.98);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (342321, 'Евгений', 'Онегин', 3242, '04-22-1982', 'город Архангельск', 3.48);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (453432, 'Григорий', 'Печорин', 1232, '04-22-1983', 'город Архангельск', 4.38);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (543432, 'Илья', 'Обломов', 2222, '04-22-1984', 'город Архангельск', 4.18);
INSERT INTO student (n_z, name, surname, group_num, date_birth, address, score) VALUES (654543, 'Поручик', 'Ржевский', 4011, '04-22-1985', 'город Архангельск', 3.92);
```
  
### Внесение данных о хобби
```SQL
INSERT INTO hobby (id, risk, name) VALUES (1, 0.5, 'Футбол');
INSERT INTO hobby (id, risk, name) VALUES (2, 0.2, 'Теннис');
INSERT INTO hobby (id, risk, name) VALUES (3, 0.5, 'Баскетбол');
INSERT INTO hobby (id, risk, name) VALUES (4, 0.3, 'Биатлон');
INSERT INTO hobby (id, risk, name) VALUES (5, 0.6, 'Лыжные');
INSERT INTO hobby (id, risk, name) VALUES (6, 0.3, 'Волейбол');
INSERT INTO hobby (id, risk, name) VALUES (7, 0.7, 'Фехтование');
INSERT INTO hobby (id, risk, name) VALUES (8, 0.1, 'Музыка');
INSERT INTO hobby (id, risk, name) VALUES (9, 0.9, 'Прыжки с парашютом');
INSERT INTO hobby (id, risk, name) VALUES (10, 0.0, 'Рисование');
INSERT INTO hobby (id, risk, name) VALUES (11, 0.2, 'Программирование');
INSERT INTO hobby (id, risk, name) VALUES (12, 0.1, 'Базы данных');
INSERT INTO hobby (id, risk, name) VALUES (13, 0.8, 'Дайвинг');
```

### Внесение данных о хобби студентов
```SQL
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (1, 123123, 3, '03-15-2004', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (2, 123123, 5, '02-18-2009', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (3, 123123, 4, '11-12-1993', '12-11-2016');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (4, 345345, 5, '03-14-2004', '05-03-2006');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (5, 234234, 8, '06-18-2014', '08-09-2017');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (6, 678678, 7, '03-19-2018', '03-15-2017');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (7, 765765, 4, '04-07-2017', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (8, 765765, 2, '11-09-2018', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (9, 345345, 1, '02-28-2019', '03-02-2019');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (10, 456456, 4, '12-19-2009', '12-24-2009');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (11, 765765, 5, '06-18-2013', '09-25-2018');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (12, 345345, 6, '06-18-2014', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (13, 456456, 11, '01-23-1999', '04-14-2001');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (14, 567567, 1, '07-19-2017', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (15, 678678, 13, '02-13-2018', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (16, 123234, 11, '02-28-2019', '04-02-2012');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (17, 456456, 9, '12-19-2009', '11-23-2005');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (18, 234345, 5, '06-18-2013', '09-25-2008');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (19, 345345, 8, '06-18-2014', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (20, 456567, 7, '01-23-1999', '04-14-2014');
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (21, 654654, 13, '07-19-2017', null);
INSERT INTO student_hobby (id, n_z, id_hobby, date_start, date_finish) VALUES (22, 678678, 12, '02-13-2018', null);
```
