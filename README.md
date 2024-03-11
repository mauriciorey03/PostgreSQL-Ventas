### CREACIÓN DE TABLAS  POSTGRESQL -  VENTAS


```postgresql
DROP DATABASE IF EXISTS ventas;
CREATE DATABASE ventas;

CREATE TABLE cliente (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  apellido1 VARCHAR(100) NOT NULL,
  apellido2 VARCHAR(100),
  ciudad VARCHAR(100),
  categoria INT 
);

CREATE TABLE comercial (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  apellido1 VARCHAR(100) NOT NULL,
  apellido2 VARCHAR(100),
  comisión FLOAT
);

CREATE TABLE pedido (
  id SERIAL PRIMARY KEY,
  total FLOAT NOT NULL,
  fecha DATE,
  id_cliente INT NOT NULL,
  id_comercial INT NOT NULL,
  FOREIGN KEY (id_cliente) REFERENCES cliente(id),
  FOREIGN KEY (id_comercial) REFERENCES comercial(id)
);

INSERT INTO cliente VALUES(1, 'Aarón', 'Rivero', 'Gómez', 'Almería', 100);
INSERT INTO cliente VALUES(2, 'Adela', 'Salas', 'Díaz', 'Granada', 200);
INSERT INTO cliente VALUES(3, 'Adolfo', 'Rubio', 'Flores', 'Sevilla', NULL);
INSERT INTO cliente VALUES(4, 'Adrián', 'Suárez', NULL, 'Jaén', 300);
INSERT INTO cliente VALUES(5, 'Marcos', 'Loyola', 'Méndez', 'Almería', 200);
INSERT INTO cliente VALUES(6, 'María', 'Santana', 'Moreno', 'Cádiz', 100);
INSERT INTO cliente VALUES(7, 'Pilar', 'Ruiz', NULL, 'Sevilla', 300);
INSERT INTO cliente VALUES(8, 'Pepe', 'Ruiz', 'Santana', 'Huelva', 200);
INSERT INTO cliente VALUES(9, 'Guillermo', 'López', 'Gómez', 'Granada', 225);
INSERT INTO cliente VALUES(10, 'Daniel', 'Santana', 'Loyola', 'Sevilla', 125);

INSERT INTO comercial VALUES(1, 'Daniel', 'Sáez', 'Vega', 0.15);
INSERT INTO comercial VALUES(2, 'Juan', 'Gómez', 'López', 0.13);
INSERT INTO comercial VALUES(3, 'Diego','Flores', 'Salas', 0.11);
INSERT INTO comercial VALUES(4, 'Marta','Herrera', 'Gil', 0.14);
INSERT INTO comercial VALUES(5, 'Antonio','Carretero', 'Ortega', 0.12);
INSERT INTO comercial VALUES(6, 'Manuel','Domínguez', 'Hernández', 0.13);
INSERT INTO comercial VALUES(7, 'Antonio','Vega', 'Hernández', 0.11);
INSERT INTO comercial VALUES(8, 'Alfredo','Ruiz', 'Flores', 0.05);

INSERT INTO pedido VALUES(1, 150.5, '2017-10-05', 5, 2);
INSERT INTO pedido VALUES(2, 270.65, '2016-09-10', 1, 5);
INSERT INTO pedido VALUES(3, 65.26, '2017-10-05', 2, 1);
INSERT INTO pedido VALUES(4, 110.5, '2016-08-17', 8, 3);
INSERT INTO pedido VALUES(5, 948.5, '2017-09-10', 5, 2);
INSERT INTO pedido VALUES(6, 2400.6, '2016-07-27', 7, 1);
INSERT INTO pedido VALUES(7, 5760, '2015-09-10', 2, 1);
INSERT INTO pedido VALUES(8, 1983.43, '2017-10-10', 4, 6);
INSERT INTO pedido VALUES(9, 2480.4, '2016-10-10', 8, 3);
INSERT INTO pedido VALUES(10, 250.45, '2015-06-27', 8, 2);
INSERT INTO pedido VALUES(11, 75.29, '2016-08-17', 3, 7);
INSERT INTO pedido VALUES(12, 3045.6, '2017-04-25', 2, 1);
INSERT INTO pedido VALUES(13, 545.75, '2019-01-25', 6, 1);
INSERT INTO pedido VALUES(14, 145.82, '2017-02-02', 6, 1);
INSERT INTO pedido VALUES(15, 370.85, '2019-03-11', 1, 5);
INSERT INTO pedido VALUES(16, 2389.23, '2019-03-11', 1, 5);


```


