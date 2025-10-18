# Ejercicio: Base de datos para un comercio

https://planetscale.com/blog/schema-design-101-relational-databases

Diseña una **base de datos para un nuevo comercio** en tu ciudad. Este comercio valora mucho la relación con sus clientes y quiere premiar a los clientes que alcancen un objetivo de gasto y regalarles en el aniversario de su primera compra. El comercio también necesita organizar productos por precio y categoría para recomendar mejor los productos según la edad del cliente. Igualmente, quiere seguir el rendimiento de los empleados para premiar con aumentos a los que consigan más ventas al final del año.

## Diseño del esquema de la base de datos

El esquema es la estructura que definimos para nuestros datos. El esquema determina las tablas, las relaciones entre las tablas, los campos y los índices.
El esquema también influye considerablemente en el rendimiento de nuestra base de datos. Dedicar tiempo al diseño del esquema nos ahorrará problemas en el futuro. Una herramienta útil para diseñar nuestro esquema es un diagrama ER (Entidad-Relación). Usaremos Lucidchart para crear nuestro diagrama ER, y puedes darte de alta gratis. Este diagrama permitirá visualizar las entidades y sus relaciones.

Estos son los pasos principales en el diseño del esquema:
1. Entender las necesidades del negocio
2. Identificar entidades
3. Identificar propiedades/campos de esas entidades
4. Definir las relaciones entre las tablas

Paso 1: Entender las necesidades del negocio
El primer paso para diseñar el esquema de una base de datos relacional es comprender las necesidades del negocio. Esto nos ayudará a determinar qué información debemos almacenar. Por ejemplo, si trabajamos con un comercio que quiere ofrecer un regalo de aniversario a sus clientes, necesitaremos guardar la fecha en que el cliente se unió.

Resumen de los requisitos para los clientes:
- Guardar el gasto acumulado del cliente
- Guardar la fecha de aniversario de la primera compra
- Guardar la edad del cliente
- Guardar el total de ventas hechas por el empleado (en dinero)
- Guardar los productos, incluyendo categoría y precio

Paso 2: Definir entidades o tablas
Una vez claro lo anterior, el siguiente paso es definir las entidades sobre las que queremos guardar datos. Estas entidades serán nuestras tablas. Siguiendo el ejemplo del comercio, nuestras entidades deberían ser:
- clientes
- productos
- pedidos
- empleados

Podríamos añadir más entidades como tiendas si hay varias sedes, fabricantes, etc., según las necesidades del negocio. Para este ejemplo trabajamos solo con las cuatro entidades para cubrir las necesidades del comercio ficticio. En el diagrama ER se representa cada entidad con un rectángulo y el nombre de la tabla en la parte superior.

Paso 3: Definir propiedades o campos
Después de identificar las entidades, debemos definir los campos que vamos a almacenar sobre cada entidad. Es importante que cada tabla o entidad tenga una propiedad única que la identifique. Ese valor único es la clave primaria y permite diferenciar los registros entre sí. Por ejemplo, si tenemos dos clientes con el mismo nombre o la misma fecha de nacimiento, la clave primaria indica de cuál se trata.

Dos formas típicas de crear una clave primaria:
- Generar el valor único de forma programática
- Asignar un número entero que se incrementa automáticamente con cada nuevo registro

Todo esto se extrae fácilmente de las especificaciones que nos da el negocio. Por ejemplo, el comercio necesita saber qué cliente realizó la compra, qué empleado realizó la venta y qué productos se incluyeron en el pedido. En la tabla pedidos verás que se tiene un campo customerID, employeeID y productID para cumplir con esas necesidades.

Paso 4: Definir relaciones
Una vez definidas las entidades y sus propiedades, hay que pensar cómo se relacionan las tablas entre sí. El fundamento de las bases de datos relacionales es que las tablas se relacionan. Una tabla “padre” tendrá una columna que sirva de clave primaria, y una tabla “hija” tendrá su propia clave primaria y una columna parent_id que referencia a la tabla padre. Ya hicimos esto al definir los campos en el paso anterior. Por ejemplo, la tabla clientes tiene su customerID como clave primaria. En la tabla pedidos hay un campo orderID como clave primaria y se referencia el customerID para saber qué cliente hizo el pedido. De igual forma, hay un campo que referencia employees, employeeID, para saber qué empleado realizó la venta.

Cuando una clave primaria aparece en otra tabla, ese campo se llama clave foránea en esa tabla. La relación entre clave primaria y clave foránea es lo que crea la relación entre tablas.

¡Ya tienes el esquema!
Hemos repasado los pasos fundamentales para el diseño de un esquema de base de datos: entender las necesidades del negocio, definir las entidades, definir los campos y definir las relaciones. El diseño del esquema puede dar miedo porque, en las bases relacionales tradicionales, algunos cambios de esquema pueden provocar problemas graves e incluso pérdida de datos. Con la función de ramificación (branching) de PlanetScale, puedes crear ramas de tu esquema igual que con el código. Prueba cambios de esquema en un entorno aislado y, cuando estés satisfecho, puedes fusionar tu rama de cambios con la rama principal de producción sin sufrir interrupciones ni pérdida de datos.]

