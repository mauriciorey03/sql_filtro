### CREACIÓN DE DATABASE

------

```sql
DROP DATABASE IF EXISTS filtro_mysql;
CREATE DATABASE filtro_mysql;
USE filtro_mysql;
```
### ELIMINAR TABLAS ANTERIORES  DE DATABASE

------

```
--ELIMINACIÓN DE TABLES ANTERIORES
DROP TABLE IF EXISTS zona;
DROP TABLE IF EXISTS parada;
DROP TABLE IF EXISTS bus;
DROP TABLE IF EXISTS conductor;
DROP TABLE IF EXISTS ruta;
DROP TABLE IF EXISTS estacionxruta;
DROP TABLE IF EXISTS planeacion;
DROP TABLE IF EXISTS zonaxruta;
```

### CREACIÓN DE TABLAS

------

```sql
--CREACIÓN DE TABLAS
CREATE TABLE zona (
    id_zona int NOT NULL PRIMARY KEY,
    zona varchar(32) NOT NULL
    );

CREATE TABLE parada (
    id_parada INT NOT NULL PRIMARY KEY,
    parada VARCHAR(255) NOT NULL
);

CREATE TABLE bus (
    id_bus INT NOT NULL PRIMARY KEY,
    bus VARCHAR(255) NOT NULL
);

CREATE TABLE conductor (
    id_conductor INT NOT NULL PRIMARY KEY,
    conductor VARCHAR(255) NOT NULL
);

CREATE TABLE ruta (
    id_ruta int NOT NULL PRIMARY KEY,
    ruta varchar(50) NOT NULL,
    tiempo TIME NOT NULL
);

CREATE TABLE estacionesxruta (
    id_ruta int NOT NULL,
    id_parada int NOT NULL,
    inicio VARCHAR(200) NULL,
    final VARCHAR(200) NULL,
    FOREIGN KEY (id_ruta) REFERENCES ruta (id_ruta),
    FOREIGN KEY (id_parada) REFERENCES parada (id_parada)
);

CREATE TABLE planeacion (
    dia varchar(50) NOT NULL,
    id_ruta int NOT NULL,
    id_conductor int NOT NULL,
    id_bus int NOT NULL,
    FOREIGN KEY (id_ruta) REFERENCES ruta (id_ruta),
    FOREIGN KEY (id_conductor) REFERENCES conductor (id_conductor),
    FOREIGN KEY (id_bus) REFERENCES bus (id_bus)
);

CREATE TABLE zonaxruta (
    id_zona int NOT NULL,
    id_ruta int NOT NULL,
    FOREIGN KEY (id_zona) REFERENCES zona (id_zona),
    FOREIGN KEY (id_ruta) REFERENCES ruta (id_ruta)
);
```

### INFORMACIÓN PARA POBLAR

------

