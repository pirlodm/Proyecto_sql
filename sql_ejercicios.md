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

```sql
select 
	DATE (r.rental_date) as Fecha_Alquiler,
	count(r.rental_id ) as Cantidad_alquiler
from rental r 
group by DATE (r.rental_date) 
order by cantidad_alquiler DESC;
```

## 📘 EJERCICIO 24. Encuentra las películas con una duración superior al promedio.

```sql
select 
	f.title as titulo_pelicula,
	f.length as duracion
from film f 
where f.length >(
	select avg(fi.length) 
	from film fi)
order by f.length;
```

## 📘 EJERCICIO 25. Averigua el número de alquileres registrados por mes.

```sql
select 
	date_trunc('month',r.rental_date ) as mes,
	count(r.rental_id) as Numero_Alquileres
from rental r 
group by date_trunc('month',r.rental_date );
```

### * Como vi que no podia ordenarlo por mes , busque otra manera de hacerlo.

```sql
select 
	date_trunc('year',r.rental_date ) as Año,
	date_trunc('month',r.rental_date ) as Mes,
	count(r.rental_id) as Numero_Alquileres
from rental r 
group by Año,Mes
order by Año,Mes;
```

## 📘 EJERCICIO 26. Encuentra el promedio, la desviación estándar y varianza del total pagado.

```sql
select 
	round(AVG(p.amount),2) as Media,
	round(STDDEV(p.amount),2) as Desviacion_estandar,
	round(VARIANCE(p.amount),2)	as varianza
from payment p ;
```

## 📘 EJERCICIO 27. ¿Qué películas se alquilan por encima del precio medio?.

```sql
SELECT 
    f.title as Titulo_Pelicula,
    f.rental_rate as Precio_alquiler
FROM film f
WHERE f.rental_rate > (
    SELECT AVG(rental_rate)
    FROM film
);
```

## 📘 EJERCICIO 28. Muestra el id de los actores que hayan participado en más de 40 películas.

```sql
select 
	fa.actor_id,
	count(fa.film_id) as Numero_peliculas
from film_actor fa
group by actor_id
having count(fa.film_id) > 40;
```


### * si ademas queremos añadirle los nombres al ejercicio.

```sql
select 
	a.actor_id,
	concat(a.first_name ,' ' ,a.last_name ) as Nombre_Actor,
	count(fa.film_id) as Numero_peliculas
from film_actor fa
inner join actor a 
	on fa.actor_id = a.actor_id 
group by a.actor_id, a.first_name, a.last_name
having count(fa.film_id) > 40;
```

## 📘 EJERCICIO 29. Obtener todas las películas y, si están disponibles en el inventario, mostrar la cantidad disponible.

```sql
select 
	f.film_id,
	f.title ,
	count(i.inventory_id )
from film f 
left join inventory i 
	on f.film_id = i.film_id
group by f.film_id , f.title ;
```

## 📘 EJERCICIO 30. Obtener los actores y el número de películas en las que ha actuado.

```sql
select 
	concat(a.first_name,' ',a.last_name  ) as NombreActor,
	count(fa.film_id ) as NumeroPeliculas
from actor a 
inner join film_actor fa 
	on a.actor_id = fa.actor_id
group by a.first_name , a.last_name 
order by numeropeliculas desc;
```

## 📘 EJERCICIO 31. Obtener todas las películas y mostrar los actores que han actuado en ellas, incluso si algunas películas no tienen actores asociados.

```sql
SELECT 
	f.film_id,
    f.title as Titulo_Pelicula,
    concat(a.first_name,' ',a.last_name) as Nombre_Actor
FROM film f
LEFT JOIN film_actor fa 
    ON f.film_id = fa.film_id
LEFT JOIN actor a 
    ON fa.actor_id = a.actor_id
ORDER BY f.title, a.last_name, a.first_name;
```

## 📘 EJERCICIO 32. Obtener todos los actores y mostrar las películas en las que han actuado, incluso si algunos actores no han actuado en ninguna película.

