# Ejercicio: conceptos básicos

### Ejercicio: Identificación de claves primaria y foránea

Se presentan dos tablas relacionadas con un equipo de fútbol y jugados:

#### Tabla "Jugadores"

| id_jugador | nombre        | posición       | id_equipo |
|------------|--------------|----------------|-----------|
| 1          | Javier Pérez | Delantero      | 201       |
| 2          | Sergio Díaz  | Portero        | 202       |
| 3          | Marcos Ruiz  | Defensa        | 201       |
| 4          | Luis Gómez   | Centrocampista | 203       |

#### Tabla "Equipos"

| id_equipo | nombre_equipo        | ciudad      |
|-----------|----------------------|-------------|
| 201       | Club Deportivo Roma  | Madrid      |
| 202       | Atlético Sur         | Sevilla     |
| 203       | Unión Norte          | Valencia    |
| 204       | Fútbol Club Este     | Barcelona   |

***

**Responde a las siguientes preguntas:**

1. ¿Cuál debería ser la clave primaria (PK) en la tabla "Jugadores"?  
   - ( ) nombre  
   - ( ) id_jugador  
   - ( ) id_equipo  

2. ¿Cuál debería ser la clave primaria (PK) en la tabla "Equipos"?  
   - ( ) ciudad  
   - ( ) nombre_equipo  
   - ( ) id_equipo  

3. ¿Qué campo en la tabla "Jugadores" sirve como clave foránea (FK) para relacionarla con la tabla "Equipos"?  
   - ( ) nombre_equipo  
   - ( ) id_equipo  
   - ( ) posición  
  
4. ¿En qué ciudad juega Sergio Díaz?

   - ( ) Madrid
   - ( ) Sevilla
   - ( ) Valencia

***

Marca la opción correcta en cada pregunta y justifica brevemente tus respuestas.
