

## Nivel Básico

**1. En la tabla ALUMNADO, ¿cuál es la clave primaria?**  
- [ ] nombre  
- [ ] PK_alumno  
- [ ] FK_curso  

**2. ¿Qué significa FK_curso en la tabla ALUMNADO?**  
- [ ] Es el nombre del curso  
- [ ] Es un identificador que apunta a un curso en la tabla CURSOS  
- [ ] Es el número de alumnos del curso  

**3. ¿En qué edificio estudia Ana?** (Usa ambas tablas)

*Busca a Ana en ALUMNADO → FK_curso → Busca en CURSOS → ubicacion*

- [ ] Edificio B
- [ ] Edificio C
- [ ] No se puede saber

**4. ¿Puedo añadir un alumno en el curso con FK_curso = "CU999" si CU999 todavía no existe en CURSOS?**
- [ ] Sí, sin problema
- [ ] No, la BD rechazará la inserción por integridad referencial
- [ ] Sí, pero con un aviso

---

## Nivel Intermedio

**5. ¿Por qué es mejor tener dos tablas (ALUMNADO + CURSOS) que una sola tabla con todos los datos?**

> Respuesta esperada: Evita redundancia, permite cambiar datos del curso en un solo lugar, podemos registrar cursos sin alumnos, mayor consistencia de datos.

**6. ¿Cuál es la relación entre CURSOS y ALUMNADO?**  
- [ ] Uno a uno (1:1)  
- [ ] Uno a muchos (1:N)  
- [ ] Muchos a muchos (M:N)  

Justifica: ___

**7. Si cambias el aula de 2ºBAC de A205 a A300, ¿cuántas filas tienes que modificar?**  
- [ ] 1 fila (en CURSOS)  
- [ ] 3 filas (Ana, Luis y Marcos en ALUMNADO)  
- [ ] Depende del número de alumnos  

¿Y por qué?

---

## Nivel Avanzado

**8. Si intentásemos eliminar el curso CU06 (2ºBAC) de la tabla CURSOS:**

```sql
DELETE FROM CURSOS WHERE PK_curso = 'CU06';
```

¿Qué debería pasar? ¿Por qué?

> Respuesta esperada: La BD debería rechazar la eliminación porque existen alumnos (Ana, Luis, Marcos) que todavía referencian CU06 a través de FK_curso. Esto previene la pérdida de datos.

**9. ¿Se puede insertar un curso nuevo sin alumnos?**

```sql
INSERT INTO CURSOS (PK_curso, nombre_curso, aula, ubicacion)
VALUES ('CU07', '1ºESO', 'A007', 'Ala A');
```

¿Por qué sí?

> Respuesta esperada: Sí, porque no hay restricción que oblige a un curso a tener alumnos. La FK está en ALUMNADO (tabla dependiente), no en CURSOS (tabla principal).

**10. Compara la Opción 1 (curso en ALUMNADO) con la Opción 2 (tabla CURSOS separada):**

| Aspecto | Opción 1 | Opción 2 |
|---------|----------|----------|
| Redundancia | _____ | _____ |
| Facilidad de actualización | _____ | _____ |
| Inserción de cursos sin alumnos | _____ | _____ |
| Consistencia | _____ | _____ |

---