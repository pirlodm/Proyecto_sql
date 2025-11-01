## 📘 EJERCICIO 1. Crea el esquema de la BBDD.  
--Se adjunta el fichero `diagrama_peliculasSQL.jpg`, que contiene el diagrama de la base de datos `peliculasSQL`.  

## 📘 EJERCICIO 2. Muestra los nombres de todas las películas con una clasificación por edades de ‘Rʼ.  

```sql
SELECT f.title AS Nombre_Pelicula
FROM film f
WHERE f.rating = 'R';
```

## 📘 EJERCICIO 3. Encuentra los nombres de los actores que tengan un “actor_idˮ entre 30 y 40.

```sql
select 
	a.actor_id ,
	concat(a.first_name ,' ',a.last_name ) as nombre_actor
from actor a 
	where a.actor_id between 30 and 40;
```

## 📘 EJERCICIO 4. Obtén las películas cuyo idioma coincide con el idioma original.

```sql
SELECT f.title 
FROM film f 
WHERE f.original_language_id = f.language_id 
```

## 📘 EJERCICIO 5. Ordena las películas por duración de forma ascendente.

```sql
SELECT 
	f.title as titulo_pelicula,
	f.length as Duracion
FROM film f 
order by duracion asc;
```

## 📘 EJERCICIO 6. Encuentra el nombre y apellido de los actores que tengan ‘Allenʼ en su apellido

```sql
SELECT 
	a.first_name as nombre, 
	a.last_name as apellido
FROM actor a 
WHERE last_name LIKE '%Allen%';
```

## 📘 EJERCICIO 7. Encuentra la cantidad total de películas en cada clasificación de la tabla “filmˮ y muestra la clasificación junto con el recuento.

```sql
select 
	f.rating as clasificaion,
	count(f.film_id ) as cantidad
from film f 
group by f.rating ;
```

## 📘 EJERCICIO 8. Encuentra el título de todas las películas que son ‘PG13ʼ o tienen una duración mayor a 3 horas en la tabla film

```sql
select 
	f.title as titulo_pelicula,
	f.length as duracion
from film f 
where f.rating  = 'PG-13'
and f.length > 180;
```

## 📘 EJERCICIO 9. Encuentra la variabilidad de lo que costaría reemplazar las películas.

```sql
select 
	round(AVG(f.replacement_cost ),2) as media,
	round(variance(f.replacement_cost ),2) as varianza,
	round(stddev(f.replacement_cost ),2) as desviacion_estandar
from film f ;
```

## 📘 EJERCICIO 10. Encuentra la mayor y menor duración de una película de nuestra BBDD.

```sql
select 
	max(f.length ) as mayor_duracion,
	min	(f.length ) as menor_duracion
from film f ;
```
## 📘 EJERCICIO 11. Encuentra lo que costó el antepenúltimo alquiler ordenado por día.

```sql
select 
	r.customer_id  as precio, 
	r.rental_date as dia_alquiler
from rental r 
order by r.rental_date desc
limit 1 
offset 2;
```

## 📘 EJERCICIO 12. Encuentra el título de las películas en la tabla “filmˮ que no sean ni ‘NC-17ʼ ni ‘Gʼ en cuanto a su clasificación.

```sql
select
	f.title as nombre_pelicula,
	f.rating as clasificacion
from film f
where f.rating not in ('NC-17','G');
```

## 📘 EJERCICIO 13.Encuentra el promedio de duración de las películas para cada clasificación de la tabla film y muestra la clasificación junto con el promedio de duración.

```sql
select 
	f.rating as clasificacion,
	round(avg(f.length ),2) as promedio
from film f 
group by f.rating ;
```
## 📘 EJERCICIO 14. Encuentra el título de todas las películas que tengan una duración mayor a 180 minutos.

```sql
select 
	f.title as titulo_pelicula,
	f.length as duracion
from film f 
where f.length > 180;
```

## 📘 EJERCICIO 15. ¿Cuánto dinero ha generado en total la empresa?.

```sql
select 
	SUM(p.amount ) as total_generado
from payment p ;
```

## 📘 EJERCICIO 16. Muestra los 10 clientes con mayor valor de id.

```sql
select 
	c.customer_id ,
	concat(c.first_name , ' ',c.last_name ) as nombre_cliente
from customer c 
order by c.customer_id desc
limit 10;
```
## 📘 EJERCICIO 17. Encuentra el nombre y apellido de los actores que aparecen en la película con título ‘Egg Igbyʼ.

```sql
select 
	f.title as Titulo_pelicula,
	concat(a.first_name ,' ',a.last_name ) as Nombre_Actor
from film f 
inner join film_actor fa 
	on f.film_id = fa.film_id
inner join actor a 
	on fa.actor_id = a.actor_id
where f.title = 'Egg Igby';
```
### * para comprobar si la falta de resultados era correcta , puse otra sentencia:
	
```sql
SELECT title 
FROM film
WHERE title LIKE '%Egg Igby%';
```

## 📘 EJERCICIO 18. Selecciona todos los nombres de las películas únicos.

```sql
select distinct title
from film f 
order by f.title ;
```
## 📘 EJERCICIO 19. Encuentra el título de las películas que son comedias y tienen una duración mayor a 180 minutos en la tabla “filmˮ.

```sql
select 
	f.title as titulo,
	f.length as Duracion,
	c."name" as categoria 
from film f 
inner join film_category fc 
	on f.film_id = fc.film_id
inner join category c
	on fc.category_id = c.category_id 
where c."name" = 'Comedy'
	and f.length > 180;
```

## 📘 EJERCICIO 20. Encuentra las categorías de películas que tienen un promedio de duración superior a 110 minutos y muestra el nombre de la categoría junto con el promedio de duración.

```sql
select
	c."name" as categoria,
	round(avg (f.length )) as Promedio_Duracion
from film f 
inner join film_category fc  
	on f.film_id = fc.film_id
inner join category c 
	on fc.category_id = c.category_id
group by c."name" 
having avg(f.length ) > 110;
```

## 📘 EJERCICIO 21. ¿Cuál es la media de duración del alquiler de las películas?.

```sql
select 
	AVG(f.rental_duration ) as Media_Duracion
from film f ;
```

## 📘 EJERCICIO 22. Crea una columna con el nombre y apellidos de todos los actores y actrices.

```sql
select
	concat(a.first_name, ' ', a.last_name)  as Nombre_Completo
from actor a 
order by nombre_completo ;
```

## 📘 EJERCICIO 23. Números de alquiler por día, ordenados por cantidad de alquiler de forma descendente.



















