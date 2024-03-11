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


### Consultas

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

6. Consulta 1

   ```postgresql
    SELECT * FROM pedido 
    ORDER BY fecha DESC;
   ```

7. Consulta 1

   ```postgresql
    SELECT * FROM pedido 
    ORDER BY fecha DESC;
   ```

8. Consulta 1

   ```postgresql
    SELECT * FROM pedido 
    ORDER BY fecha DESC;
   ```

9. Consulta 1

   ```postgresql
    SELECT * FROM pedido 
    ORDER BY fecha DESC;
   ```

10. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

11. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

12. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

13. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

14. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

15. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

16. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

17. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

18. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

19. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

20. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

21. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

22. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

23. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

24. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

25. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

26. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

27. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

28. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

29. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

30. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

31. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

32. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

33. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

34. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

35. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

36. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

37. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

38. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

39. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

40. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

41. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

42. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

43. Consulta 1

    ```postgresql
     SELECT * FROM pedido 
     ORDER BY fecha DESC;
    ```

44. 
