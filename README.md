# Домашнее задание к занятию "`SQL. Часть 1`" - `Тен Денис`


Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Решение Задание 1

```sql
USE sakila;
SELECT DISTINCT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```
![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/af5bf82a-e4f5-41ce-837f-114399289a2c)

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

### Решение Задание 2

```sql
USE sakila;
SELECT * FROM payment WHERE payment_date >= '2005-06-15' AND payment_date <= '2005-06-18' AND amount > 10.00;
```

![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/710aa4fb-7e5c-4b33-a287-f2447af16bd4)



### Задание 3

Получите последние пять аренд фильмов.

### Решение Задание 3

```sql
USE sakila;
SELECT * FROM rental ORDER BY rental_id desc LIMIT 5;
```
![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/961eb6ff-9d76-42a6-84ec-6e303fef5cd9)



### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

### Решение Задание 4

```sql
USE sakila;
SELECT 
  REPLACE(LOWER(first_name), 'll', 'pp') AS first_name,
  REPLACE(LOWER(last_name), 'll', 'pp') AS last_name
FROM customer
WHERE active = 1
  AND (first_name = 'Kelly' OR first_name = 'Willie');
```
![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/2dbd58f3-94a2-46f3-a8f8-0e7ed458e347)



## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

### Решение Задание 5*

```sql
USE sakila;
SELECT 
  SUBSTRING_INDEX(email, '@', 1) AS email_username,
  SUBSTRING_INDEX(email, '@', -1) AS email_domain
FROM customer;
```
![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/1b96fafa-2b59-4037-9c42-16adbeb64609)


### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

### Решение Задание 6*

```sql
USE sakila;
SELECT 
  CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 2))) AS email_username,
  CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', -1), 2))) AS email_domain
FROM customer;
```
![image](https://github.com/killakazzak/12-03-sdb-hw/assets/32342205/e831341d-46eb-440b-baeb-84960cbd0bb9)