```sql
--DATOS PARA POBLAR

INSERT INTO zona (id_zona, zona)
VALUES 
(1,'Norte'), 
(2,'Sur'), 
(3,'Oriente'), 
(4,'Occidente'), 
(5,'Floridablanca'),
(6,'Girón'),
(7,'Piedecuesta');

INSERT INTO parada (id_parada, parada)
VALUES 
(1,'Colseguros'),
(2,'Clínica Chicamocha'),
(3,'Plaza Guarín'),
(4,'Mega Mall'),
(5,'UIS'),
(6,'UDI'),
(7,'Santo Tomás'),
(8,'Boulevard Santander'),
(9,'Búcaros'),
(10,'Rosita'),
(11,'Puerta del Sol'),
(12,'Cacique'),
(13,'Plaza Satélite'),
(14,'La Sirena'),
(15,'Provenza'),
(16,'Fontana'),
(17,'Gibraltar'),
(18,'Terminal'),
(19,'Mutis'),
(20,'Plaza Real');

INSERT INTO bus (id_bus, bus)
VALUES 
(1,'XVH345'), 
(2,'XDL965'),
(3,'XFG847'), 
(4,'XRJ452'), 
(5,'XDF459'),
(6,'XET554'),
(7,'XKL688'),
(8,'XXL757');

INSERT INTO conductor (id_conductor, conductor)
VALUES 
(1,'Andrés Manuel López Obrador'), 
(2,'Nicolás Maduro Moros'), 
(3,'Alberto Fernández'), 
(4,'Luiz Inácio Lula da Silva'), 
(5,'Gabriel Boric'),
(6,'Miguel Díaz-Canel'),
(7,'Daniel Ortega'),
(8,'Gustavo Petro Urrego'),
(9,'Luis Arce'),
(10,'Xiomara Castro');

INSERT INTO ruta (id_ruta, ruta,tiempo)
VALUES 
(1,"Universidades", "2:00:00"), 
(2,"Café Madrid", "2:15:00"), 
(3,"Cacique", "1:45:00"), 
(4,"Diamantes", "1:50:00"), 
(5,"Terminal", "2:00:00"), 
(6,"Prado", "1:30:00"), 
(7,"Cabecera", "1:30:00"), 
(8,"Ciudadela", "2:00:00"), 
(9,"Punta Estrella", "2:30:00"), 
(10,"Niza", "2:45:00"), 
(11,"Autopista", "2:15:00"), 
(12,"Lagos", "2:15:00"), 
(13,"Centro Florida", "2:30:00");

INSERT INTO estacionesxruta (id_ruta, id_parada, inicio, final)
VALUES 
(1,1,"Inicio", "Final"),
(1,2,"Inicio", "Final"),
(1,3,"Inicio", "Final"),
(1,4,"Inicio", "Final"),
(1,5,"Inicio", "Final"),
(1,6,"Inicio", "Final"),
(1,7,"Inicio", "Final"),
(3,8,"Inicio", "Final"),
(3,9,"Inicio", "Final"),
(3,10,"Inicio", "Final"),
(3,11,"Inicio", "Final"),
(3,12,"Inicio", "Final"),
(4,13,"Inicio", "Final"),
(4,14,"Inicio", "Final"),
(4,15,"Inicio", "Final"),
(5,16,"Inicio", "Final"),
(5,17,"Inicio", "Final"),
(8,18,"Inicio", "Final"),
(8,19,"Inicio", "Final"),
(8,20,"Inicio", "Final");

INSERT INTO planeacion(id_conductor, id_bus, dia, id_ruta)
VALUES 
    (5, 1, "Lunes", 1),
    (5, 1, "Martes", 1),
    (5, 3, "Miércoles", 1),
    (5, 3, "Jueves", 1),
    (5, 5, "Viernes", 2),
    (5, 5, "Sábado", 2),
    (5, 5, "Domingo", 2),
    (3, 5, "Lunes", 4),
    (3, 6, "Martes", 4),
    (3, 1, "Miércoles", 4),
    (3, 1, "Jueves", 5),
    (3, 3, "Viernes", 5),
    (3, 3, "Sábado", 5),
    (3, 3, "Domingo", 5),
    (10, 3, "Lunes", 10),
    (10, 3, "Martes", 10),
    (10, 5, "Miércoles", 10),
    (10, 5, "Jueves", 10),
    (10, 4, "Viernes", 10),
    (10, 7, "Sábado", 11),
    (10, 7, "Domingo", 11),
    (7, 7, "Lunes", 11),
    (7, 7, "Martes", 11),
    (6, 7, "Miércoles", 12),
    (6, 7, "Jueves", 12),
    (6, 7, "Viernes", 12),
    (6, 6, "Sábado", 12),
    (6, 6, "Domingo", 12);

INSERT INTO zonaxruta (id_zona, id_ruta)
VALUES 
(1,1),
(1,2),
(4,4),
(4,5),
(5,10),
(5,11),
(5,12)
;
```

------

### CONSULTAS PROPUESTAS

1.  Cantidad de Paradas por Ruta

2.  Nombre de las Paradas de la Ruta Universidades

