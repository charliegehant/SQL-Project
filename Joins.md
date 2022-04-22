
# JOINING TABLES 
## To find the TOP 10 COUNTRIES

```
SELECT 		D.country,
		COUNT(customer_id) AS count_of_customers
FROM 		customer A
INNER JOIN 	address B ON A.address_id = B.address_id
INNER JOIN 	city C ON B.city_id = C.city_id
INNER JOIN 	country D ON C.country_id = D.country_id 
GROUP BY 	country
ORDER BY 	count_of_customers DESC
LIMIT 		10
```

![SQL_JOIN_top10countries](https://user-images.githubusercontent.com/104154067/164775588-bfc39261-ae36-4066-8236-82aa753a2ea4.png)


## To find the TOP 5 CUSTOMERS of the TOP 10 CITIES

```
SELECT 		A.customer_id, 
		B.first_name, 
		B.last_name, 
		E.country, 
		D.city,
		SUM(amount) AS total_paid
FROM 		payment A
INNER JOIN 	customer B ON A.customer_id = B.customer_id
INNER JOIN 	address C ON B.address_id = C.address_id
INNER JOIN 	city D ON C.city_id = D.city_id
INNER JOIN 	country E ON D.country_id = E.country_id 
WHERE 		E.country IN ('India', 'China', 'United States', 'Japan', 'Mexico', 'Brazil', 'Russian Federation', 'Philippines', 'Turkey', 'Indonesia')
AND 		D.city IN ('Aurora', 'Tokat', 'Tarsus', 'Atlixco', 'Emeishan', 'Pontianak', 'Shimoga', 'Aparecida de Goinia', 'Zalantun', 'Taguig')
GROUP BY 	A.customer_id, 
		B.first_name, 
		B.last_name, 
		E.country, 
		D.city
ORDER BY 	total_paid DESC
LIMIT 		5
```

![SQL_JOIN_top5cust_top10countries](https://user-images.githubusercontent.com/104154067/164775413-8394a992-0662-4b8d-a5b1-9a4df2910935.png)

