# Opciones y cláusulas de SELECT

La instrucción `SELECT` en SQL dispone de varias **opciones y cláusulas** que permiten personalizar y afinar la consulta de datos en una base de datos relacional. A continuación se enumeran las más importantes, con su descripción formal y su uso típico. Veámoslo con un ejemplo:


```sql
SELECT nombre, apellidos, ciudad, edad
FROM clientes
WHERE edad >= 18 AND ciudad = 'Sevilla'
ORDER BY nombre ASC
LIMIT 2;
```

Como es de suponer, no es necesario utilizar todas las opciones si no son necesarias.

| Cláusula       | Descripción                                                  | Ejemplo breve                                 |
|----------------|--------------------------------------------------------------|-----------------------------------------------|
| SELECT         | Especifica las columnas (o expresiones) que devolverá la consulta | `SELECT nombre, apellidos, ciudad, edad `                         |
| **FROM**           | Indica la tabla o tablas de las que se extraen los datos      | `FROM clientes`                               |
| **WHERE**          | Permite filtrar los registros que cumplen ciertas condiciones | `WHERE edad > 18 AND ciudad = 'Sevilla'`                             |
| GROUP BY       | Agrupa los registros según valores de una o más columnas     |                              |
| HAVING         | Filtra los grupos generados por GROUP BY según una condición | `                         |
| **ORDER BY**       | Ordena el resultado según una o varias columnas              | `ORDER BY nombre ASC`                       |
| **LIMIT** / **TOP**    | Restringe el número de registros devueltos                   | `LIMIT 2` o `SELECT TOP 5`                   |

## Ejemplo completo

Aquí tienes una tabla de ejemplo con datos representativos para explicar el uso de las cláusulas principales de SELECT:

| id | nombre   | apellidos         | correo                | ciudad     | edad |
|----|----------|-------------------|-----------------------|------------|------|
| 1  | Luis     | López García      | luis1@email.com       | Sevilla    | 19   |
| 2  | Ana      | Ruiz Fernández    | ana@email.com         | Sevilla    | 17   |
| 3  | Luis     | Martínez Pérez    | luis2@email.com       | Madrid     | 18   |
| 4  | Marta    | Sánchez Torres    | marta@email.com       | Valencia   | 17   |
| 5  | Juan     | Gómez Ramírez     | juan@email.com        | Madrid     | 21   |
| 6  | Pedro    | Alonso Vidal      | pedro@email.com       | Sevilla    | 19   |
| 7  | Clara    | Peña Morales      | clara@email.com       | Valencia   | 21   |
| 8  | Sergio   | Fernández Moya    | sergio@email.com      | Sevilla    | 22   |
| 9  | Laura    | Jiménez Rosado    | laura@email.com       | Valencia   | 17   |
| 10 | Raúl     | Montes Acosta     | raul@email.com        | Madrid     | 19   |

La consulta es:


```sql
SELECT nombre, apellidos, ciudad, edad
FROM clientes
WHERE edad >= 18 AND ciudad = 'Sevilla'
ORDER BY nombre ASC
LIMIT 2;
```
**Análisis de la consulta:**

Esta consulta SQL busca clientes sevillanos mayores de edad y los ordena alfabéticamente.

**Desglose de la consulta:**

- **`SELECT nombre, apellidos, ciudad, edad`**: Selecciona estos 4 campos
- **`FROM clientes`**: De la tabla clientes
- **`WHERE edad >= 18 AND ciudad = 'Sevilla'`**: Filtra clientes mayores de edad (≥18) que vivan en Sevilla
- **`ORDER BY nombre ASC`**: Ordena por nombre de forma ascendente (A-Z)
- **`LIMIT 2`**: Solo muestra los 2 primeros resultados

---

**Aplicando a tus datos:**

**Clientes que cumplen `edad >= 18 AND ciudad = 'Sevilla'`:**

| id | nombre | apellidos       | ciudad  | edad |
|----|--------|-----------------|---------|------|
| 1  | Luis   | López García    | Sevilla | 19   |
| 6  | Pedro  | Alonso Vidal    | Sevilla | 19   |
| 8  | Sergio | Fernández Moya  | Sevilla | 22   |

**Ordenados por nombre (ASC):**
1. **Luis** López García
2. **Pedro** Alonso Vidal  
3. **Sergio** Fernández Moya

**Aplicando `LIMIT 2`:**
Solo muestra los 2 primeros.

---

**Resultado final:**


nombre | apellidos       | ciudad  | edad
-------|-----------------|---------|------
Luis   | López García    | Sevilla | 19
Pedro  | Alonso Vidal    | Sevilla | 19

**Nota:** Sergio Fernández no aparece en el resultado debido al `LIMIT 2`, a pesar de cumplir todas las condiciones.
