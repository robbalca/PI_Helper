# PI_Helper
Primer proyecto individual

MovieAPI

Este proyecto pretende tomar dataset acerca de películas y sus plataformas, y mediante estos datos crear 
funciones con las cuales poder solicitarle a una API desplegada en Render la información necesaria, esto lo 
lograremos con las siguientes funciones:

•	@app.get('/peliculas_mes/{mes}'): Se ingresa el mes y la función retorna la cantidad de películas que se   
  estrenaron ese mes históricamente.

•	@app.get('/peliculas_dis/{dis}'): Se ingresa el día y la función retorna la cantidad de películas que se   
  estrenaron ese día históricamente.

•	@app.get('/franquicia/{franquicia}'): Se ingresa la franquicia, retornando la cantidad de películas, ganancia 
  total y promedio.

•	@app.get('/peliculas_pais/{pais}'): Ingresas el país, retornando la cantidad de películas producidas en el mismo.

•	@app.get('/productoras/{productora}'): Ingresas la productora, retornando la ganancia total y la cantidad de 
  películas que produjeron.

•	@app.get('/retorno/{pelicula}'): Ingresas la película, retornando la inversión, la ganancia, el retorno y el 
  año en el que se lanzó.

•	@app.get('/recomendacion/{titulo}'): Ingresas un nombre de película y te recomienda las similares en una lista.


ETL


Antes de hacer las funciones con las que esta API va a trabajar, fue necesario hacer un trabajo previo de ETL donde 
será más fácil trabajar. Algunos de los procesos con los cuales se trabajó este ETL fueron:

•	Algunos campos, como belongs_to_collection, production_companies y otros (ver diccionario de datos) están anidados, 
  esto es o bien tienen un diccionario o una lista como valores en cada fila, ¡deberán desanidarlos para poder y 
  unirlos al dataset de nuevo hacer alguna de las consultas de la API! O bien buscar la manera de acceder a esos datos 
  sin desanidarlos.

•	Los valores nulos de los campos revenue, budget deben ser rellenados por el número 0.

•	Los valores nulos del campo release date deben eliminarse.

•	De haber fechas, deberán tener el formato AAAA-mm-dd, además deberán crear la columna release_year donde extraerán el 
  año de la fecha de estreno.

•	Crear la columna con el retorno de inversión, llamada return con los campos revenue y budget, dividiendo estas dos 
  últimas revenue / budget, cuando no hay datos disponibles para calcularlo, deberá tomar el valor 0.
  
•	Eliminar las columnas que no serán utilizadas: video, imdb_id, adult, original_title, vote_count, poster_path y homepage.


EDA

En el análisis exploratorio de datos podemos buscar patrones en los datos, correlaciones y tendencias.

Por ejemplo, el siguiente grafico nos muestra la relación que hay entre el presupuesto y el tiempo de ejecución de películas:

![image](https://github.com/robbalca/PI_Helper/assets/108275516/bbbad931-501e-43d3-9655-de9ecd81fe12)

De este análisis también podemos encontrar los países que producen más películas.


![image](https://github.com/robbalca/PI_Helper/assets/108275516/41d76bb4-9394-42b5-addc-d852da3380ab)

Aquí están los géneros más producidos y las de menor producción.


![image](https://github.com/robbalca/PI_Helper/assets/108275516/bb42b8b4-f7fc-4028-a46f-df1a29a24b83)

También podemos ver la frecuencia por año de lanzamiento.


![image](https://github.com/robbalca/PI_Helper/assets/108275516/35c610e7-8d2f-412c-8b3b-73a188c312e2)

Modelo de recomendación

Una vez tenemos todo preparado, podemos trabajar un modelo de aprendizaje supervisado, en este caso fue el algoritmo 
support vector machine para ello se tomó como feature a las columnas Budget y reléase_year así podremos visualizar y 
como target, utilizaremos la columna runtime para encontrar una recta que las relacione.