### Consultas básicas

1. Consulta 1

   ```postgresql
    SELECT * FROM pedido 
    ORDER BY fecha DESC;
   ```

   <img src="C:\Users\mauri\AppData\Roaming\Typora\typora-user-images\image-20240311144225695.png" alt="image-20240311144225695" style="zoom:50%;" />

2. Consulta 2

   ```postgresql
   SELECT * 
   FROM pedido 
   ORDER BY total 
   DESC LIMIT 2;
   ```

   ![image-20240311144259347](C:\Users\mauri\AppData\Roaming\Typora\typora-user-images\image-20240311144259347.png)

3. Consulta 3

   ```postgresql
   SELECT DISTINCT id_cliente 
   FROM pedido;
   ```

   ![image-20240311144336014](C:\Users\mauri\AppData\Roaming\Typora\typora-user-images\image-20240311144336014.png)

4. Consulta 4

   ```postgresql
   SELECT * 
   FROM pedido 
   WHERE fecha 
   BETWEEN '2017-01-01' AND '2017-12-31' AND total > 500;
   ```

   ![image-20240311144405502](C:\Users\mauri\AppData\Roaming\Typora\typora-user-images\image-20240311144405502.png)

5. Consulta 5

   ```postgresql
   SELECT nombre || ' '  || apellido1 || ' '|| apellido2 AS COMERCIAL, comisión 
   FROM COMERCIAL 
   WHERE comisión 
   BETWEEN 0.05 AND 0.11 ;
   ```

   ![image-20240311144422257](C:\Users\mauri\AppData\Roaming\Typora\typora-user-images\image-20240311144422257.png)

6. Consulta 6

   ```postgresql
   SELECT MAX(comisión) 
   FROM comercial;
   ```

7. Consulta 7

   ```postgresql
   SELECT id, nombre, apellido1 
   FROM cliente 
   WHERE apellido2 IS NOT NULL 
   ORDER BY apellido1;
   ```

8. Consulta 8

   ```postgresql
   SELECT * 
   FROM cliente 
   WHERE nombre 
   LIKE 'A%' AND nombre LIKE '%n' OR nombre LIKE 'P%' 
   ORDER BY nombre;
   ```

9. Consulta 9

   ```postgresql
   SELECT * 
   FROM cliente 
   WHERE nombre NOT LIKE 'A%'
   ORDER BY nombre;
   ```

10. Consulta 10

    ```postgresql
    SELECT DISTINCT nombre 
    FROM comercial 
    WHERE nombre LIKE '%el' OR nombre LIKE '%o' 
    ORDER BY nombre;
    ```

### CONSULTAS MULTITABLA

1. CONSULTA  MULTITABLA #1

    ```postgresql
    SELECT DISTINCT C.id, C.nombre, C.apellido1, C.apellido2 
    FROM cliente C 
    INNER JOIN pedido P ON C.id = P.id_cliente 
    ORDER BY 3 ASC, 4 ASC, 2 ASC;
    ```

2. CONSULTA  MULTITABLA #2

    ```postgresql
    SELECT c.id, c.nombre, c.apellido1, c.apellido2, p.id, p.fecha, p.total
    FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente
    ORDER BY 3 ASC, 4 ASC, 2 ASC;
    ```

3. CONSULTA  MULTITABLA #3

    ```postgresql
    SELECT co.nombre, co.apellido1, co.apellido2, p.id, p.fecha, p.total
    FROM comercial co INNER JOIN pedido p ON co.id = p.id_cliente
    ORDER BY 2 ASC, 3 ASC, 1 ASC;
    ```

