# Домашнее задание к занятию "Работа с данными (DDL/DML)" - `Александра Бужор`

### Задание 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.7. По ссылке [https://downloads.mysql.com/docs/sakila-db.zip](https://github.com/AngryCFO/SDB-DDL-DML/blob/36bd5afedbefc5d08b0c99ebd2125539e8d879b1/sakila-db.zip) скачайте дамп базы данных.

1.8. Восстановите дамп в базу данных.

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

### Решение:

![image](https://github.com/user-attachments/assets/9f611fa3-6557-446d-8c38-879ba19d3b00)

![image](https://github.com/user-attachments/assets/b7fc24ca-8876-415b-8c46-cd1a74963ede)

![image](https://github.com/user-attachments/assets/c95e43ae-d945-4618-9f2e-b6c1cfcd5b56)

![image](https://github.com/user-attachments/assets/ecdd0511-896a-4b55-bf48-2b32697e7910)

![image](https://github.com/user-attachments/assets/3ad70bf1-9832-4e61-bf87-ef1763a3f707)

![image](https://github.com/user-attachments/assets/4cc83570-6c8e-4b3a-8eba-ebf92d261b8f)

![image](https://github.com/user-attachments/assets/4ce35fd0-a702-4555-b341-49f80aefb51b)

---

### Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

### Решение:

```sql
SELECT 
    TABLE_NAME AS 'Название таблицы', 
    COLUMN_NAME AS 'Название первичного ключа'
FROM 
    information_schema.KEY_COLUMN_USAGE
WHERE 
    TABLE_SCHEMA = 'sakila' AND
    CONSTRAINT_NAME = 'PRIMARY';
```

```
Название таблицы|Название первичного ключа|
----------------+-------------------------+
actor           |actor_id                 |
address         |address_id               |
category        |category_id              |
city            |city_id                  |
country         |country_id               |
customer        |customer_id              |
film            |film_id                  |
film_actor      |actor_id                 |
film_actor      |film_id                  |
film_category   |film_id                  |
film_category   |category_id              |
film_text       |film_id                  |
inventory       |inventory_id             |
language        |language_id              |
payment         |payment_id               |
rental          |rental_id                |
staff           |staff_id                 |
store           |store_id                 |
```


---

### Задание 3

3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

### Решение:

```
SHOW GRANTS FOR 'sys_temp'@'%';
```
```
REVOKE ALL PRIVILEGES ON sakila.* FROM 'sys_temp'@'%';
```
```
GRANT SELECT ON sakila.* TO 'sys_temp'@'%';
```
```
SHOW GRANTS FOR 'sys_temp'@'%';
```


Console log:
```
> SHOW GRANTS FOR 'sys_temp'@'%'

Grants for sys_temp@%                               |
----------------------------------------------------+
GRANT USAGE ON *.* TO `sys_temp`@`%`                |
GRANT ALL PRIVILEGES ON `sakila`.* TO `sys_temp`@`%`|

2 row(s) fetched.

> REVOKE ALL PRIVILEGES ON sakila.* FROM 'sys_temp'@'%'

0 row(s) modified.

> GRANT SELECT ON sakila.* TO 'sys_temp'@'%'

0 row(s) modified.


> SHOW GRANTS FOR 'sys_temp'@'%'

Grants for sys_temp@%                       |
--------------------------------------------+
GRANT USAGE ON *.* TO `sys_temp`@`%`        |
GRANT SELECT ON `sakila`.* TO `sys_temp`@`%`|

2 row(s) fetched.
```
