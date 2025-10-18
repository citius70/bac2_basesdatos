
# Funciones de agregación

Las funciones de agregación en SQL permiten **realizar cálculos** sobre un conjunto de valores y **devolver un solo resultado resumido**. Ayudan a realizar **análisis de datos** y a obtener **resúmenes** útiles, siendo esenciales en informes y procesos de toma de decisiones.

Estas funciones se usan frecuentemente junto con la cláusula `GROUP BY` para agrupar los datos y obtener resultados por categorías o grupos.

## Principales funciones de agregación

| Función        | Descripción                                                               | Ejemplo                                              |
|----------------|---------------------------------------------------------------------------|------------------------------------------------------|
| `COUNT`        | Devuelve el número total de filas (o valores no nulos de una columna)      | `SELECT COUNT(*) FROM clientes;`                     |
| `SUM`          | Calcula la suma total de los valores de una columna numérica               | `SELECT SUM(salario) FROM empleados;`                |
| `AVG`          | Devuelve la media o promedio de los valores de una columna numérica        | `SELECT AVG(edad) FROM alumnos;`                     |
| `MIN`          | Obtiene el valor mínimo de una columna                                    | `SELECT MIN(precio) FROM productos;`                 |
| `MAX`          | Obtiene el valor máximo de una columna                                    | `SELECT MAX(fecha_compra) FROM ventas;`              |

Algunos sistemas gestores de bases de datos añaden otras funciones como `STDDEV` (desviación estándar), `VARIANCE` (varianza), `MEDIAN` (mediana) y funciones para contar valores distintos.

## Uso habitual con `GROUP BY`

Por ejemplo, para obtener el total de ventas por producto:

```sql
SELECT producto, 
    SUM(cantidad) FROM ventas GROUP BY producto;
```

## Ejemplo

Aquí tienes un ejemplo de tabla llamada `ventas` que puede ser utilizada para la consulta:

| id_venta | producto      | cantidad |
|----|--------------|----------|
| VT01  | Lápiz        | 10       |
| VT02  | Bolígrafo    | 5        |
| VT03  | Lápiz        | 7        |
| VT04  | Cuaderno     | 3        |
| VT05  | Bolígrafo    | 8        |
| VT06  | Lápiz        | 6        |
| VT07  | Cuaderno     | 4        |
| VT08  | Bolígrafo    | 2        |


```sql
SELECT producto, 
    SUM(cantidad)
FROM ventas
GROUP BY producto;
```

**Resultado**

| producto | SUM(cantidad) |
| -------- | ------------- |
| Teclado  | 50            |
| Ratón    | 32            |
| Monitor  | 12            |


En SQL puedes **cambiar el nombre de una columna en el resultado de una consulta** usando un **alias**, con la palabra clave `AS` (aunque en MySQL es opcional).

```sql
SELECT producto, 
       SUM(cantidad) AS total_vendido
FROM ventas
GROUP BY producto;
```

---

**Resultado**

| producto | **total_vendido** |
| -------- | ------------- |
| Teclado  | 50            |
| Ratón    | 32            |
| Monitor  | 12            |

