# Домашнее задание к занятию «Базы данных» - Михайлов Дмитрий

---
### Легенда

Заказчик передал вам [файл в формате Excel](https://github.com/netology-code/sdb-homeworks/blob/main/resources/hw-12-1.xlsx), в котором сформирован отчёт. 

На основе этого отчёта нужно выполнить следующие задания.

### Задание 1

Опишите не менее семи таблиц, из которых состоит база данных:

- какие данные хранятся в этих таблицах;
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- ...
- идентификатор структурного подразделения, внешний ключ, integer).

### Решение 1

Сотрудники (
- идентификатор, первичный ключ, serial,
- Фамилия, varchar,
- Имя, varchar,
- Отчество, varchar,
- Дата найма, date,
- Пол, check,
- Оклад - идентификатор Окладов, внешний ключ, integer
- Должность - идентификатор Должностей, внешний ключ, integer
- Тип подразделения 
- Структурное подразделение и тип подразеделения- идентификатор структурного подразделения, составной ключ - внешний ключ, integer
- Адрес филиала - идентификатор Адреса филиалов, внешний ключ, integer
- Проект на который назначен - идентификатор Проекты, внешний ключ, integer )

Оклад (
- идентификатор, первичный ключ, serial,
- Структурное подразделение, внешний ключ, integer,
- Тип подразделения, text,
- Должность, text,
- Город, text,
- Проект на который назначен, varchar )

Должности (
- идентификатор, первичный ключ, serial,
- Наименование должности, text,
- Структурное подразделение, внешний ключ, integer,
- Тип подразделения, внешний ключ, integer )

Структурные подразделения (
- идентификатор, первичный ключ, serial,
- Наименование структурного подразделения, text )

Типы подразделений (
- идентификатор, первичный ключ, serial,
- Тип подразделения, varchar )

Адрес филиала (
- идентификатор, первичный ключ, serial,
- Наименование филиала, text,
- Адрес филиала, text,
- Руководитель филиала, text
- Контактный номер телефона филиала, char(11) )

Проекты (
- идентификатор, первичный ключ, serial,
- Наименование проекта
- Дата начала/создания проекта, date, 
- Дата окончания проекта, date,
- Структурное подразделение
- Тип подразделения
- Должность)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.


### Задание 2*

Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.