```sql
SELECT 
	a.actor_id,
	concat(a.first_name,' ',a.last_name) as NombreActor,
	f.title as Titulo_Pelicula
from actor a 
left join film_actor fa 
	on a.actor_id = fa.actor_id
left join film f 
	on fa.film_id = f.film_id;
```

## 📘 EJERCICIO 33. Obtener todas las películas que tenemos y todos los registros de alquiler.

```sql
select 
	f.film_id,
	f.title as Titutlo_Pelicula,
	r.rental_id,
	r.rental_date as Registro_Alquiler
from film f 
left join inventory i 
	on f.film_id = i.film_id
left join rental r 
	on i.inventory_id = r.inventory_id	;
```

## 📘 EJERCICIO 34.  Encuentra los 5 clientes que más dinero se hayan gastado con nosotros.

```sql
select 
	c.customer_id,
	concat(c.last_name,' ',c.first_name) as Nombre_Cliente,
	SUM(p.amount )as Total_Ventas
from  customer c
inner join rental r 
	on c.customer_id = r.customer_id
inner join payment p 
	on c.customer_id = p.customer_id
group by c.customer_id, c.first_name ,c.last_name
order by total_ventas desc
limit  5;
```

## 📘 EJERCICIO 35. Selecciona todos los actores cuyo primer nombre es 'Johnny'.

```sql
select
	a.first_name
from actor a
where a.first_name = 'Johnny';
```

### * No muestra ningun resultado , la causa es por que todos los nombres estan en mayusculas y nosotros bucamos el resultado en miniscula.


## 📘 EJERCICIO 36.Renombra la columna “first_nameˮ como Nombre y “last_nameˮ como Apellido.

```sql
select 
	a.first_name as Nombre,
	a.last_name as Apellido
from actor a ;
```

## 📘 EJERCICIO 37.  Encuentra el ID del actor más bajo y más alto en la tabla actor.

```sql
select 
	MIN(a.actor_id) as Minimo,
	MAX(a.actor_id) as maximo
from actor a;
```

## 📘 EJERCICIO 38. Cuenta cuántos actores hay en la tabla “actorˮ.

```sql
select 
	count(a.actor_id) as Total_actores
from actor a; 
```
## 📘 EJERCICIO 39. Selecciona todos los actores y ordénalos por apellido en orden ascendente.

```sql
select 
	a.first_name as Nombre,
	a.last_name as Apellido
from actor a 
order by apellido asc;
```

## 📘 EJERCICIO 40.  Selecciona las primeras 5 películas de la tabla “filmˮ.

```sql
select
	f.film_id,
	f.title as Titulo_Pelicula
from film f
limit 5;
```

## 📘 EJERCICIO 41.  Agrupa los actores por su nombre y cuenta cuántos actores tienen el mismo nombre. ¿Cuál es el nombre más repetido?.

```sql
select 
	a.first_name as Nombre,
	count(a.actor_id ) as cantidad
from actor a 
group by a.first_name
order by cantidad desc;
```

### * si solo queremos ver el mas repetido :
```sql
select 
	a.first_name as Nombre,
	count(a.actor_id ) as cantidad
from actor a 
group by a.first_name
order by cantidad desc
limit 1;
```

## 📘 EJERCICIO 42. Encuentra todos los alquileres y los nombres de los clientes que los realizaron.

```sql
select 
	r.rental_id ,
	concat(c.first_name ,' ',c.last_name ) as Nombre_Cliente
from rental r
inner join customer c 
	on r.customer_id = c.customer_id;
```

## 📘 EJERCICIO 43. Muestra todos los clientes y sus alquileres si existen, incluyendo aquellos que no tienen alquileres.

```sql
select 
	c.customer_id,
	concat(c.first_name ,' ',c.last_name ) as NombreCliente,
	r.rental_date ,
	r.rental_id 
from customer c
left join rental r 
	on c.customer_id = r.customer_id;
```

## 📘 EJERCICIO 44. Realiza un CROSS JOIN entre las tablas film y category. ¿Aporta valor esta consulta? ¿Por qué? Deja después de la consulta la contestación.

