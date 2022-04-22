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


## COUNTING ALL CUSTOMERS by COUNTRY & EXTRACTING TOP CUSTOMERS from TOP 10 CITIES

´´´
WITH 		cte_step1_q2_t9 (customer_id, 
				 first_name, 
				 last_name, 
				 city, 
				 country, 
				 total_amount_paid) AS

(SELECT 	customer.customer_id, 
		customer.first_name, 
		customer.last_name, 
		city.city, 
		country.country, 
		SUM(payment.amount) AS total_amount_paid
FROM 		payment
INNER JOIN 	customer ON payment.customer_id = customer.customer_id
INNER JOIN 	address ON customer.address_id = address.address_id
INNER JOIN 	city ON address.city_id = city.city_id
INNER JOIN 	country ON city.country_id = country.country_id 
WHERE 		city.city IN ('Aurora', 
			      'Tokat',
			      'Tarsus',
			      'Atlixco', 
			      'Emeishan',
			      'Pontianak',
			      'Shimoga',
			      'Aparecida de Goinia',
			      'Zalantun',
			      'Taguig')
GROUP BY 	customer.customer_id, 
		customer.first_name, 
		customer.last_name, 
		city.city, 
		country.country
ORDER BY 	total_amount_paid DESC
LIMIT 5) 

SELECT 		country.country,
	       	COUNT(DISTINCT customer.customer_id) AS all_customer_count,
	       	COUNT(DISTINCT cte_step1_q2_t9.customer_id) AS top_customer_count
FROM 		customer 
INNER JOIN 	address ON customer.address_id = address.address_id
INNER JOIN 	city ON address.city_id = city.city_id
INNER JOIN 	country ON city.country_id = country.country_id
LEFT JOIN 	cte_step1_q2_t9 ON country.country = cte_step1_q2_t9.country
GROUP BY 	country.country
ORDER BY 	top_customer_count DESC
´´´


##### _Query Result_:
###### _(screenshot of 11 out of 108 rows)_
