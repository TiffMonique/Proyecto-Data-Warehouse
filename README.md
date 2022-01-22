<div align="center">
  <h1 >DATA WAREHOUSE</h1>
    <img src="Presentacion Del Proyecto/Cover.png"> </img> 
</div>
  
## Objetivos

### Objetivo General 
Creación de un Data Warehouse como solución de inteligencia de negocios, para optimizar la toma de decisiones en un negocio de venta de comida china con envíos a domicilio.

### Objetivos Específicos
  - Identificar los procesos de toma de decisiones y analizar los requerimientos de información de acuerdo a las perspectivas y necesidades de la empresa. 
  - Creación de Diagrama relacional y el script de la base de datos OLTP.
  - Diseño de la base de datos OLAP modelo en estrella.
  - Desarrollo de ETL que se permita ejecutar siempre de forma exitosa.
 ______________
  
 ## Explicación de la base de datos usada
### Base de datos OLTP
 La base de datos que utilizamos es una Base de Datos OLTP, es de creación inédita y está realizada para un restaurante llamado Samogi. Contiene 8 entidades, las cuales son las siguientes: Customers, Ordes, Sizes, Products, Categories, Prices, Employees y Dealers.
La base de datos OLTP se diseñó utilizando un modelo entidad-relación, el cual permitió crear relaciones específicas entre cada una de las entidades.

A continuación, el siguiente diagrama representa el modelo entidad-relación de la Base de datos OLTP.

<div align="center">
    <img src="Diagramas/Diagrama BD .png"> </img> 
</div>

### Base de datos OLAP
Así como los sistemas OLTP son típicos para bases de datos convencionales y data warehouse, los sistemas OLAP son propios de los datamart. 
Se utilizó el **modelo en estrella** para la creación de nuestra base de datos OLAP.<br>
Las tablas de dimensiones utilizadas fueron cinco y se llamaron de la siguiente forma (Dim Nombre). 
Se realizaron las uniones correspondientes entre la tabla de hechos y las tablas de dimensiones. <br>
**Las tablas de dimensiones:**
-	Dim Products, 
-	Dim Employees ,
-	Dim Customers,
-	Dim Time. <br>
En base a las preguntas del negocio y a la métrica (las cuales se definen en el siguiente enunciado) se determinó que la tabla de Hechos se llamará **Hechos Orders Sales.**<br>
**Campos de Dimensiones:**
Dimensión Products:
-	Product_ID.
-	Product_name.
-	Product_size.
-	Product_price.
-	Product Category.

Dimensión Employees:
-	Employee_ID.
-	Employee_FullName.
Dimensión Customers:
-	Customer_ID.
-	Customer_FullName. 





