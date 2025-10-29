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






