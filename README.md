* `\c` -- показывает в какой бд мы находимся и через какого юзера

* `\c name_of_db` -- переключается к этой бд

* `\l` -- показывает все бд

* `\dt` -- показывает все таблицы в бд

* `\du` -- показывает всех юзеров

* `\q` -- выход

```sql
CREATE DATABASE name_of_db; -- создает базу данных
```

```sql
CREATE TABLE name_of_table (
    name_of_column1 data_type constraint,
    name_of_column2 data_type constraint.
    ...
); -- создает таблицу с полями
```
```sql
INSERT INTO name_of_table (name_of_column1, name_of_column2)
VALUES (val1, val2); -- добавляет запись в таблицу
```

```sql
SELECT * FROM name_of_table; -- достает все поля и записи из таблицы
SELECT name_of_column1, name_of_column2 FROM name_of_table; -- достает только указанные столбцы из таблицы
```

> primary key (pk) -- первичный ключ
> это ограничение, которые мы указываем на те поля, которые должны быть уникальными для того, что бы потом их использовать в связях (например id)

> foreign key (fk) -- внешний ключ
> это ограничение, которое мы указываем на те поля, которые будут ссылаться на pk в другой таблице, для создания связи

```sql
CREATE TABLE author (
    id serial primary key,
    first_name varchar(50),
    last_name varchar(50)
);

CREATE TABLE book (
    id serial,
    title varchar(100),
    published year,
    author_id int foreign key references author (id)
);
```
## виды связей(теория)
> one to one -- (один к одному)
например:

* один автор -- одна биография

* один флаг -- одна страна

* один человек -- одно сердце


> one to many -- (один ко многим)
например:

* один человек -- много клеток, но у одной клетки только один человек

* одни родители -- много детей, но у одного ребенка только одни родители

* один аккаунт -- много постов, но у одного поста только один автор (аккаунт)

* один makers -- много maker'ов, но у одного maker'a только один makers


> many to many -- (многие ко многим)
например:

* у человека много друзей и у одного друга много других друзей

* у доктора много пациентов и у пациента много докторов

* у пользователя много социальных сетей и у одной соцсети много пользователей


## виды связей(практика)
### one to one
```sql
CREATE TABLE flag (
    id serial primary key,
    photo text
);

CREATE TABLE country (
    id serial primary key,
    title varchar(50),
    gimn text,
    flag_id int,
    constraint fk_country_flag foreign key flag_id references flag(id)
);
```

### one to many
```sql
CREATE TABLE account (
    id serial primary key,
    nickname varchar(25) unique,
    u_password varchar(255)
);

CREATE TABLE post (
    id serial primary key,
    title varchar(100),
    body text,
    photo text,
    account_id int,
    constraint fk_account_post foreign key account_id references account(id)
);
```

### many to many
```sql
CREATE TABLE doctor (
    id serial primary key,
    first_name varchar(25),
    last_name varchar(50)
);

CREATE TABLE patient (
    id serial primary key,
    first_name varchar(25),
    last_name varchar(50)
);

CREATE TABLE doctor_patient (
    doctor_id int,
    patient_id int,

    constraint fk_doctor foreign key (doctor_id) references doctor(id),
    constraint fk_patient foreign key (patient_id) references patient(id)

);
```

## joins
> JOIN -- инструкция, которая позволякт в запросах SELECT брать данные из нескольких таблиц

> INNER JOIN (JOIN) -- когда достаются только те записи, у которых есть полная связь

> FULL JOIN -- когда достаются абсолютна все записи со всех таблиц

> LEFT JOIN -- когда достаются все записи с 'левой' таблицы и так же те записи с полной связью

> RIGHT JOIN -- когда достаются все записи с 'правой' таблицы и так же те записи с полной связью

```sql
SELECT author.first_name, book.title
FROM author
JOIN book ON author.id = book.author_id;
```

# import export данных
write from file to db
```bash
psql db_name < file.sql
```
```bash

```