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
| date_of_birth | date            | Дата рождения |           |

### SQL код:  
```SQL
CREATE TABLE student (
	n_z INTEGER PRIMARY KEY,
	name VARCHAR(255),
	surname VARCHAR(255),
	group_num INTEGER,
	score NUMERIC(3,2),
	address VARCHAR(2000),
	date_of_birth DATE,
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
