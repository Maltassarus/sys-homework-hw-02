# Домашнее задание к занятию "`SQL. Часть 2`" - `Борзенко Андрея`

### Задание 1

1.1.
```
SELECT
    CONCAT(s.last_name, ' ', s.first_name) AS 'Фамилия и имя сотрудника',
    c.city AS 'Город нахождения магазина',
    COUNT(cust.customer_id) AS 'Количество покупателей'
FROM store st
JOIN staff s ON st.manager_staff_id = s.staff_id
JOIN address a ON st.address_id = a.address_id
JOIN city c ON a.city_id = c.city_id
JOIN customer cust ON st.store_id = cust.store_id
GROUP BY st.store_id, s.last_name, s.first_name, c.city
HAVING COUNT(cust.customer_id) > 300;
```
```
Фамилия и имя сотрудника        Город нахождения магазина       Количество покуп
ателей
Hillyer Mike    Lethbridge      326
```

1.2.
```
SELECT COUNT(*) AS 'Количество фильмов'
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```
```
Количество фильмов
489
```

1.3.
```
SELECT
    DATE_FORMAT(payment_date, '%Y-%m') AS 'Месяц',
    SUM(amount) AS 'Общая сумма платежей',
    COUNT(rental_id) AS 'Количество аренд'
FROM payment
GROUP BY DATE_FORMAT(payment_date, '%Y-%m')
ORDER BY SUM(amount) DESC
LIMIT 1;
```

```
Месяц   Общая сумма платежей    Количество аренд
2005-07 28368.91        6709
```