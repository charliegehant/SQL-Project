# FILTERING
## Various FILTERING queries

##### -> _Film title contains the word Uptown in any position_
```
SELECT  film_id, 
        title, 
        description
FROM    film
WHERE   title LIKE '%Uptown%'
```

##### -> _Rental duration is between 3 and 7 days (where 3 and 7 aren’t inclusive)_
```
SELECT  film_id, 
        title, 
        description
FROM    film
WHERE   rental_duration > 3 
AND     rental_duration < 7
```

