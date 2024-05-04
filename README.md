# Домашнее задание к занятию «Базы данных» - Михайлов Дмитрий



Правки вторые от преподавателя следующие:

Проект базы данных становится все лучше и лучше, осталось несколько небольших комментариев:
* ФИО должно храниться в разных столбцах таблицы Сотрудники. Это связано с тем, что для аналитики может быть нужна, к примеру, только фамилия, а вычленять силами бд - это затратная операция. - *Я переделал. Теперь Фамилия Имя Отчество отдельные поля.*
* В таблице Позиция должен быть внешний ключ на Оклад (у вас наоборот), иначе получиться, что для каждого оклада может быть только одна позиция. Также в таблице Оклад не нужен внешний ключ на Проект. Если же ваша логика состоит в том, чтобы оклад сделать зависимым от проекта и позиции, тогда свой собственный первичный ключ не нужен и первичным ключом должны быть поля внешние ключи Позиции + Проект, и в этом случае в таблице Позиция действительно не нужен внешний ключ на Оклад. - *Да, моя логика состоит в том, что оклад зависим от проекта и позиции сотрудника, первичным ключом таблицы Оклад будут поля внешние ключи "Позиция сотрудника" + "Проекты".*
* По поводу того, что нет в легенде Руководителей, тогда зачем вы изначально его добавляли?) К тому же легенда не запрещает вводить новые сущности, которые в целом соответствует логики легенды, суть в том, чтобы ваша база данных покрывала все сущности, которые есть в легенде. - *Я подумал, что это логично и добавил поле Руководитель, тем самым усложнив себе решение задания)))*




Предыдущие правки от преподавателя:

*Я добавил ещё одну таблицу под названием "Позиция сотрудника" - эта таблица является промежуточной таблицей (если я правильно понимаю, о чём говорю/пишу).
Правки, которые отметил преподаватель, я постарался исправить.*

* Внешний ключ на Тип подразделения должен храниться в Структурном подразделении, а не в Сотрудниках, так как это характеристика подразделения. - *Я переделал. Теперь "Тип подразделения, внешний ключ" находится в таблице "Структурное подразделение"*
* Не очень поняла, зачем в таблице оклад внешние ключи, они создают избыточность данных. Чтобы завязываться на логику, что оклад зависит от других параметров, то это надо реализовывать иначе, логика куда более сложная. Поэтому рекомендую просто оставить внешний ключ в Сотрудника, а из Оклада внешние ключи убрать. - *Я переделал. Оклад, согласно файлу [файл в формате Excel](https://github.com/netology-code/sdb-homeworks/blob/main/resources/hw-12-1.xlsx), зависит не только от должности сотрудника (а также его структурного подразделения и типа подразделения), но зависит и от проекта, на который назначен сотрудник. Поэтому внешние ключи в таблице оклад будут присутствовать следующие: Позиция сотрудника, внешний ключ, и Проект на который назначен, внешний ключ.*
* В таблице адрес Филиала не надо хранить на прмямую информацию о руководители, это не соответствует нормализации данных, вы можете просто хранить внешний ключ на конкретного сотрудника, а в таблице сделать галку руководитель - *Согласно легенде, которая изложена ниже, там нет столбца "руководитель", получается я его придумал сам. Поэтому, переосмыслив задание, я бы эти поля убрал, я их пометил комментарием курсивным шрифтом.*

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
- Фамилия сотрудника, varchar,
- Имя сотрудника, varchar,
- Отчество сотрудника, varchar,
- Дата найма, date,
- Пол, check,
- Позиция сотрудника, внешний ключ, integer,
- Адрес филиала, внешний ключ, integer,
- Является ли руководителем филиала?, boolean, *Я бы это поле убрал, так как его нет в легенде.*
- Проект на который назначен, внешний ключ, integer )

Позиция сотрудника (
- идентификатор, первичный ключ, serial,
- Должность, внешний ключ, integer
- Структурное подразделение, внешний ключ, integer )

Оклад (
- идентификатор, первичный ключ, serial, составной из внешних ключей: Поцизия сотрудника, внешний ключ, integer + Проект на который назначен, внешний ключ, integer,
- Оклад, numeric )

Должности (
- идентификатор, первичный ключ, serial,
- Наименование должности, varchar )

Структурное подразделение (
- идентификатор, первичный ключ, serial,
- Наименование структурного подразделения, text,
- Тип подразделения, внешний ключ, integer )

Тип подразделения (
- идентификатор, первичный ключ, serial,
- Тип подразделения, varchar )

Адрес филиала (
- идентификатор, первичный ключ, serial,
- Наименование филиала, text,
- Почтовый адрес, text,
- Контактный номер телефона филиала, char(11),
- Руководитель филиала - идентификатор Сотрудника, внешний ключ, integer *Я бы это поле убрал, так как его нет в легенде.* )

Проекты (
- идентификатор, первичный ключ, serial,
- Наименование проекта, text,
- Дата начала/создания проекта, date, 
- Дата окончания проекта, date,
- Структурное подразделение, внешний ключ, integer )


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.


### Задание 2*

Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.
