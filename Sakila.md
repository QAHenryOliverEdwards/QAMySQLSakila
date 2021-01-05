# Sakila Challenge

1. List all actors.

SELECT first_name, last_name FROM actor;

2. Find the surname of the actor with the forename 'John'.

SELECT last_name FROM actor WHERE first_name = 'John';

3. Find all actors with surname 'Neeson'.

SELECT * FROM actor WHERE last_name = 'Neeson';

4. Find all actors with ID numbers divisible by 10.

SELECT * FROM actor WHERE actor_id % 10 = 0;

5. What is the description of the movie with an ID of 100?

SELECT description FROM film WHERE film_id = 100;

6. Find every R-rated movie.

SELECT * FROM film WHERE rating = 'R';

7. Find every non-R-rated movie.

SELECT * FROM film WHERE rating != 'R';

8. Find the ten shortest movies.

SELECT * FROM film ORDER BY length limit 10;

9. Find the movies with the longest runtime, without using LIMIT.

SELECT * FROM film ORDER BY length DESC;

10. Find all movies that have deleted scenes.

SELECT * FROM film WHERE special_features = 'Deleted Scenes';

11. Using HAVING, reverse-alphabetically list the last names that are not repeated.

SELECT DISTINCT last_name FROM actor ORDER BY last_name DESC;

12. Using HAVING, list the last names that appear more than once, from highest to lowest frequency.

SELECT COUNT(last_name) FROM actor GROUP BY last_name ORDER BY COUNT(last_name) DESC;

13. Which actor has appeared in the most films?

SELECT film_actor.actor_id, actor_info.first_name, actor_info.last_name, COUNT(film_actor.actor_id) AS films
FROM film_actor
JOIN actor_info ON film_actor.actor_id=actor_info.actor_id
GROUP BY film_actor.actor_id

14. When is 'Academy Dinosaur' due?

SELECT release_year 
FROM film
WHERE title =  'Academy Dinosaur';

15. What is the average runtime of all films?

SELECT AVG(length)
FROM film

16. List the average runtime for every film category.

SELECT AVG(film.length), category.category_id
FROM category
JOIN film_category ON film_category.category_id = category.category_id
JOIN film ON film.film_id = film_category.film_id
GROUP BY category.category_id
ORDER BY AVG(film.length) DESC;

17. List all movies featuring a robot.

SELECT film.title
FROM film_text 
JOIN film ON film.film_id=film_text.film_id
WHERE film_text.description LIKE '%robot%';

18. How many movies were released in 2010?

SELECT title 
FROM film
WHERE release_year = 2010;

19. Find the titles of all the horror movies.

SELECT title
FROM film
JOIN film_category ON film_category.film_id = film.film_id
JOIN category ON category.category_id = film_category.category_id
WHERE category.name='Horror'
GROUP BY title

20. List the full name of the staff member with the ID of 2.

SELECT first_name, last_name
FROM staff
WHERE staff_id = 2

21. List all the movies that Fred Costner has appeared in.

SELECT film.title
FROM film
JOIN film_actor ON film_actor.actor_id = film.film_id
JOIN actor ON actor.actor_id = film_actor.actor_id
AND actor.last_name='Costner'

22. How many distinct countries are there?

SELECT DISTINCT COUNT(country) FROM country;

23. List the name of every language in reverse-alphabetical order.

SELECT name FROM language ORDER BY name DESC;

24. List the full names of every actor whose surname ends with '-son' in alphabetical order by their forename.

SELECT first_name, last_name
FROM actor
WHERE last_name LIKE '%son%' 
ORDER BY first_name ASC;

25. Which category contains the most films?

SELECT COUNT(film_id), category_id
FROM film_category
GROUP BY category_id
ORDER BY COUNT(film_id) DESC;