```
SELECT DISTINCT ruta, parada 

FROM parada 

INNER JOIN estacionesxruta ON estacionesxruta.id_parada = parada.id_parada

INNER JOIN ruta ON estacionesxruta.id_ruta = ruta.id_ruta

WHERE ruta.ruta LIKE "Universidades";
```

+---------------+--------------------+
| ruta          | parada             |
+---------------+--------------------+
| Universidades | Colseguros         |
| Universidades | Clínica Chicamocha |
| Universidades | Plaza Guarín       |
| Universidades | Mega Mall          |
| Universidades | UIS                |
| Universidades | UDI                |
| Universidades | Santo Tomás        |

3.  Nombres de las Rutas No Programadas

```
SELECT RUTA AS "RUTAS NO PROGRAMADAS"

FROM RUTA AS R

LEFT JOIN planeacion ON planeacion.id_ruta = r.id_ruta

WHERE planeacion.id_conductor IS NULL;
```

+----------------------+
| RUTAS NO PROGRAMADAS |
+----------------------+
| Cacique              |
| Prado                |
| Cabecera             |
| Ciudadela            |
| Punta Estrella       |
| Centro Florida       |
+----------------------+
6 rows in set (0.00 sec)

4.  Rutas Programadas sin Conductor Asignado

```
SELECT conductor AS VALIDACION, ruta AS "RUTAS SIN CONDUCTOR"

FROM ruta  

LEFT JOIN planeacion ON planeacion.id_ruta=ruta.id_ruta

LEFT JOIN conductor ON conductor.id_conductor=planeacion.id_conductor

WHERE conductor is NULL;
```

+------------+---------------------+
| VALIDACION | RUTAS SIN CONDUCTOR |
+------------+---------------------+
| NULL       | Cacique             |
| NULL       | Prado               |
| NULL       | Cabecera            |
| NULL       | Ciudadela           |
| NULL       | Punta Estrella      |
| NULL       | Centro Florida      |
+------------+---------------------+
6 rows in set (0.00 sec)

5. Conductores No Asignados a la Programación

```
SELECT conductor, ruta

FROM ruta  

LEFT JOIN planeacion ON planeacion.id_ruta=ruta.id_ruta

LEFT JOIN conductor ON conductor.id_conductor=planeacion.id_conductor

WHERE planeacion.id_conductor is NULL;
```

+-----------+----------------+
| conductor | ruta           |
+-----------+----------------+
| NULL      | Cacique        |
| NULL      | Prado          |
| NULL      | Cabecera       |
| NULL      | Ciudadela      |
| NULL      | Punta Estrella |
| NULL      | Centro Florida |
+-----------+----------------+
6 rows in set (0.00 sec)

6. Buses No asignados a la Programación

```
SELECT DISTINCT BUS

FROM bus  

RIGHT JOIN planeacion ON planeacion.id_bus=bus.id_bus;
```

+--------+
| BUS    |
+--------+
| XVH345 |
| XFG847 |
| XRJ452 |
| XDF459 |
| XET554 |
| XKL688 |
+--------+
6 rows in set (0.00 sec)

7. Zonas NO Programadas

```
SELECT DISTINCT zona

FROM zona  

INNER JOIN zonaxruta ON zonaxruta.id_zona=zona.id_zona

INNER JOIN planeacion ON zonaxruta.id_ruta=planeacion.id_ruta

;
```

+---------------+
| zona          |
+---------------+
| Norte         |
| Occidente     |
| Floridablanca |
+---------------+
3 rows in set (0.00 sec)



8. Programación asignada a cada conductor (Conductor, Ruta y Día)

```
SELECT DISTINCT conductor,  ruta, dia

FROM ruta  

INNER JOIN planeacion ON planeacion.id_ruta=ruta.id_ruta

INNER JOIN conductor ON conductor.id_conductor=planeacion.id_conductor

;
```