4. CONSULTA  MULTITABLA #4
    ```postgresql
    SELECT *
    FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente 
    INNER JOIN comercial co ON p.id_comercial = co.id;
    ```

5. CONSULTA  MULTITABLA #5
    ```postgresql
    SELECT *
    FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente
    WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31' AND p.total BETWEEN 300 AND 1000
    ```
6. CONSULTA  MULTITABLA #6
    ```postgresql
    SELECT MAX(comisión)
    FROM comercial c;
    ```

7. CONSULTA  MULTITABLA #7
    ```postgresql
    SELECT c.id, c.nombre, c.apellido1
    FROM cliente c
    WHERE c.apellido2 IS NOT NULL 
    ORDER BY 3 ASC, 2 ASC;
    ```

8. CONSULTA  MULTITABLA #8
    ```postgresql
    SELECT c.nombre
    FROM cliente c
    WHERE c.nombre ILIKE 'a%' AND c.nombre LIKE '%n' OR c.nombre LIKE 'p%'
    ORDER BY 1 ASC;
    ```
    
9. CONSULTA  MULTITABLA #9
    ```postgresql
    SELECT c.nombre
    FROM cliente c
    WHERE c.nombre NOT ILIKE 'a%'
    ORDER BY 1 ASC;
	```
	
10. CONSULTA  MULTITABLA #10
    ```postgresql
    SELECT DISTINCT c.nombre
    FROM comercial c
    WHERE c.nombre LIKE '%el' OR c.nombre LIKE '%o';
    ```
    

### CONSULTAS MULTITABLA (Composición interna)

--CONSULTA #1

```postgresql
SELECT DISTINCT c.id, c.nombre, c.apellido1, c.apellido2
FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente
ORDER BY 3 ASC, 4 ASC, 2 ASC;
```

--CONSULTA #2
```postgresql
SELECT c.id, c.nombre, c.apellido1, c.apellido2, p.id, p.fecha, p.total
FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente
ORDER BY 3 ASC, 4 ASC, 2 ASC;
```

--CONSULTA #3
```postgresql
SELECT co.nombre, co.apellido1, co.apellido2, p.id, p.fecha, p.total
FROM comercial co INNER JOIN pedido p ON co.id = p.id_cliente
ORDER BY 2 ASC, 3 ASC, 1 ASC;
```

--CONSULTA #4
```postgresql
SELECT *
FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente 
INNER JOIN comercial co ON p.id_comercial = co.id;
```

--CONSULTA #5
```postgresql
SELECT *
FROM cliente c INNER JOIN pedido p ON c.id = p.id_cliente
WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31' AND p.total BETWEEN 300 AND 1000;
```

--CONSULTA #6
```postgresql
SELECT DISTINCT co.nombre, co.apellido1, co.apellido2
FROM comercial co INNER JOIN pedido p ON co.id = p.id_comercial
INNER JOIN cliente c ON p.id_cliente = c.id
WHERE c.nombre = 'María' AND c.apellido1 = 'Santana' AND c.apellido2 = 'Moreno'
```

--CONSULTA #7
```postgresql
SELECT DISTINCT c.nombre, c.apellido1, c.apellido2
FROM comercial co INNER JOIN pedido p ON co.id = p.id_comercial
INNER JOIN cliente c ON p.id_cliente = c.id
WHERE co.nombre = 'Daniel' AND co.apellido1 = 'Sáez' AND co.apellido2 = 'Vega'
```

### CONSULTAS MULTITABLA (Composición externa)
--CONSULTA #1
```postgresql
SELECT *
FROM cliente c LEFT JOIN pedido p ON c.id = p.id_cliente
ORDER BY c.apellido1 ASC, c.apellido2 ASC, c.nombre ASC 
```

