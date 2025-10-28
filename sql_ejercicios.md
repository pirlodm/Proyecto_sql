# 📘 EJERCICIO 1.
##Crea el esquema de la BBDD.  
###Se adjunta el fichero `diagrama_peliculasSQL.jpg`, que contiene el diagrama de la base de datos `peliculasSQL`.  

# 📘 EJERCICIO 2. ### Muestra los nombres de todas las películas con una clasificación por edades de ‘Rʼ.  

```sql
SELECT f.title AS Nombre_Pelicula
FROM film f
WHERE f.rating = 'R';

## 📘 EJERCICIO 3. Encuentra los nombres de los actores que tengan un “actor_idˮ entre 30 y 40.
