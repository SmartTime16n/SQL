# Proyecto uso de SQL en bases de datos
### Julian Villaseñor Ibarra
### Maestria en Ciencia de datos

En este trabajo vamos a usar un data set de kaggle llamado 'US Cars' que usaremos para hacer consultas, usare postgres para hacer las querys,
lo primero que necesitamos en postgres es crear una base de datos, esto se hace con un "CREATE DATABASE ejercicio", igual la podemos eliminar don un
"DROP DATABASE ejercicio", ya que tenemos nuestra base de datos podemos comenzar a crear nuestras tablas, como para el ejercicio empezare usando un
data set de kaggle primero creare una tabla para poner todos los datos ahi, es importante que las columnas que se creen para la tabla puedan almacenar
los datos que se encuentra en el csv, es decir si los datos son flotantes, la columna tiene que ser de tipo float, si son string tiene que ser de tipo varchar()
, si son fechas se recomienda el formato DATE para poder realizar un order by luego a esa columna, identificar la columna identidad del dataset, para asignarle
la primary key, con esto podremos crear otra tabla que pueda hacer una referencia a esta columna con las foregin keys, es importante es lo que le va a dar una 
estructura relacional a nuestra base de datos. Despues de revisar el contenido del csv realice la siguiente query:   
CREATE TABLE usa_cars (  
id SERIAL PRIMARY KEY,  
price INTEGER,  
brand VARCHAR(45),  
model VARCHAR(45),  
year INTEGER,  
title_status VARCHAR,  
milage FLOAT,  
color VARCHAR(45),  
vin VARCHAR(255),  
lot BIGINT,  
state VARCHAR(45),  
country VARCHAR(45),  
condition VARCHAR(45)  
)  
Con esto creamos nuestra tabla y estamos listos para poner la informacion del csv en el :  

<img src="select_usa_cars.png" width="400" height="300" alt="Texto alternativo">

Muy bien ahora podemos proceder a usar COPY para poner los datos del csv, es importante conocer la ruta de nuestro documento y que sea un documento publico en la pc, es decir que tenga permisos de lectura y escritura para poder ponder los datos en nuestra tabla, una vez que veamos la ruta y los permisios en propiedades en security, podemos aplicar nuestra query:  
COPY usa_cars (id,price, brand, model, year, title_status, mileage, color, vin, lot, state, country, condition)  
FROM 'C:\Users\Public\Documents\csv\USA_cars_datasets.csv'  
DELIMITER ','  
CSV HEADER;  
<img src="select_usa_copy.png" width="400" height="300" alt="Texto alternativo">

Muy bien ya tenemos los datos dentro de postgres, ahora podemos hacer consultas exploartorias de nuestros datos, usaremos MAX(), MIN(), AVG(), DISTINCT(),
ORDER BY, GROUP BY y LIMIT. Primero quiero saber que marcas de carro tenemos en el dataset, lo consultare usando DISTINCT: SELECT  DISTINCT(brand) FROM usa_cars;  
"chevrolet"  
"mazda"  
"audi"  
"acura"  
"nissan"  
"mercedes-benz"  
"chrysler"  
"ram"  
"bmw"  
Muy bien ahora sabemos cuales son las marcas de carro que tiene el dataset, muy bien quiero saber cuales son los 5 carros mas caros que tenemos en el dataset, de que marca son , cual es el modelo, cual es el precio, su color, su kilometrage y su condicion, para esto usare el siguiente query:  
SELECT brand, model, year, title_status, milage, color, price from usa_cars order by price desc limit 5  
