# sql-select-fundamentals

Consultas SQL básicas de exploración y selección de columnas, resueltas sobre la tabla `sales` de TechStore. Es un ejercicio práctico del curso de Data Analytics, enfocado en algo simple pero clave: cómo mostrar los datos según quién los va a leer.

## ¿Por qué es mala práctica usar `SELECT *` en producción?

Porque trae todas las columnas de la tabla, se usen o no, y eso trae dos problemas.

El primero es de rendimiento. Acá la tabla `sales` tiene 9 columnas nada más, pero pensemos en un caso real con 40, algunas con textos largos o datos pesados. Si un reporte solo necesita 3 y de todos modos usa `SELECT *`, la base tiene que leer y mover las otras 37 igual, sin que sirvan para nada. Es trabajo de más para la base y tiempo de más esperando el resultado.

El segundo tiene que ver con la seguridad y con lo fácil o difícil que sea mantener el código después. `SELECT *` no dice qué información estás usando realmente. Si mañana alguien agrega una columna nueva a la tabla, por ejemplo algo sensible como un número de tarjeta, cualquier consulta vieja con `SELECT *` la va a empezar a traer sola, sin que nadie lo haya pedido ni se dé cuenta. Eligiendo las columnas a mano, en cambio, cualquiera que lea la consulta sabe exactamente qué datos entran en juego.

Ahora, hay un momento donde `SELECT *` sí tiene sentido: cuando estás abriendo una tabla por primera vez y todavía no sabés qué tiene adentro (es lo que hice en la Consulta 1 de este ejercicio, para explorar `sales`). Una vez que ya la conocés, no hay motivo para seguir pidiendo todo.

## ¿Por qué son importantes los alias para un stakeholder no técnico?

Porque las columnas de una base de datos suelen tener nombres pensados para el sistema, no para la persona que va a leer el reporte. `total_amount` está en inglés y con un formato técnico; alguien de finanzas que nunca abrió una base de datos tiene que pararse a pensar qué significa, o directamente preguntar.

Si en cambio esa misma columna se renombra con `AS` a `monto_total`, ya no hace falta explicar nada: se entiende sola. Es como cuando te llega un Excel con una columna `emp_id` versus otro con `id_empleado` — el dato es el mismo, pero solo uno lo entendés de una.

Para mí ese es justamente el trabajo del analista: traducir el lenguaje técnico de la base al lenguaje que entiende quien va a usar el reporte, para que no tenga que volver a preguntarme cada vez qué significa cada columna.
