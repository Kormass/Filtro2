## CREACION DE LAS BASE DE DATOS A TRABAJAR

~~~sql
CREATE DATABASE Proyecto
    DEFAULT CHARACTER SET = 'utf8mb4';


use Proyecto

CREATE TABLE `Conductores`(
    `id_conductor` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `nombre` VARCHAR(255) NOT NULL
);
CREATE TABLE `Estaciones`(
    `id_estacion` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `nombre_estacion` VARCHAR(255) NOT NULL
);
CREATE TABLE `Zonas`(
    `id_zona` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `nombre_zona` VARCHAR(255) NOT NULL,
    `id_estaciones` BIGINT NOT NULL,
    `id_ruta` BIGINT NOT NULL
);
CREATE TABLE `Estacionesxruta`(
    `id_estacion` INT NOT NULL,
    `id_ruta` INT NOT NULL
);
CREATE TABLE `Conductorxdia`(
    `id_conductor` BIGINT NOT NULL,
    `id_bus` BIGINT NOT NULL,
    `dia` BIGINT NOT NULL,
    `id_ruta` BIGINT NOT NULL
);


CREATE TABLE `Rutas`(
    `id_ruta` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `nombre_ruta` INT NOT NULL,
    `tiempo_ruta` VARCHAR(50) NOT NULL
);

drop table Buses

CREATE TABLE `Buses`(
    `id_bus` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `id_placa` VARCHAR (50)
);

INSERT INTO Estacionesxruta (id_ruta, id_estacion) value
(1, 1),
(1, 2),
(1, 3),
(1, 4),
(1, 5),
(1, 6),
(1, 7),
(3, 8),
(3, 9),
(3, 10),
(3, 11),
(3, 12),
(4, 13),
(4, 14),
(4, 15),
(5, 16),
(5, 17),
(8, 18),
(8, 19),
(8, 20);

INSERT INTO Buses (id_placa) value 
("XVH345"),
("XDL965"),
("XFG847"),
("XRJ452"),
("XDF459"),
("XET554"),
("XKL688"),
("XXL757");


INSERT INTO Estaciones (nombre_estacion) value 
("Colseguros"),
("Clínica Chicamocha"),
("Plaza Guarín"),
("Mega Mall"),
("UIS"),
("UDI"),
("Santo Tomás"),
("Boulevard Santander"),
("Búcaros"),
("Rosita"),
("Puerta del Sol"),
("Cacique"),
("Plaza Satélite"),
("La Sirena"),
("Provenza "),
("Fontana"),
("Gibraltar "),
("Terminal"),
("Mutis"),
("Plaza Real");

INSERT INTO Conductores (nombre) value
("Andrés Manuel López Obrador"),
("Nicolás Maduro Moros"),
("Alberto Fernández"),
("Luiz Inácio Lula da Silva"),
("Gabriel Boric"),
("Miguel Díaz-Canel"),
("Daniel Ortega"),
("Gustavo Petro Urrego"),
("Luis Arce"),
("Xiomara Castro");

~~~

### 1. Cantidad de Paradas por Ruta

~~~sql

~~~

### 2. Nombre de las Paradas de la Ruta Universidades

~~~sql
select nombre_estacion from Estaciones
join Rutas ON id_ruta = Estaciones.id_ruta
where nombre_ruta = "Universidades"
~~~

```
+------------------------------+--------------+
| Paradas	                   | Ruta         |
+------------------------------+--------------+
| Colseguros                   |Universidades |
| Clínica Chicamocha           |Universidades |
| Plaza Guarín                 |Universidades |
| Mega Mall                    |Universidades |
| UIS                          |Universidades |
| UDI                          |Universidades |
| Santo Tomás                  |Universidades |
+------------------------------+--------------+
```

### 3. Nombres de las Rutas No Programadas

~~~sql
select nombre_ruta from Rutas
join Estaciones_ruta ON id_ruta = Rutas.id_ruta
where id_ruta ISNULL
~~~

```
+------------------------------+-------------------------+
| nombre_rutas	               |nombre_ruta_no_programada|
+------------------------------+-------------------------+
| Cacique                      |Cacique                  |
|  Prado                       |Prado                    |
|  Cabecera                    |Cabecera                 |
|  Ciudadela                   |Ciudadela                |
|  Punta estrella              |Punta estrella           |
|  Centro Florida              |Centro Florida           |
+------------------------------+-------------------------+
```

### 4. Rutas Programadas sin Conductor Asignado

~~~sql

~~~

### 5. Conductores No Asignados a la Programación

~~~sql
select nombre_conductor from Conductores
where id_instructor not in (select nombre_conductor from conductorxdia where id_conductor is NOT NULL)
~~~

```
+----------------------------------------------------------+
| nombre_conductores          |Conductores_no_asignados    |
+----------------------------------------------------------+
| Andres Manuel Lopez Obrador |Andres Manuel Lopez Obrador |
| Nicolas maduro moros        |Nicolas maduro moros        |
| Luiz Inácio Lula da Silva   |Luiz Inácio Lula da Silva   |
| Gustavo Petro Urrego        |Gustavo Petro Urrego        |
| Luis Arce                   |Luis Arce                   |
+----------------------------------------------------------+
```

### 6. Buses No asignados a la Programación

~~~sql
select placa_bus from Buses
where id_bus not in (select placa_bus from conductorxdia where id_bus is not null)
~~~

```
+----------------------------------------------------------+
| id_Placa      	          |Placas_no_asignada          |
+----------------------------------------------------------+
| XDL965                      |XDL965                      |
| XRJ452                      |XRJ452                      |
| XXL757                      |XXL757                      |
+----------------------------------------------------------+
```

### 7. Zonas NO Programadas

~~~sql
~~~

### 8. Programación asignada a cada conductor (Conductor, Ruta y Día)

~~~sql
select conductor, ruta, dia FROM conductorxdia
~~~

### 9. Programación asignada a conductores que hacen rutas de más de dos horas

~~~sql
select conductor from conductorxdia
join rutas ON id_conductor = conductorxdia.id_conductor
where tiempo < 2:00:00
~~~

### 10. Nombres de Zonas y cantidad de rutas que tienen programadas (Contar)