```sql
select *
from film f 
cross join category c ;
```

### * la consulta no aporta ningun valor practico ya que no aporta datos reales, lo mas logico hubiera sido usar un INNER JOIN.

## 📘 EJERCICIO 45. Encuentra los actores que han participado en películas de la categoría 'Action'.

### * al principio creia que de esta manera era correcto hasta que me di cuenta que se repetian.


```sql
select
	concat(a.first_name,' ',a.last_name) as Nombre_Actor,
	c."name" as categoria
from actor a 
inner join film_actor fa 
	on a.actor_id = fa.actor_id
inner join film f 
	on fa.film_id = f.film_id
inner join film_category fc 
	on f.film_id = fc.film_id
inner join category c
	on fc.category_id = c.category_id 
where c."name" = 'Action' ;
```
### * correcion del ejercicio, aplicando distinct.

```sql
select distinct
	concat(a.first_name,' ',a.last_name) as Nombre_Actor,
	c."name" as categoria
from actor a 
inner join film_actor fa 
	on a.actor_id = fa.actor_id
inner join film f 
	on fa.film_id = f.film_id
inner join film_category fc 
	on f.film_id = fc.film_id
inner join category c
	on fc.category_id = c.category_id 
where c."name" = 'Action' ;
```

## 📘 EJERCICIO 46. Encuentra todos los actores que no han participado en películas.

```sql
select 
	a.actor_id,
	concat(a.first_name,' ',a.last_name)	
from actor a 
left join film_actor fa 
on a.actor_id = fa.actor_id
where fa.film_id is null;
```

## 📘 EJERCICIO 47. Selecciona el nombre de los actores y la cantidad de películas en las que han participado.

```sql
select 
	a.actor_id ,
	concat(a.first_name ,' ',a.last_name ) as Nombre_Actor,
	count(fa.film_id ) as Cantidad_Peliculas
from actor a 
left join film_actor fa 
	on a.actor_id = fa.actor_id
group by a.actor_id , a.first_name ,a.last_name 
order by cantidad_peliculas  desc;
```

## 📘 EJERCICIO 48. Crea una vista llamada “actor_num_peliculasˮ que muestre los nombres de los actores y el número de películas en las que han participado.

```sql
create view Actor_Num_Peliculas as
select 
	a.actor_id ,
	concat(a.first_name ,' ',a.last_name ) as Nombre_Actor,
	count(fa.film_id ) as Cantidad_Peliculas
from actor a 
left join film_actor fa 
	on a.actor_id = fa.actor_id
group by a.actor_id , a.first_name ,a.last_name 
order by cantidad_peliculas  desc;
```

## 📘 EJERCICIO 49. Calcula el número total de alquileres realizados por cada cliente.

```sql
select 
	c.customer_id,
	concat(c.first_name,' ',c.last_name) as Nombre_cliente,
	count(Rental_id) as Numero_Alquileres
from customer c 
left join rental r 
	on c.customer_id = r.customer_id
group by c.customer_id, c.first_name, c.last_name 
order by numero_alquileres desc;
```

## 📘 EJERCICIO 50. Calcula la duración total de las películas en la categoría 'Action'.

```sql
select 
	c."name" as Categoria,
	sum(f.length) as Duracion_Total
from category c 
inner join film_category fc
	on c.category_id = fc.category_id
inner join film f 
	on fc.film_id = f.film_id 
where c."name" = 'Action'
group by c."name";
```

## 📘 EJERCICIO 51. Crea una tabla temporal llamada “cliente_rentas_temporalˮ para almacenar el total de alquileres por cliente.

```sql
create temporary table cliente_rentas_temporal as 
	select 
		c.customer_id ,
		concat(c.first_name, ' ', c.last_name ) as Nombre_Cliente,
		count(r.rental_id) as Total_Alquiler
	from customer c
	inner join rental r 
		on c.customer_id = r.customer_id
	group by c.customer_id, c.first_name ,c.last_name
	order by Total_Alquiler desc;
```

