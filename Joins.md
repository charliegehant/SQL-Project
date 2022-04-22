## heloo

SELECT A.customer_id,
	B.first_name,
	B.last_name,
	E.country,
	D.city,
	SUM(amount) AS total_paid
FROM payment A
INNER JOIN customer B ON A.customer_id = B.customer_id
INNER JOIN address C ON B.address_id = C.address_id
INNER JOIN city D ON C.city_id = D.city_id
INNER JOIN country E ON D.country_id = E.country_id 
WHERE city = 'Aurora'
	OR city = 'Tokat'
	OR city = 'Tarsus'
	OR city = 'Atlixco'
	OR city = 'Emeishan'
	OR city = 'Pontianak'
	OR city = 'Shimoga'
	OR city = 'Aparecida de Goinia'
	OR city = 'Zalantun'
	OR city = 'Taguig'
GROUP BY A.customer_id,
	B.first_name,
	B.last_name,
	E.country,
	D.city
ORDER BY total_paid DESC
LIMIT 5