| conductor         | ruta          | dia       |
+-------------------+---------------+-----------+
| Gabriel Boric     | Universidades | Lunes     |
| Gabriel Boric     | Universidades | Martes    |
| Gabriel Boric     | Universidades | Miércoles |
| Gabriel Boric     | Universidades | Jueves    |
| Gabriel Boric     | Café Madrid   | Viernes   |
| Gabriel Boric     | Café Madrid   | Sábado    |
| Gabriel Boric     | Café Madrid   | Domingo   |
| Alberto Fernández | Diamantes     | Lunes     |
| Alberto Fernández | Diamantes     | Martes    |
| Alberto Fernández | Diamantes     | Miércoles |
| Alberto Fernández | Terminal      | Jueves    |
| Alberto Fernández | Terminal      | Viernes   |
| Alberto Fernández | Terminal      | Sábado    |
| Alberto Fernández | Terminal      | Domingo   |
| Xiomara Castro    | Niza          | Lunes     |
| Xiomara Castro    | Niza          | Martes    |
| Xiomara Castro    | Niza          | Miércoles |
| Xiomara Castro    | Niza          | Jueves    |
| Xiomara Castro    | Niza          | Viernes   |
| Xiomara Castro    | Autopista     | Sábado    |
| Xiomara Castro    | Autopista     | Domingo   |
| Daniel Ortega     | Autopista     | Lunes     |
| Daniel Ortega     | Autopista     | Martes    |
| Miguel Díaz-Canel | Lagos         | Miércoles |
| Miguel Díaz-Canel | Lagos         | Jueves    |
| Miguel Díaz-Canel | Lagos         | Viernes   |
| Miguel Díaz-Canel | Lagos         | Sábado    |
| Miguel Díaz-Canel | Lagos         | Domingo   |
+-------------------+---------------+-----------+
28 rows in set (0.00 sec)

9. Programación asignada a conductores que hacen rutas de más de dos horas

```
SELECT conductor, ruta, tiempo

FROM ruta  

INNER JOIN planeacion ON planeacion.id_ruta=ruta.id_ruta

INNER JOIN conductor ON conductor.id_conductor=planeacion.id_conductor

WHERE tiempo > (2-00-00);
```

| conductor         | ruta          | tiempo   |
+-------------------+---------------+----------+
| Gabriel Boric     | Universidades | 02:00:00 |
| Gabriel Boric     | Universidades | 02:00:00 |
| Gabriel Boric     | Universidades | 02:00:00 |
| Gabriel Boric     | Universidades | 02:00:00 |
| Gabriel Boric     | Café Madrid   | 02:15:00 |
| Gabriel Boric     | Café Madrid   | 02:15:00 |
| Gabriel Boric     | Café Madrid   | 02:15:00 |
| Alberto Fernández | Diamantes     | 01:50:00 |
| Alberto Fernández | Diamantes     | 01:50:00 |
| Alberto Fernández | Diamantes     | 01:50:00 |
| Alberto Fernández | Terminal      | 02:00:00 |
| Alberto Fernández | Terminal      | 02:00:00 |
| Alberto Fernández | Terminal      | 02:00:00 |
| Alberto Fernández | Terminal      | 02:00:00 |
| Xiomara Castro    | Niza          | 02:45:00 |
| Xiomara Castro    | Niza          | 02:45:00 |
| Xiomara Castro    | Niza          | 02:45:00 |
| Xiomara Castro    | Niza          | 02:45:00 |
| Xiomara Castro    | Niza          | 02:45:00 |
| Xiomara Castro    | Autopista     | 02:15:00 |
| Xiomara Castro    | Autopista     | 02:15:00 |
| Daniel Ortega     | Autopista     | 02:15:00 |
| Daniel Ortega     | Autopista     | 02:15:00 |
| Miguel Díaz-Canel | Lagos         | 02:15:00 |
| Miguel Díaz-Canel | Lagos         | 02:15:00 |
| Miguel Díaz-Canel | Lagos         | 02:15:00 |
| Miguel Díaz-Canel | Lagos         | 02:15:00 |
| Miguel Díaz-Canel | Lagos         | 02:15:00 |
+-------------------+---------------+----------+
28 rows in set (0.00 sec)

10. Nombres de Zonas y cantidad de rutas que tienen programadas (Contar)
