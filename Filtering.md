# FILTERING
## Various FILTERING queries using WHERE statement

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
##### -> _Film rating is either PG or G_
```
SELECT  film_id, 
        title, 
        description
FROM    film
WHERE   rating = 'PG' 
OR      rating = 'G'
```
##### -> _Descriptive Statistics with Filtering_
```
SELECT          COUNT(film_id)          AS count_of_movies,
                AVG(rental_rate)        AS average_movie_rental_rate,
                MIN(rental_duration)    AS minimum_rental_duration,
                MAX(rental_duration)    AS maximum_rental_duration
FROM            film
WHERE           rating = 'PG' 
OR              rating = 'G'
GROUP BY        rating
```

![Screenshot 2022-04-22 at 22 59 23](https://user-images.githubusercontent.com/104154067/164801368-3a19e4bc-dee9-483d-9806-d2769c16dabf.png)

