# MySQL vs SQLite

## ¿Qué son y para qué sirven?

Tanto **MySQL** como **SQLite** son sistemas gestores de bases de datos relacionales (SGBD) que usan el lenguaje **SQL** para crear tablas, insertar datos y hacer consultas. Sin embargo, están pensados para situaciones muy distintas.

| | MySQL | SQLite |
|---|---|---|
| **Tipo** | Sistema cliente-servidor | Biblioteca embebida |
| **Instalación** | Requiere servidor y configuración | Un solo archivo, sin instalación |
| **Uso típico** | Aplicaciones web, empresas | Apps móviles, prototipos, aprendizaje |
| **Ejemplos reales** | WordPress, Twitter, Airbnb | Android, iOS, Firefox, WhatsApp |

---

## Lo que tienen en común ✅

Estos conceptos funcionan **igual** en los dos sistemas. Todo lo que aprendas aquí te sirve para ambos:

- **Lenguaje SQL:** `SELECT`, `FROM`, `WHERE`, `JOIN`, `INSERT`, `CREATE TABLE`...
- **Claves primarias (PK) y foráneas (FK)**
- **Tipos de relaciones:** 1:1, 1:N, M:N
- **Normalización de tablas**
- **Integridad referencial** (`FOREIGN KEY ... REFERENCES`)
- **Operadores:** `=`, `>`, `<`, `LIKE`, `BETWEEN`, `AND`, `OR`
- **Funciones de agregación:** `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`
- **Agrupaciones:** `GROUP BY`
- **Uniones:** `JOIN`, `LEFT JOIN`

> 💡 **Conclusión:** el 90% de lo que escribes en SQL es idéntico en ambos sistemas. Las diferencias están en los detalles de configuración y algunos tipos de datos.

---

## Las diferencias clave ⚠️

### 1. Tipos de datos

Esta es la diferencia más importante para los ejercicios en clase.

| Concepto | MySQL | SQLite |
|---|---|---|
| Texto corto | `VARCHAR(50)` | `TEXT` |
| Texto largo | `TEXT` | `TEXT` |
| Número entero | `INT` | `INTEGER` |
| Número decimal | `FLOAT` o `DECIMAL` | `REAL` |
| Fecha | `DATE` | `TEXT` (formato `AAAA-MM-DD`) |
| Verdadero/Falso | `BOOLEAN` | `INTEGER` (0 = falso, 1 = verdadero) |

> ⚠️ **En SQLite no existe `VARCHAR` ni `BOOLEAN`.** Si los usas, SQLite los acepta sin error pero los convierte internamente a `TEXT` o `INTEGER`. Para evitar confusiones, usa siempre los tipos propios de SQLite.

---

### 2. Autoincremento de la clave primaria

```sql
-- En MySQL:
CREATE TABLE COCINEROS (
    pk_cocinero INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50)
);

-- En SQLite:
CREATE TABLE COCINEROS (
    pk_cocinero INTEGER PRIMARY KEY,
    nombre TEXT
);
```

> 💡 En SQLite basta con escribir `INTEGER PRIMARY KEY` — el autoincremento es automático. No existe la palabra `AUTO_INCREMENT`.

---

### 3. Claves foráneas

En MySQL las claves foráneas funcionan siempre. En SQLite hay que **activarlas** al inicio de la sesión, porque por defecto están desactivadas:

```sql
-- Solo en SQLite — ejecutar antes de cualquier INSERT:
PRAGMA foreign_keys = ON;
```

> ⚠️ Si no ejecutas esta línea en SQLite, podrás insertar registros con claves foráneas que no existen sin que SQLite te avise. En DB Browser, actívalo en **Herramientas → Preferencias → Base de datos → Activar soporte de clave foránea**.

---

### 4. Arquitectura: ¿cómo funciona cada uno?

```
MySQL (cliente-servidor)                SQLite (archivo único)
─────────────────────────               ──────────────────────
  [ Aplicación / Programa ]               [ Aplicación / Programa ]
          │                                        │
          │  petición SQL                          │  llamada directa
          ▼                                        ▼
  [ Servidor MySQL ]                      [ Archivo .db ]
  (proceso separado,                      (en el mismo disco,
   puede estar en otro                     sin servidor)
   ordenador)
```