```sql
select *
from cliente_rentas_temporal;
```

## 📘 EJERCICIO 52. Crea una tabla temporal llamada “peliculas_alquiladasˮ que almacene las películas que han sido alquiladas al menos 10 veces.

```sql
create temporary table Peliculas_Alquiladas as
select 
	f.film_id ,
	f.title as Titulo_Pelicula,
	count(r.rental_id) as Cantidad_Alquiler
from film f 
inner join inventory i 
	on f.film_id = i.film_id
inner join rental r 
	on i.inventory_id = r.inventory_id
group by f.film_id , f.title
having count(r.rental_id) >= 10
order by cantidad_alquiler ;
```

```sql
select *
from Peliculas_Alquiladas ;
```

## 📘 EJERCICIO 53. Encuentra el título de las películas que han sido alquiladas por el cliente con el nombre ‘Tammy Sandersʼ y que aún no se han devuelto. Ordena los resultados alfabéticamente por título de película.

```sql
select 
	f.title 
from customer c
inner join rental r 
	on c.customer_id = r.customer_id
inner join inventory i
	on r.inventory_id = i.inventory_id
inner join film f 
	on i.film_id = f.film_id
where 
	c.first_name = 'Tammy'
	and c.last_name = 'Sanders'
group by title
order by f.title ;
```

### * Al ver que no me ofrecia ningun resultado , comprobe si existia ese cliente.


```sql
select 
	c.customer_id,
	c.first_name,
	c.last_name 
from customer c 
where 
	c.first_name = 'Tammy'
	and c.last_name  = 'Sanders';
```

## 📘 EJERCICIO 54.  Encuentra los nombres de los actores que han actuado en al menos una película que pertenece a la categoría ‘Sci-Fiʼ. Ordena los resultados alfabéticamente por apellido.

```sql
select distinct
	a.first_name as Nombre,
	a.last_name as Apellido,
	c."name" as categoria
from actor a 
inner join film_actor fa 
	on a.actor_id = fa.actor_id
inner join film f 
	on fa.film_id = f.film_id
inner join film_category fc
	on f.film_id = fc.film_id
inner join category c 
	on fc.category_id = c.category_id 
where c."name" = 'Sci-Fi'
group by a.first_name ,a.last_name,c."name"
order by a.last_name ;
```

## 📘 EJERCICIO 55. Encuentra el nombre y apellido de los actores que han actuado en películas que se alquilaron después de que la película ‘Spartacus Cheaperʼ se alquilara por primera vez. Ordena los resultados alfabéticamente por apellido.

```sql
select
	a.first_name as nombre,
	a.last_name as apellido
from actor a 
inner join film_actor fa 
	on a.actor_id = fa.actor_id
inner join film f 
	on fa.film_id = f.film_id
inner join inventory i 
	on f.film_id = i.film_id
inner join rental r 
	on i.inventory_id = r.inventory_id
where r.rental_date > (
		SELECT  MIN(r.rental_date ) 
		FROM film f
		inner join inventory i  
			on f.film_id = i.film_id
		inner join rental r 
			on i.inventory_id = r.inventory_id
		WHERE LOWER(f.title) LIKE LOWER('%spartacus%')
)
group by a.actor_id, a.first_name, a.last_name
order by apellido, nombre;
```

## 📘 EJERCICIO 56.  Encuentra el nombre y apellido de los actores que no han actuado en ninguna película de la categoría ‘Musicʼ.

```sql
SELECT a.first_name, a.last_name
FROM actor a
WHERE NOT EXISTS (
    SELECT 1
    FROM film_actor fa
    JOIN film f ON fa.film_id = f.film_id
    JOIN film_category fc ON f.film_id = fc.film_id
    JOIN category c ON fc.category_id = c.category_id
    WHERE fa.actor_id = a.actor_id
      AND c.name = 'Music'
)
ORDER BY a.last_name, a.first_name;
```


## 📘 EJERCICIO 57. Encuentra el título de todas las películas que fueron alquiladas por más de 8 días.















