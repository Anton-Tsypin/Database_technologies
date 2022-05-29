# Проект

## Задание

| Пользователь | Действие |
| --- | --- |
|Администратор | Добавление нового сотрудника |
| Администратор | Выдача прав по доступу в определённые помещения (единичное, временное, постоянное) |
| Сотрудник | Попытка прохода в определенное помещение |
| Администратор | Уведомления о попытке прохода без разрешения |
| Сотрудник | Запрос доступа для прохода (разовое, временное) |
| Администратор | Просмотр списка всех пользователей с поиском по: правам, фамилии/имени/отчеству, по активности. Сортировка по: активности последней, пагинация |
| Администратор | Просмотр всех действий конкретного пользователя (время входа, время выхода; поиск по помещению, пагинация) |
| Администратор | Некоторые помещения должны иметь максимальное время нахождения в них, уведомлять администратора если сотрудник превышает это время. Записывать такие инциденты в базу |
| Администратор | Забрать права (Предусмотреть случай, когда сотрудник вошёл в помещение и у него забрали права на выход) |
| Администратор | Просмотр всех инцидентов (сортировка по дате, сотруднику). Возможность решить инцидент (записать решение) |

## Реализация

### Создание таблиц
```SQL
CREATE TABLE room(
        id serial PRIMARY KEY,
        name varchar(64)
);

CREATE TABLE user_(
        id serial PRIMARY KEY,
        name varchar(32),
        role varchar(16) DEFAULT 'worker',
        room_id integer,
        FOREIGN KEY (room_id) REFERENCES room(id)
);

CREATE TABLE access(
        id serial PRIMARY KEY,
        duration varchar(32),
        user_id integer,
        room_id integer,
        FOREIGN KEY (user_id) REFERENCES user_(id),
        FOREIGN KEY (room_id) REFERENCES room(id)
);

CREATE TABLE action(
        id serial PRIMARY KEY,
        user_id integer,
        room_id integer,
        access_id integer,
        FOREIGN KEY (user_id) REFERENCES user_(id),
        FOREIGN KEY (room_id) REFERENCES room(id),
        FOREIGN KEY (access_id) REFERENCES access(id)
);

CREATE TABLE incident(
        id serial PRIMARY KEY,
        user_id integer,
        FOREIGN KEY (user_id) REFERENCES user_(id)
);
```
### SQL запросы

#### Создание комнат

```SQL
INSERT INTO room(id, name)
VALUES (1, 'office');
```

#### Создание админа только через запрос

```SQL
INSERT INTO user_(id, name, room_id, role)
VALUES (1, 'Vasya', 1, 'admin');

INSERT INTO access(id, duration, user_id, room_id)
VALUES (1, 'permanent', 1, 1);
```

```SQL


```