¿Qué es una base de datos relacional?
Una base de datos relacional es una manera de almacenar datos que están relacionados entre sí de forma predefinida. Por “predefinida” se entiende que, al crear la base, puedes identificar las relaciones que existen entre diferentes entidades o grupos de datos. Las bases relacionales son ideales para almacenar datos estructurados que modelan relaciones entre entidades del mundo real.

La anatomía de una base de datos relacional:
- Tablas: Datos de una entidad, organizados en columnas y filas.
- Propiedades: Atributos que queremos guardar sobre una entidad.
- Relaciones: Las conexiones entre las tablas.
- Índices: Útiles para conectar tablas y agilizar consultas.

Una base relacional está compuesta por dos o más tablas con distintas filas y columnas. Cada tabla representa una entidad específica. Cada columna corresponde a una propiedad de cada registro (fila) de la tabla. Para ilustrar el funcionamiento de una base relacional, se diseña una base para un comercio que gestiona productos, clientes, pedidos y empleados.

Diseño de una base de datos para un nuevo comercio
El comercio valora mucho la relación con sus clientes y quiere premiar a los que alcanzan un objetivo de gasto con un regalo en el aniversario de su primera compra. Además, necesita organizar productos por precio y categoría para recomendar los mejores productos en función de la edad del cliente. También desea seguir el rendimiento de los empleados para recompensar a los que tengan más ventas con un aumento anual.

Diseño del esquema de la base de datos
El esquema es la estructura que definimos para los datos: determina tablas, relaciones entre ellas, campos e índices.
El esquema afecta mucho al rendimiento de la base. Dedicar tiempo a su diseño evita problemas futuros. Es útil crear un diagrama ERD (Entidad-Relación), por ejemplo con Lucidchart, que se puede usar gratis. Este diagrama permite visualizar entidades y relaciones.

Pasos principales para diseñar el esquema:
- Entender las necesidades del negocio
- Identificar entidades (tablas)
- Identificar propiedades/campos de cada entidad
- Definir las relaciones entre las tablas

Paso 1: Entender las necesidades del negocio
El primer paso es comprender qué requiere el negocio: así determinamos qué información almacenar. Por ejemplo, si el comercio quiere regalar algo en el aniversario de un cliente, hay que guardar la fecha en que se unió.

Resumen de requisitos para los clientes:
- Guardar el gasto acumulado
- Guardar la fecha de aniversario de la primera compra
- Guardar la edad del cliente
- Guardar el total de ventas del empleado (en dinero)
- Guardar productos, indicando categoría y precio

Paso 2: Definir entidades (tablas)
Tras esto, definimos las entidades a almacenar. Éstas serán nuestras tablas. En el ejemplo del comercio serían:
- clientes
- productos
- pedidos
- empleados

Podrían añadirse más entidades como tiendas, fabricantes, etc., según el negocio. En este ejemplo se emplean solo estas cuatro. En el diagrama ERD, cada entidad es un rectángulo que muestra el nombre de la tabla.

Paso 3: Definir propiedades (campos)
Para cada entidad, se definen los campos a almacenar. Cada tabla debe tener un campo único que identifique el registro: la clave primaria. Esto distingue registros y evita confusiones cuando hay datos repetidos.

Dos formas habituales de crear la clave primaria:
- Generar un valor único programáticamente
- Asignar un entero que aumenta automáticamente

Esto se deduce directamente de lo que pide el negocio. Por ejemplo, conviene saber qué cliente hizo la compra, qué empleado la gestionó y qué productos incluyó el pedido. En la tabla pedidos aparecen customerID, employeeID y productID para satisfacer estos requisitos.

Paso 4: Definir relaciones
Con entidades y campos definidos, se analiza cómo se relacionan las tablas. El núcleo de las bases relacionales es la relación entre tablas. Una tabla "padre" tendrá una clave primaria; la tabla "hija" tendrá su clave primaria y un campo parent_id que referencia a la tabla padre. Esto ya se introdujo en el paso anterior. Por ejemplo, la tabla clientes tiene customerID como clave primaria; en pedidos hay orderID (clave primaria), y un customerID que indica quién hizo el pedido. También hay un campo referenciando employees, employeeID, para saber qué empleado hizo la venta.

Cuando una clave primaria aparece en otra tabla, ese campo es clave foránea. La relación entre claves primarias y foráneas crea la relación entre tablas.

¡Has terminado!
Estos son los pasos fundamentales para diseñar tu esquema: entender el negocio, definir entidades, campos y relaciones. El diseño del esquema puede asustar porque, en bases relacionales tradicionales, algunos cambios pueden provocar problemas graves e incluso pérdida de datos. Con el “branching” de PlanetScale puedes crear ramas del esquema como ocurre con el código: prueba cambios en un entorno aislado y, si te convencen, fusiónalos con la rama principal sin interrupciones ni pérdidas de datos.]