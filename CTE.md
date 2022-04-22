# COMMON TABLE EXPRESSIONS

## Finding the AVERAGE AMOUNT PAID by the TOP 5 CUSTOMERS of the TOP 10 CITIES

```
WITH          cte_total_paid (customer_id, 
                              first_name, 
                              last_name, 
                              country, 
                              city, 
                              total_amount_paid) AS                             

(SELECT         A.customer_id, 
                B.first_name, 
                B.last_name, 
                E.country, 
                D.city,
	        SUM(amount) AS total_amount_paid
FROM            payment A
INNER JOIN      customer B ON A.customer_id = B.customer_id
INNER JOIN      address C ON B.address_id = C.address_id
INNER JOIN      city D ON C.city_id = D.city_id
INNER JOIN      country E ON D.country_id = E.country_id 
WHERE           D.city IN ('Aurora', 
                           'Tokat',
                           'Tarsus',
                           'Atlixco', 
                           'Emeishan',
                           'Pontianak',
                           'Shimoga',
                           'Aparecida de Goinia',
                           'Zalantun',
                           'Taguig')
GROUP BY        A.customer_id, 
                B.first_name, 
                B.last_name, 
                E.country, 
                D.city
ORDER BY        total_amount_paid DESC
LIMIT           5) 

SELECT AVG      (total_amount_paid) AS average_amount_paid
FROM            cte_total_paid
```

##### _Query Result_:
> ![Screenshot 2022-04-22 at 22 29 48](https://user-images.githubusercontent.com/104154067/164798414-d5fbf821-5481-481e-92cb-ef648eeac1bd.png)

##### _Data re-used from Joins.md_:
> ![SQL_JOIN_top5cust_top10countries](https://user-images.githubusercontent.com/104154067/164798520-5a08c95f-285d-46d1-ab43-11c6cf190c62.png)