- **MySQL** necesita un servidor corriendo en segundo plano. Es como un restaurante: hay un cocinero (servidor) que recibe pedidos y los procesa.
- **SQLite** guarda todo en un único archivo `.db`. Es como una fiambrera: tú mismo abres el recipiente y accedes directamente.

---

### 5. Resumen rápido de diferencias

| Característica | MySQL | SQLite |
|---|---|---|
| `AUTO_INCREMENT` | ✅ Sí | ❌ No (usar `INTEGER PRIMARY KEY`) |
| `VARCHAR(n)` | ✅ Sí | ⚠️ Funciona, pero se recomienda `TEXT` |
| `BOOLEAN` | ✅ Sí | ❌ No (usar `INTEGER`: 0/1) |
| `DATE` | ✅ Tipo nativo | ⚠️ Usar `TEXT` en formato `AAAA-MM-DD` |
| FK activas por defecto | ✅ Sí | ❌ No (activar con `PRAGMA foreign_keys = ON`) |
| Servidor necesario | ✅ Sí | ❌ No |
| Archivo único `.db` | ❌ No | ✅ Sí |
| Varios usuarios simultáneos | ✅ Sí | ⚠️ Limitado |
| Ideal para aprender SQL | ✅ Sí | ✅ Sí (más sencillo de instalar) |

---

## Equivalencias directas — tabla de traducción

Cuando veas código MySQL en un tutorial o libro, usa esta tabla para adaptarlo a SQLite:

| Si en MySQL ves... | En SQLite escribe... |
|---|---|
| `INT AUTO_INCREMENT PRIMARY KEY` | `INTEGER PRIMARY KEY` |
| `VARCHAR(50)` | `TEXT` |
| `BOOLEAN` | `INTEGER` |
| `DATE` | `TEXT` |
| `TINYINT(1)` | `INTEGER` |
| `DECIMAL(8,2)` | `REAL` |
| `AUTO_INCREMENT` (solo la palabra) | *(elimínala)* |

---

## Ejemplo comparativo completo

El mismo `CREATE TABLE` escrito para cada sistema:

```sql
-- ✅ MySQL
CREATE TABLE JUGADORES (
    pk_jugador  INT          AUTO_INCREMENT PRIMARY KEY,
    nombre      VARCHAR(50)  NOT NULL,
    fecha_alta  DATE,
    activo      BOOLEAN,
    salario     DECIMAL(8,2),
    fk_equipo   INT,
    FOREIGN KEY (fk_equipo) REFERENCES EQUIPOS(pk_equipo)
);
```

```sql
-- ✅ SQLite
CREATE TABLE JUGADORES (
    pk_jugador  INTEGER  PRIMARY KEY,
    nombre      TEXT     NOT NULL,
    fecha_alta  TEXT,
    activo      INTEGER,
    salario     REAL,
    fk_equipo   INTEGER,
    FOREIGN KEY (fk_equipo) REFERENCES EQUIPOS(pk_equipo)
);
```

> 💡 La estructura es idéntica. Solo cambian los tipos de datos y desaparece `AUTO_INCREMENT`.

---

## ¿Cuándo usar cada uno?

| Situación | Recomendación |
|---|---|
| Aprender SQL por primera vez | ✅ **SQLite** — sin instalación, más sencillo |
| Proyecto personal o prototipo | ✅ **SQLite** |
| App para móvil (Android/iOS) | ✅ **SQLite** |
| Página web con muchos usuarios | ✅ **MySQL** (o PostgreSQL) |
| Empresa con base de datos grande | ✅ **MySQL** |
| Varios programas accediendo a la vez | ✅ **MySQL** |

---

## Para recordar 🧠

1. **El SQL es prácticamente igual** en ambos — lo que aprendes sirve para los dos.
2. En SQLite: **`TEXT`** en vez de `VARCHAR`, **`REAL`** en vez de `FLOAT`, **`INTEGER PRIMARY KEY`** en vez de `INT AUTO_INCREMENT`.
3. En SQLite: las **fechas son texto** (`'2024-03-15'`), no un tipo especial.
4. En SQLite: activar siempre **`PRAGMA foreign_keys = ON`** para que las FK funcionen.
5. SQLite guarda todo en **un archivo `.db`** — fácil de copiar, mover y entregar.

---