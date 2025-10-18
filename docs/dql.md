# Comandos DQL (Data Query Language)

Los comandos DQL sirven para **consultar** y **extraer** datos. El más importante es `SELECT` y `SELECT DISTINCT`, que admiten varias cláusulas y opciones para refinar los resultados.

## `SELECT`   
```sql
SELECT columna1, columna2, …
FROM tabla;
```
Permite consultar y mostrar la información concreta de ciertas columnas de una tabla en una base de datos relacional.

**Explicación formal**

* `SELECT` indica qué columnas mostrar en el resultado.

* Se listan una o varias columnas separadas por comas (por ejemplo: nombre, correo).

* `FROM` especifica de qué tabla se extraen los datos.

* La consulta devuelve todas las filas de las columnas indicadas, a menos que se limite con una cláusula adicional como `WHERE`.​

**Ejemplo práctico**

Dada una **tabla: clientes** con las **columnas: nombre, correo y teléfono**, 

| id | nombre   | apellidos        | correo                | teléfono    |
|----|----------|------------------|-----------------------|-------------|
| 1  | Luis     | López García     | luis1@email.com       | 666111222   |
| 2  | Ana      | Ruiz Fernández   | ana@email.com         | 666333444   |
| 3  | Luis     | Martínez Pérez   | luis2@email.com       | 666555666   |
| 4  | Marta    | Sánchez Torres   | marta@email.com       | 666777888   |
| 5  | Juan     | Gómez Ramírez    | juan@email.com        | 666999000   |

Si se quiere ver solo los nombres y correos de todos los clientes, la consulta sería:

```sql
SELECT nombre, correo
FROM clientes;
```

El resultado mostrará una lista con el nombre y el correo electrónico de **todos los clientes** almacenado en la tabla.

| id | nombre   | correo                |
|----|----------|-----------------------|
| 1  | Luis     | luis1@email.com       |
| 2  | Ana      | ana@email.com         |
| 3  | Luis     | luis2@email.com       |
| 4  | Marta    | marta@email.com       |
| 5  | Juan     | juan@email.com        |

> ¿Sabrías explicar qué consulta obtendríamos añadiendo la opción `WHERE`?

```sql
SELECT id, nombre, apellidos, correo, teléfono
FROM clientes
WHERE nombre = 'Luis';
```

| id | nombre   | apellidos        | correo                | teléfono    |
|----|----------|------------------|----------------------|-------------|
| 1  | Luis     | López García     | luis1@email.com       | 666111222   |
| 3  | Luis     | Martínez Pérez   | luis2@email.com       | 666555666   |

## `SELECT DISTINCT` 

La instrucción `SELECT DISTINCT` en SQL se utiliza para obtener sólo los valores únicos de una o varias columnas en el resultado de una consulta, eliminando cualquier fila duplicada que pueda existir en esos campos.

**Ejemplo de sintaxis general:**

```sql
SELECT DISTINCT columna1, columna2
FROM tabla;
```
Esta consulta mostrará sólo las combinaciones únicas de valores de columna1 y columna2, retirando los duplicados.

### Ejemplo práctico

Supón la siguiente tabla: **clientes**:

| nombre   | ciudad    |
|----------|-----------|
| Ana      | Sevilla   |
| Luis     | Madrid    |
| Marta    | Sevilla   |
| Mabel    | Valencia  |
| Pedro    | Madrid    |

Si se ejecuta la consulta:

```sql
SELECT DISTINCT ciudad
FROM clientes;
```
El resultado será:

| ciudad   |
|----------|
| Sevilla  |
| Madrid   |
| Valencia |

Así, aunque Madrid y Sevilla aparecen más de una vez, en el resultado de la consulta sólo figuran una vez cada ciudad, sin duplicados.