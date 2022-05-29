# Проект

## Задание

| Пользователь | Действие |
| --- | --- |
| Администратор | Добавление нового сотрудника |
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
        name varchar(64),
        hours integer DEFAULT null
);

CREATE TABLE user_(
        id serial PRIMARY KEY,
        name varchar(32),
        role varchar(16) DEFAULT 'worker',
        current_room_id integer DEFAULT null,
        FOREIGN KEY (current_room_id) REFERENCES room(id)
);

CREATE TABLE access(
        id serial PRIMARY KEY,
        duration varchar(32),
        hours integer DEFAULT null,
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

CREATE TABLE attempt(
        id serial PRIMARY KEY,
        success boolean,
        user_id integer,
        room_id integer,
        access_id integer DEFAULT null,
        FOREIGN KEY (user_id) REFERENCES user_(id),
        FOREIGN KEY (room_id) REFERENCES room(id),
        FOREIGN KEY (access_id) REFERENCES access(id)
);

CREATE TABLE incident(
        id serial PRIMARY KEY,
        user_id integer,
        room_id integer,
        attempt_id integer,
        FOREIGN KEY (user_id) REFERENCES user_(id),
        FOREIGN KEY (room_id) REFERENCES room(id),
        FOREIGN KEY (attempt_id) REFERENCES attempt(id)
);
```
### SQL запросы

#### Создание комнат

```SQL
INSERT INTO room(id, name) VALUES (1, 'office')
INSERT INTO room(id, name) VALUES (2, 'storage')
INSERT INTO room(id, name) VALUES (3, 'toilet')
INSERT INTO room(id, name) VALUES (4, 'secret_room')
```

#### Создание админа только через запрос

```SQL
INSERT INTO user_(id, name, current_room_id, role) VALUES (1, 'Vasya', 1, 'admin');
INSERT INTO access(id, duration, user_id, room_id) VALUES (1, 'permanent', 1, 1);
```

#### Администратор. Добавление нового сотрудника 
```SQL
INSERT INTO user_(name, room_id) VALUES ('Petya', 1);
INSERT INTO user_(name, room_id) VALUES ('Ivan', 1);
INSERT INTO user_(name, room_id) VALUES ('Evgeniy', 1);
INSERT INTO user_(name, room_id) VALUES ('Michael', 1);
```

#### Администратор. Выдача прав по доступу в определённые помещения (единичное, временное, постоянное)
```SQL
INSER INTO access(duration, user_id, room_id) VALUES ('one-time', 2, 4);
INSER INTO access(duration, hours, user_id, room_id) VALUES ('temporary', 8, 1, 2);
INSER INTO access(duration, user_id, room_id) VALUES ('permanent', 3, 3);
```

#### Сотрудник. Попытка прохода в определенное помещение
```SQL
IF (SELECT id FROM access WHERE user_id = 2 AND room_id = 4) THEN
INSERT INTO attempt(success, user_id, room_id, access_id) VALUES ('true', 2, 4, SELECT id FROM access WHERE user_id = 2 AND room_id = 4)

ELSE
INSERT INTO attempt(success, user_id, room_id) VALUES ('false', 2, 4)
INSERT INTO incident(user_id, room_id, acce) VALUES (2, 4, SELECT id FROM attemp WHERE success = 'false' , user_id = 2, room_id = 4)

END IF
```
#### Администратор. Уведомления о попытке прохода без разрешения
```SQL

```

#### Сотрудник. Запрос доступа для прохода (разовое, временное)
```SQL

```

#### Администратор. Просмотр списка всех пользователей с поиском по: правам, фамилии/имени/отчеству, по активности. Сортировка по: активности последней, пагинация
```SQL

```

#### Администратор. Просмотр всех действий конкретного пользователя (время входа, время выхода; поиск по помещению, пагинация)
```SQL

```

#### Администратор. Некоторые помещения должны иметь максимальное время нахождения в них, уведомлять администратора если сотрудник превышает это время. Записывать такие инциденты в базу
```SQL

```

#### Администратор. Забрать права (Предусмотреть случай, когда сотрудник вошёл в помещение и у него забрали права на выход)
```SQL

```

#### Администратор. Просмотр всех инцидентов (сортировка по дате, сотруднику). Возможность решить инцидент (записать решение)
```SQL

```
