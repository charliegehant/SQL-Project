# SUBQUERIES
## Counting ALL CUSTOMERS and TOP CUSTOMERS

```
SELECT      country.country,
	    COUNT(DISTINCT customer.customer_id) AS all_customer_count,
	    COUNT(DISTINCT top_5_customers.customer_id) AS top_customer_count
FROM        customer 
INNER JOIN  address ON customer.address_id = address.address_id
INNER JOIN  city ON address.city_id = city.city_id
INNER JOIN  country ON city.country_id = country.country_id

LEFT JOIN   (SELECT     customer.customer_id, 
                        customer.first_name, 
                        customer.last_name, 
                        city.city, country.country, 
                        SUM(payment.amount) AS total_amount_paid
            FROM        payment
            INNER JOIN  customer ON payment.customer_id = customer.customer_id
            INNER JOIN  address ON customer.address_id = address.address_id
            INNER JOIN  city ON address.city_id = city.city_id
            INNER JOIN  country ON city.country_id = country.country_id 
            WHERE       city.city IN ('Aurora', 
                                      'Tokat',
                                      'Tarsus',
                                      'Atlixco', 
                                      'Emeishan',
                                      'Pontianak',
                                      'Shimoga',
                                      'Aparecida de Goinia',
                                      'Zalantun',
                                      'Taguig')
            GROUP BY    customer.customer_id, customer.first_name, customer.last_name, city.city, country.country
            ORDER BY    total_amount_paid DESC
            LIMIT 5) AS top_5_customers ON country.country = top_5_customers.country

GROUP BY    country.country
ORDER BY    top_customer_count DESC
```

##### _Query Result (screenshot of 11 out of 108 rows)_:
![Screenshot 2022-04-22 at 22 43 17](https://user-images.githubusercontent.com/104154067/164802701-37d16fed-3d18-495b-bb51-ba80666e6b40.png)
