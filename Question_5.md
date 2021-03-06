(i)
Query:
```sql
SELECT SUM(salary) 
FROM employee
```

Response:
30000.3

sql> SELECT SUM(salary) from employee
[2020-02-28 17:11:29] 1 row retrieved starting from 1 in 65 ms (execution: 11 ms, fetching: 54 ms)

Description:
This query returns one row with one value: 30000.3 (see i in q5_images). This value represents the sum of all employees' salaries.

This query could be used by our company to determine yearly expenses from employees' wages for accounting purposes.

(ii)
Query:
```sql
SELECT registration_num, MAX(milage) 
FROM car 
GROUP BY name
```
Response:
Intermediate SUV	10000
Intermediate Car	2000
Economy Car	1000
Standard Car	2000
Full Size Car	5000
Compact Car	2000
Mini Van	2000

sql> SELECT name, MAX(milage)
     FROM car
     GROUP BY name
[2020-02-28 21:25:27] 7 rows retrieved starting from 1 in 52 ms (execution: 28 ms, fetching: 24 ms)

Description:
This query returns the highest mileage of cars grouped by their car classes.

This query could be used by our company to determine the cars that may need certain services, and cars that are getting to a point for which their expenses will likely exceed their profitability. It makes sense to group these by car class because different car classes may have different maximum mileages. For example, for an electric car, the mileage at which it would need to be scrapped is likely quite different from a hybrid or a gasoline car.

(iii)
Query:
```sql
SELECT registration_num
FROM car
WHERE car.name IN (SELECT name
                        FROM carclass
                        WHERE daily_price < 30)
```
Response:
7

sql> SELECT registration_num
     FROM car
     WHERE car.name IN (SELECT name
                             FROM carclass
                             WHERE daily_price < 30)
[2020-02-28 21:29:57] 1 row retrieved starting from 1 in 38 ms (execution: 23 ms, fetching: 15 ms)

Description:
This query could be used when customers wish to rent and price is more important to them than storage space.

(iv)
Query:
```sql
SELECT COUNT(DISTINCT email)
FROM rental
```
Response:
5

sql> SELECT COUNT(DISTINCT email)
     FROM rental
[2020-02-28 21:15:44] 1 row retrieved starting from 1 in 34 ms (execution: 21 ms, fetching: 13 ms)

Description: This could be used for our company to determine how many unique customers there have been.

(v)
Query:
```sql
SELECT COUNT(rental.rental_id)
FROM rental, sells
WHERE dropedoffat > '2020-02-28' AND pickedupat < '2020-03-01'
AND sells.rental_id=rental.rental_id
GROUP BY employee_id;

```
Response:
1

sql> SELECT COUNT(rental.rental_id)
     FROM rental, sells
     WHERE dropedoffat > '2020-02-28' AND pickedupat < '2020-03-01'
     AND sells.rental_id=rental.rental_id
     GROUP BY employee_id
[2020-02-28 21:59:51] 1 row retrieved starting from 1 in 72 ms (execution: 31 ms, fetching: 41 ms)

Description: This query can be used to see the number of sales for each employee to track their performance from time x to time y.
