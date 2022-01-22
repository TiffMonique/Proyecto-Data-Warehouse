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
  <br> <br>
 ______________

 ## Explicación de la base de datos usada
### Base de datos OLTP
 La base de datos que utilizamos es una Base de Datos OLTP, es de creación inédita y está realizada para un restaurante llamado Samogi. Contiene 8 entidades, las cuales son las siguientes: Customers, Ordes, Sizes, Products, Categories, Prices, Employees y Dealers.
La base de datos OLTP se diseñó utilizando un modelo entidad-relación, el cual permitió crear relaciones específicas entre cada una de las entidades.

A continuación, el siguiente diagrama representa el modelo entidad-relación de la Base de datos OLTP.

<div align="center">
    <img src="Diagramas/Diagrama BD .png"> </img> 
     <i> Figura 1 - Base de Datos OLTP</i>
</div><br><br>

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
</div><br><br>

_______________________

## Preguntas del negocio

El restaurante Samogi desea conocer lo siguiente:
1)	Se desea conocer el monto total de ventas en las entregas de platillos en base a los empleados. 
Es necesario conocer el id y nombre completo del empleado que hace la entrega. 
2)	Las ventas deben analizarse por mes, trimestre, semestre (tiempo). 
3)	Se desea conocer el día de la semana (conteo) que representa mayor consumo. 
4)	Se desea conocer la cantidad de clientes atendidos en base al mes. 
5)	Se desea conocer los productos que más y menos se han vendido en el restaurante. Es necesario mostrar el nombre, id del producto categoría y precio.<br><br>


_________



## Explicación de métrica utilizada

A partir de las preguntas de negocio planteadas en el punto anterior identificamos y decidimos que utilizaremos tres métricas. Dado que como primer objetivo de las preguntas del negocio es el de conocer el monto obtenido a través de las ventas, se creó una primera métrica con el nombre Total_Amount, la segunda métrica identificada está basada en el deseo de conocer la cantidad de clientes atendidos en base al mes, por lo tanto, esa métrica se llamó Quantity_Clients. Y para finalizar la métrica número tres que se estableció para formar parte de las que se utilizarían, fue Quantity_Sale_Products haciendo referencia a los productos que más se han vendido o que menos se han vendido en el restaurante.

-	Se desea conocer el **monto total de ventas** en las entregas de platillos en base a los empleados. Es necesario conocer el id y nombre completo del empleado que hace la entrega. 
-	Se desea conocer la **cantidad de clientes** atendidos en base al mes. 
-	Se desea conocer los **productos que más y menos se han vendido** en el restaurante. Es necesario  mostrar el nombre, id del producto categoría y precio.

**Métricas:**

1)	Total_Amount: Monto total de una orden (se debe multiplicar el precio del producto por el número de unidades). 
2)	Quantity_Clients: Cantidad de clientes atendidos durante el mes.
3)	Quantity_Sale_Products: Cuáles son los productos más y menos demandados.<br><br>


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
</div><br>

Cuando las tablas se han llenado se procede a comprobar el éxito de nuestro ETL.
<div align="center">
    <img src="Capturas ETL/ETL - terminado exitoso.png" width="570px"> </img> 
   <br><i> Figura 8 - ETL Completado con éxito</i>
</div>

________
## Creación de Reportes Tableau Desktop
Para la creación de los informes utilizamos Tableau desktop ya que Tableau server pide muchos requerimientos que nuestras computadoras no cumplen.<br>
Tableau es una herramienta de Inteligencia de Negocios que permite analizar, visualizar y compartir grandes volúmenes de información en forma rápida, flexible y amigable. Tableau se destaca por su flexibilidad y rapidez tanto en el procesamiento de los datos, como en la obtención de resultados. Según se necesiten, se pueden ir agregando y cambiando parámetros, añadir puntos de referencia o tendencias y otros elementos que enriquezcan el análisis a realizar. Esto permite que quien lo use, lo haga en forma independiente, liberando recursos del área de sistemas.<br><br>
Ahora podremos realizar análisis con la información y múltiples cantidades de reportes que nos muestran los resultados de la exploración de los datos.<br>
A continuación, se mostrarán algunos de esos análisis:<br>

<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte1.png" width="570px"> </img> 
   <br><i> Figura 9 - Cantidad de productos vendidos por mes.</i>
</div>
<br>

<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte2.png" width="570px"> </img> 
   <br><i> Figura 10 - Cantidad de productos vendidos en el año.</i>
</div>
<br>
<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte3.png" width="570px"> </img> 
   <br><i> Figura 11 - Monto total por un cliente en un trimestre.</i>
</div>
<br>
<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte4.png" width="570px"> </img> 
   <br><i> Figura 12 - Cantidad de Clientes atendidos por mes.</i>
</div>
<br>
<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte5.png" width="570px"> </img> 
   <br><i> Figura 13 - Cantidad de productos distribuidos por cada transportista.</i>
</div>
<br>
<div align="center">
    <img src="Reportes y Dashboards en Tableau/Capturas/Reporte6.png" width="570px"> </img> 
   <br><i> Figura 14 - Monto total generado por mes.</i>
</div><br>

_____________________

## Recursos 
- [Oracle 11g express](https://mega.nz/file/tkFXTQoR#__Px5kB4Da5EZk-rE-KJ1K3JQzunQP2OJQ8uaACI7Ws) 
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15) 
- [SqlDeveloper edición portable](https://mega.nz/file/p58WkRAQ#iD4w3g4XSgJPCr10vZidae-IBcpi_UIRNScL5OrU_7c) 
- [Descarga de Pentaho](https://drive.google.com/file/d/1YxZfSMdk_f4fCKbe93yh278RNzQIMkBK/view) 
- [Tableau Desktop](https://www.tableau.com/products/desktop) 


_____________________
_________

<div align="center">
 
  <p>Facultad de Ingeniería</p>
  <p>Departamento de Ingeniería en Sistemas</p>
  <img src="https://dircom.unah.edu.hn/dmsdocument/7509-unah-version-horizontal-png" width="200px"></img> 
</div>

______
<div align="center">
 Made with ❤️ by <a href="https://github.com/TiffMonique" >TiffMonique</a>😊

</div>