--CONSULTA #2
```postgresql
SELECT *
FROM comercial c LEFT JOIN pedido p ON c.id = p.id_cliente
ORDER BY c.apellido1 ASC, c.apellido2 ASC, c.nombre ASC 
```
--CONSULTA #3
```postgresql
SELECT *
FROM cliente c LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE p.id_cliente IS NULL
ORDER BY c.apellido1 ASC, c.apellido2 ASC, c.nombre ASC 
```

--CONSULTA #4
```postgresql
SELECT *
FROM comercial c LEFT JOIN pedido p ON c.id = p.id_comercial
WHERE p.id_comercial IS NULL
ORDER BY c.apellido1 ASC, c.apellido2 ASC, c.nombre ASC
```
--CONSULTA #5 
```postgresql
SELECT c.nombre || ' ' || c.apellido1 || ' '|| c.apellido2 
AS "Resultado"
FROM cliente c LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE p.id_cliente IS NULL
UNION
SELECT co.nombre || ' '|| co.apellido1 || ' ' || co.apellido2 AS "Comercial"
FROM pedido a RIGHT JOIN comercial co ON co.id = a.id_comercial
WHERE a.id_comercial IS NULL
```

-- CONSULTA #6
--
/*
No es posible utilizar NATURAL LEFT JOIN o NATURAL RIGHT JOIN por la diferencia de nombres de los campos.
En la tabla Comercial, su Id se llama "Id", y en la tabla Pedido, el campo que es "Id_Comercial".
También, en la tabla Cliente su PK se llama "Id", mientras que en Pedido, el campo se llama "Id_Cliente".
*/ 

### CONSULTAS RESÚMEN
--CONSULTA #1
```postgresql
SELECT SUM(total) AS "Total"
FROM pedido 
```

--CONSULTA #2

```postgresql
SELECT AVG(p.total) AS "Promedio"
FROM pedido p
```

--CONSULTA #3
```postgresql
SELECT COUNT(DISTINCT p.id_comercial) AS "Comerciales distintos"
FROM pedido p 
```

--CONSULTA #4
```postgresql
SELECT COUNT(*) AS "Cantidad de Clientes"
FROM cliente c
```

--CONSULTA #5
```postgresql
SELECT MAX(p.total) AS "Mayor cantidad"
FROM pedido p
```

--CONSULTA #6
```postgresql
SELECT MIN(p.total) AS "Menor cantidad"
FROM pedido p
```
--CONSULTA #7
```postgresql
SELECT ciudad, MAX(cliente.categoria) 
FROM cliente 
GROUP BY ciudad
```
--CONSULTA #8 
```postgresql
SELECT c.id, c.nombre, c.apellido1, c.apellido2, p.fecha, MAX(p.total) AS "Máximo valor"
FROM cliente c
INNER JOIN pedido p ON p.id_cliente = c.id
WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31'
GROUP BY c.id, p.fecha;
```

--CONSULTA #9
```postgresql
SELECT p.fecha, MAX(p.total) AS "Valor"
FROM pedido p
INNER JOIN cliente c ON c.id = p.id_cliente
WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31'
GROUP BY p.fecha
HAVING MAX(p.total) > 2000;
```

--CONSULTA #10
```postgresql
SELECT c.id, c.nombre, c.apellido1, c.apellido2, MAX(p.total) AS "Total"
FROM comercial c INNER JOIN pedido p ON p.id_comercial = c.id
WHERE p.fecha = '2016-08-17'
GROUP BY c.id
```

--CONSULTA #11
```postgresql
SELECT c.id, c.nombre, c.apellido1, c.apellido2, COUNT(p.id) AS "Cantidad de pedidos"
FROM cliente c LEFT JOIN pedido p ON c.id = p.id_cliente
GROUP BY c.id
```

--CONSULTA #12
```postgresql
SELECT c.id, c.nombre, c.apellido1, c.apellido2, COUNT(p.id_cliente) AS "Cantidad de pedidos"
FROM pedido p INNER JOIN cliente c ON c.id = p.id_cliente
WHERE p.fecha BETWEEN '2017-01-01' AND '2017-12-31'
GROUP BY c.id
```

