# Comandos DML (Data Manipulation Language)

Es lógico abordar ahora los comandos DML, pues permiten **insertar**, **modificar** y **eliminar** datos, y así comprenderás cómo se llena y mantiene la base antes de consultarla.

***

## `INSERT`

El comando `INSERT` sirve para **añadir uno o varios registros** a una tabla existente. A continuación se detallan diferentes formas de usarlo:

La sintaxis general es:

```sql
INSERT INTO nombre_tabla (columna1, columna2, ..., columnaN)
VALUES (valor1, valor2, ..., valorN);
```

- **nombre_tabla**: tabla destino.  
- **(columna1, …, columnaN)**: lista de columnas a rellenar.  
- **VALUES**: palabra clave que inicia la lista de valores.  
- **(valor1, …, valorN)**: valores en el mismo orden que las columnas.  

**Ejemplo para insertar un solo registro:**

```sql
INSERT INTO Jugadores (id_jugador, nombre, posición, id_equipo)
VALUES (5, 'Raúl Torres', 'Delantero', 201);
```

- **Jugadores:** nombre de la tabla.
- **(…):** lista de columnas a rellenar.  
- **VALUES (…):** valores correspondientes, en el mismo orden.

**Ejemplo para insertar múltiples registros a la vez:**

```sql
INSERT INTO Jugadores (id_jugador, nombre, posición, id_equipo)
VALUES
  (6, 'Laura Martínez', 'Centrocampista', 202),
  (7, 'Carlos Vega', 'Defensa', 201),
  (8, 'María López', 'Portero', 203);
```

- Permite optimizar la inserción masiva en una sola operación.


**Consideraciones y buenas prácticas:**

- El orden de los valores en `VALUES` debe coincidir con el de las columnas listadas.  
- Si la tabla tiene **clave primaria auto-incremental**, no incluirla en la lista de columnas:
  ```sql
  INSERT INTO Equipos (nombre_equipo, ciudad)
  VALUES ('Valencia FC', 'Valencia');
  ```
- Verificar restricciones (`NOT NULL`, `UNIQUE`) para evitar errores en tiempo de ejecución.  

***

## `UPDATE` 

El comando `UPDATE` modifica uno o varios campos de registros existentes según una condición.

La sintaxis general:
```sql
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2, …
WHERE condición;
```

Ejemplo:
```sql
UPDATE Equipos
SET ciudad = 'Pontevedra'
WHERE id_equipo = 203;
```

Ampliación:
- **Varias columnas a la vez:**
  ```sql
  UPDATE Equipos
  SET ciudad = 'Cádiz',
      nombre_equipo = 'Atlético Gaditano'
  WHERE id_equipo = 203;
  ```
- **Sin WHERE (¡cuidado!):**  
  Al omitir `WHERE`, se actualizan **todos** los registros de la tabla:
  ```sql
  UPDATE Equipos
  SET ciudad = 'Madrid';
  ```
- **Condiciones complejas:**  
  Usar operadores lógicos para afinar el filtro:
  ```sql
  UPDATE Jugadores
  SET posición = 'Defensa'
  WHERE id_equipo = 201 AND posición = 'Delantero';
  ```
- **Buenas prácticas:**  
  - Siempre comprobar la condición con un `SELECT` previo.  
  - Hacer copia de seguridad si la operación afecta muchos registros.

***

## `DELETE`  

El comando `DELETE` sirve para **eliminar** uno o varios registros de una tabla que cumplan una condición específica.

La sintaxis básica :

```sql
DELETE FROM nombre_tabla
WHERE condición;
```

- **DELETE FROM**: Indica la tabla de la que se van a borrar registros.  
- **WHERE condición**: Filtro que determina qué filas se eliminarán.  

**Ejemplo** 

```sql
DELETE FROM Alumnos
WHERE id = 4;
```
Elimina el registro cuyo campo `id` vale 4 de la tabla Alumnos.

### Variantes y consideraciones

- **Eliminar todos los registros**  
  
  Si se omite la cláusula `WHERE`, se borran **todas** las filas de la tabla:
  ```sql
  DELETE FROM Alumnos;
  ```

- **Condiciones complejas**  
  Se pueden usar operadores lógicos y comparaciones para definir criterios:
  ```sql
  DELETE FROM Jugadores
  WHERE id_equipo = 101 AND posición = 'Delantero';
  ```

- **Buen hábito: SELECT previo**  
  Antes de usar `DELETE`, conviene ejecutar un `SELECT` con la misma condición para verificar qué filas se eliminarán:
  ```sql
  SELECT * FROM Alumnos
  WHERE id = 4;
  ```

- **Transacciones**  
  En sistemas que soportan transacciones, agrupar `DELETE` dentro de una transacción permite deshacerlo si es necesario:
  ```sql
  START TRANSACTION;
  DELETE FROM Alumnos WHERE id = 4;
  ROLLBACK;  -- o COMMIT para confirmar
  ```
Con estas opciones, `DELETE` se utiliza de forma segura y controlada, evitando pérdidas accidentales de datos.

***

## `TRUNCATE`  

El comando `TRUNCATE TABLE` elimina **rápidamente** todo el contenido de una tabla, restableciendo además cualquier contador de auto-incremento, sin registrar la eliminación de cada fila individualmente.

La sintaxis es:

```sql
TRUNCATE TABLE nombre_tabla;
```

**Características principales**

- Borra **todas** las filas de la tabla de forma inmediata.
- Reinicia el contador de valores `AUTO_INCREMENT` a su valor inicial.
- Opera de manera más eficiente que `DELETE` sin `WHERE`, pues no genera registros de transacción por cada fila borrada.
- En la mayoría de motores, no puede usarse con `WHERE` ni en vistas; solo en tablas completas.

**Ejemplo**

```sql
TRUNCATE TABLE Jugadores;
```
Elimina todos los registros de “Jugadores” y deja la estructura vacía, lista para nuevos datos.

**Comparación con DELETE sin WHERE**

| Aspecto                | DELETE FROM tabla; | TRUNCATE TABLE tabla;      |
|------------------------|--------------------|----------------------------|
| Velocidad              | Lenta en tablas grandes | Muy rápida                |
| Registro de transacción| Sí (fila a fila)   | No (solo la operación)     |
| Reinicio AUTO_INCREMENT| No                 | Sí                         |
| Uso de WHERE           | No                 | No                         |

**Buenas prácticas**
- Utilizar `TRUNCATE` cuando se necesite vaciar por completo una tabla en entornos de desarrollo o limpieza de datos masivos.
- Evitar en producción si se requiere auditoría de eliminaciones, ya que no permite recuperar las filas eliminadas a través de transacciones.

***

Comprender DML te permitirá practicar cómo **poblar** y **modificar** las tablas que has creado, antes de aprender las consultas SELECT para extraer la información.