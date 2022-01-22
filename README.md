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
     <i> Figura 1 - Base de Datos OLTP</i>
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

En base a las preguntas del negocio y a la métrica (las cuales se definen en el siguiente enunciado) se determinó que la tabla de Hechos se llamará **Hechos Orders Sales.**
<br>

**Campos de Dimensiones:**<br>

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


Después de haber definido las tablas dimensionales del cubo, queda definir la tabla dimensional de time, la cual siempre debe ir en todo modelo de DWH. Los campos que tiene determinada tabla dimensional dependen de las necesidades del negocio. Para este caso se decidió la siguiente división de tiempo.

Dimensión Time:

-	Time_ID.
-	Month.
-	Trimester.
-	Semester.
-	Week_day.

Por último, queda definir la tabla de hechos. Esta tabla contiene los id de las tablas dimensionales y las métricas, las cuales se utilizarán para la medición que proporcionan los datos del cubo. 

Campos Tabla de Hechos:

-	Hecho_ID (Llave primaria, valor autoincremental)
-	Product_ID
-	Employee_ID
-	Customer_ID.
-	Time_ID.
-	Total_Amount  (métrica).
-	Quantity_Clients (métrica).
-	Quantity_Sale_Products (métrica).


<div align="center">
    <img src="Diagramas/Diagrama Modelo en Estrella - Restaurante Samogi.png" width="800px"> </img> 
   <br><i> Figura 2 - Base de datos OLAP - Data Mart</i>
</div>

_______________________

## Preguntas del negocio

El restaurante Samogi desea conocer lo siguiente:
1)	Se desea conocer el monto total de ventas en las entregas de platillos en base a los empleados. 
Es necesario conocer el id y nombre completo del empleado que hace la entrega. 
2)	Las ventas deben analizarse por mes, trimestre, semestre (tiempo). 
3)	Se desea conocer el día de la semana (conteo) que representa mayor consumo. 
4)	Se desea conocer la cantidad de clientes atendidos en base al mes. 
5)	Se desea conocer los productos que más y menos se han vendido en el restaurante. Es necesario mostrar el nombre, id del producto categoría y precio.
__________

## Explicación de métrica utilizada

A partir de las preguntas de negocio planteadas en el punto anterior identificamos y decidimos que utilizaremos tres métricas. Dado que como primer objetivo de las preguntas del negocio es el de conocer el monto obtenido a través de las ventas, se creó una primera métrica con el nombre Total_Amount, la segunda métrica identificada está basada en el deseo de conocer la cantidad de clientes atendidos en base al mes, por lo tanto, esa métrica se llamó Quantity_Clients. Y para finalizar la métrica número tres que se estableció para formar parte de las que se utilizarían, fue Quantity_Sale_Products haciendo referencia a los productos que más se han vendido o que menos se han vendido en el restaurante.

-	Se desea conocer el **monto total de ventas** en las entregas de platillos en base a los empleados. Es necesario conocer el id y nombre completo del empleado que hace la entrega. 
-	Se desea conocer la **cantidad de clientes** atendidos en base al mes. 
-	Se desea conocer los **productos que más y menos se han vendido** en el restaurante. Es necesario  mostrar el nombre, id del producto categoría y precio.

**Métricas:**

1)	Total_Amount: Monto total de una orden (se debe multiplicar el precio del producto por el número de unidades). 
2)	Quantity_Clients: Cantidad de clientes atendidos durante el mes.
3)	Quantity_Sale_Products: Cuáles son los productos más y menos demandados.

_____________

## Creación de ETL en Pentaho

El proceso de ETL se encargará de extraer, transformar y cargar la información en la base de datos OLAP. 

Fue creado en Pentaho, una plataforma de inteligencia empresarial (BI) “orientada a la solución” y “centrada en procesos” que incluye todos los principales componentes requeridos para implementar soluciones basadas en procesos tal como ha sido concebido desde el principio.

<div align="center">
    <img src="Capturas ETL/ETL - terminado exitoso.png" width="800px"> </img> 
   <br><i> Figura 3 - ETL Completo </i>
</div>

**Limpieza de datos:** Su objetivo es el de realizar diferentes tipos de acciones con la finalidad de solucionar problemas con datos erróneos, inconsistentes o irrelevantes.

<div align="center">
    <img src="Capturas ETL/Limpiar Dimensiones exitoso.png" width="800px"> </img> 
   <br><i> Figura 4 - Limpieza de tablas Dimensiones </i>
</div>
<br>
Una vez limpiadas las tablas de dimensiones procedemos a limpiar la tabla de hechos.
<br>
<div align="center">
  <img src="Capturas ETL/Limpiar tabla_Hechos exitoso.png" ></img>  <br>
  <i>Figura 5 - Limpieza de tabla Hechos </i> 
</div>
<br>
Después de la limpieza se procede al llenado de las tablas de dimensiones

<div align="center">
    <img src="Capturas ETL/Llenar tablas Dimensiones exitoso.png" width="570px"> </img> 
   <br><i> Figura 6 - Llenar tablas Dimensiones </i>
</div>
<br>

Una vez que habíamos llenado la tabla de dimensiones. Fue posible llenar la tabla de hechos que depende de las tablas de dimensiones.

<div align="center">
    <img src="Capturas ETL/imagen 4 -tabla hechos.png" width="570px"> </img> 
   <br><i> Figura 7 - Llenar tabla Hechos </i>
</div>