--CONSULTA #13 
```postgresql
SELECT c.id, c.nombre, c.apellido1, COALESCE(MAX(p.total), 0) AS "Valor"
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
GROUP BY c.id;
```

--CONSULTA #14 
```postgresql
SELECT p.fecha, MAX(p.total) AS "Total"
FROM pedido p
GROUP BY p.fecha;
```

--CONSULTA #15
```postgresql
SELECT fecha, COUNT(*) AS "Cantidad de pedidos"
FROM pedido 
GROUP BY fecha
```

### CONSULTAS SUBCONSULTAS
--CONSULTA #1
```postgresql
SELECT * 
FROM pedido p
WHERE p.id_cliente = (SELECT c.id 
FROM cliente c
WHERE c.nombre = 'Adela' AND c.apellido1 = 'Salas' AND c.apellido2 = 'Díaz')
```

--CONSULTA #2
```postgresql
SELECT COUNT(*) AS "Pedidos de Daniel Sáez Vega"
FROM pedido p 
WHERE p.id_comercial = (SELECT c.id
FROM comercial c
WHERE c.nombre = 'Daniel' AND c.apellido1 = 'Sáez' AND c.apellido2 = 'Vega')
```

--CONSULTA #3 --PENDIENTE
 ```postgresql
SELECT c.nombre, c.apellido1, c.apellido2, c.ciudad
FROM pedido p, cliente c
WHERE p.id_cliente = c.id AND p.total = (SELECT MAX(p.total)
FROM pedido p
 WHERE YEAR(p.fecha) = '2019')
 ```

--CONSULTA #4
```postgresql
SELECT p.fecha, MIN(p.total)
FROM pedido p
WHERE p.id_cliente = (SELECT c.id
FROM cliente c
WHERE c.nombre = 'Pepe' AND c.apellido1 = 'Ruiz' AND c.apellido2 = 'Santana')
```

--CONSULTA #5 
```postgresql
SELECT * FROM cliente AS c
JOIN pedido AS p ON (c.id = p.id_cliente)
WHERE EXTRACT(YEAR FROM fecha) = 2017 AND p.total >= (
    SELECT AVG(total) FROM pedido WHERE EXTRACT(YEAR FROM fecha) = 2017
);
```

### CONSULTA ALL Y ANY
--CONSULTA #1
```postgresql
SELECT *
FROM pedido p 
WHERE p.total >= ALL(SELECT MAX(p.total)
FROM pedido p)
```

--CONSULTA #2
```postgresql
SELECT c.nombre, c.apellido1, c.apellido2
FROM cliente c
WHERE c.id <> ALL(SELECT DISTINCT p.id_cliente FROM pedido p)
```

--CONSULTA #3
```postgresql
SELECT c.nombre, c.apellido1, c.apellido2
FROM comercial c
WHERE c.id <> ALL(SELECT DISTINCT p.id_comercial FROM pedido p)
```

### CONSULTA CON IN Y NOT IN
--CONSULTA #1
```postgresql
SELECT c.nombre, c.apellido1, c.apellido2
FROM cliente c
WHERE c.id NOT IN (SELECT DISTINCT p.id_cliente
                   FROM pedido p)
```

--CONSULTA #2
```postgresql
SELECT c.nombre, c.apellido1, c.apellido2
FROM comercial c
WHERE c.id NOT IN (SELECT DISTINCT p.id_comercial
                   FROM pedido p)
```

### CONSULTA CON EXISTS Y NO EXISTS
--CONSULTA #1
```postgresql
SELECT *
FROM cliente c
WHERE NOT EXISTS (SELECT p.id_cliente 
FROM pedido p
WHERE c.id = p.id_cliente)
```

--CONSULTA #2
```postgresql
SELECT *
FROM comercial c
WHERE NOT EXISTS (SELECT p.id_cliente
FROM pedido p
WHERE c.id = p.id_comercial)
```
