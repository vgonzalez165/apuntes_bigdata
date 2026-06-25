# Esto hay que moverlo a donde sea

Perfecto 🚀. Te preparo **un total de 10 ejercicios por categoría (Cadenas, Listas y Conjuntos)**, siguiendo la misma línea que te propuse antes. Así tendrás **30 ejercicios en total**.

---

# Ejercicios de Redis

## Cadenas (Strings)

1. Inserta en Redis 5 ciudades españolas utilizando los comandos `SET`, `MSET`, `SETNX`, `MSETNX`.
2. Usa el comando `APPEND` para añadir un sufijo a cada ciudad insertada (ejemplo: `"_2025"`).
3. Establece un tiempo de vida (TTL) de **30 segundos** para una de las ciudades con `EXPIRE`. Verifica cuánto tiempo queda con `TTL`.
4. Recupera los valores de todas las ciudades con `GET` y `MGET`.
5. Busca todas las claves insertadas con `KEYS`, probando diferentes patrones (`C*`, `*s`, etc.).
6. Crea una clave `contador` y usa `INCR` y `DECR` para modificar su valor.
7. Inserta una clave con un número decimal y utiliza `INCRBYFLOAT` para aumentar su valor.
8. Usa `SETEX` para guardar una clave temporal que dure solo 15 segundos.
9. Renombra una de las claves creadas con `RENAME` y comprueba que se ha modificado.
10. Elimina dos de las claves insertadas con `DEL` y verifica que ya no existen.

---

## Listas

1. Crea una lista llamada `L_Departamentos` e inserta 5 nombres de departamentos de una empresa usando `LPUSH` y `RPUSH`.
2. Muestra todo el contenido de la lista usando `LRANGE 0 -1`. Verifica el número de elementos con `LLEN`.
3. Recorre la lista en orden inverso (del último al primero) usando `LRANGE`.
4. Borra el primer elemento de la lista con `LPOP` y muestra la lista actualizada.
5. Inserta dos nuevos elementos en la lista solo si la clave existe (`LPUSHX`, `RPUSHX`).
6. Inserta un nuevo elemento antes y después de uno ya existente con `LINSERT`.
7. Sustituye un elemento de la lista en una posición concreta con `LSET`.
8. Recupera un elemento concreto usando `LINDEX`.
9. Extrae y elimina el último elemento de la lista con `RPOP`.
10. Usa `LTRIM` para quedarte solo con los tres primeros elementos de la lista.

---

## Conjuntos (Sets)

1. Crea un conjunto llamado `S_Lenguajes` e inserta al menos 5 lenguajes de programación con `SADD`.
2. Muestra el contenido completo del conjunto usando `SMEMBERS`.
3. Inserta al menos 3 elementos duplicados en el conjunto anterior y comprueba que no se repiten.
4. Recupera 2 elementos aleatorios del conjunto con `SRANDMEMBER 2`. Haz lo mismo permitiendo repetidos.
5. Elimina un elemento del conjunto con `SREM` y confirma que ha desaparecido.
6. Comprueba si un elemento concreto existe en el conjunto con `SISMEMBER`.
7. Muestra el número de elementos del conjunto con `SCARD`.
8. Crea un segundo conjunto `S_BBDD` con tipos de bases de datos y muestra la unión (`SUNION`) con `S_Lenguajes`.
9. Calcula la intersección (`SINTER`) entre `S_Lenguajes` y `S_BBDD`.
10. Guarda la diferencia (`SDIFF`) entre ambos conjuntos en un nuevo conjunto `S_Diferencia` y visualízalo con `SMEMBERS`.



## Ejercicios de Hashes

1. Crear un hash `libro:1` con los campos `titulo`, `autor`, `año`.
2. Usar `HMSET` para insertar 3 campos en `libro:2`.
3. Recuperar el valor de `titulo` de `libro:1` con `HGET`.
4. Recuperar todos los valores de `libro:2` con `HGETALL`.
5. Obtener solo las claves de `libro:1` con `HKEYS`.
6. Obtener solo los valores de `libro:1` con `HVALS`.
7. Insertar un campo nuevo `editorial` en `libro:1` con `HSET`.
8. Comprobar si existe el campo `año` en `libro:2` con `HEXISTS`.
9. Eliminar el campo `editorial` de `libro:1` con `HDEL`.
10. Incrementar un campo numérico `ejemplares` en `libro:1` con `HINCRBY`.
11. Crear un hash `usuario:1` con `nombre`, `email`, `edad`.
12. Obtener varios campos de `usuario:1` usando `HMGET`.
13. Insertar 3 usuarios (`usuario:2`, `usuario:3`, `usuario:4`) con `HSET`.
14. Contar cuántos campos tiene `usuario:1` con `HLEN`.
15. Guardar un hash `coche:1` con `marca`, `modelo`, `año`, `precio`.
16. Cambiar el valor del campo `precio` con `HSET`.
17. Usar `HGETALL` para recuperar todos los coches insertados.
18. Guardar un hash `pelicula:1` con `titulo`, `director`, `año`, `genero`.
19. Borrar el hash completo `pelicula:1` con `DEL`.
20. Exportar todas las claves que empiecen con `usuario:*` y mostrar sus hashes.


# Ejercicios de Sorted Sets

1. Crear un sorted set `ranking:juegos` con 4 juegos y sus puntuaciones (`ZADD`).
2. Mostrar todos los juegos ordenados por puntuación (`ZRANGE`).
3. Mostrar todos los juegos en orden inverso (`ZREVRANGE`).
4. Recuperar la puntuación de un juego con `ZSCORE`.
5. Obtener la posición de un juego con `ZRANK`.
6. Obtener la posición en orden inverso con `ZREVRANK`.
7. Incrementar la puntuación de un juego con `ZINCRBY`.
8. Obtener todos los juegos cuya puntuación esté entre 50 y 100 (`ZRANGEBYSCORE`).
9. Eliminar un juego con `ZREM`.
10. Contar cuántos juegos tienen puntuación entre 70 y 90 (`ZCOUNT`).
11. Mostrar los 3 mejores juegos (`ZREVRANGE` con `LIMIT`).
12. Mostrar los 3 peores juegos (`ZRANGE` con `LIMIT`).
13. Crear un ranking `ranking:canciones` con 5 canciones y puntuaciones.
14. Recuperar todos los miembros con sus puntuaciones (`ZRANGE … WITHSCORES`).
15. Unir dos rankings con `ZUNIONSTORE`.
16. Obtener la intersección de dos rankings con `ZINTERSTORE`.
17. Eliminar todos los juegos cuya puntuación esté por debajo de 50 (`ZREMRANGEBYSCORE`).
18. Eliminar los 2 juegos peor clasificados (`ZREMRANGEBYRANK`).
19. Usar `ZRANGEBYLEX` para ordenar un set alfabéticamente (requiere mismo score).
20. Recuperar el número total de elementos de un ranking con `ZCARD`.




## Ejercicios de Streams 

1. Crear un stream `pedidos` e insertar un pedido con `XADD`.
2. Insertar 3 pedidos más en `pedidos` con `XADD *`.
3. Ver todos los pedidos insertados usando `XRANGE pedidos - +`.
4. Recuperar solo los 2 primeros pedidos con `XRANGE pedidos - + COUNT 2`.
5. Recuperar los últimos 2 pedidos con `XREVRANGE pedidos + - COUNT 2`.
6. Crear un stream `mensajes` e insertar mensajes de un chat.
7. Leer todos los mensajes de `mensajes` con `XRANGE`.
8. Crear un grupo de consumidores `chat_group` sobre `mensajes` con `XGROUP CREATE`.
9. Añadir dos consumidores (`c1`, `c2`) al grupo `chat_group`.
10. Leer mensajes pendientes desde `c1` con `XREADGROUP`.
11. Reconocer un mensaje como procesado con `XACK`.
12. Insertar en `pagos` 5 operaciones bancarias con `XADD`.
13. Usar `XLEN` para ver cuántos eventos hay en `pagos`.
14. Limitar `pagos` a solo los 3 eventos más recientes con `XTRIM`.
15. Crear un grupo de consumidores para `pagos` y asignar mensajes.
16. Consultar mensajes pendientes con `XPENDING`.
17. Recuperar el ID del último mensaje insertado en `pedidos`.
18. Usar `XDEL` para borrar un mensaje específico en `pedidos`.
19. Crear un stream `sensores` e insertar datos de temperatura.
20. Consultar solo los datos de temperatura mayores a un ID específico con `XRANGE`.


## Ejercicios de Bitmaps

1. Usar `SETBIT usuarios_online 1 1` para marcar al usuario 1 como conectado.
2. Marcar a los usuarios 2, 5 y 8 como conectados.
3. Consultar si el usuario 5 está conectado (`GETBIT`).
4. Consultar si el usuario 3 está conectado (`GETBIT`).
5. Contar cuántos usuarios están conectados (`BITCOUNT`).
6. Desconectar al usuario 5 (`SETBIT usuarios_online 5 0`).
7. Consultar de nuevo cuántos usuarios están conectados (`BITCOUNT`).
8. Activar usuarios en posiciones 10 a 20.
9. Contar cuántos usuarios hay conectados entre los bits 0 y 10 (`BITCOUNT rango`).
10. Usar `BITPOS` para encontrar el primer usuario conectado.
11. Usar `BITPOS` para encontrar el primer usuario desconectado.
12. Crear otra clave `usuarios_mañana` y marcar 3 conectados.
13. Combinar `usuarios_online` y `usuarios_mañana` con `BITOP AND`.
14. Combinar los mismos con `BITOP OR`.
15. Combinar con `BITOP XOR`.
16. Usar `BITOP NOT` sobre `usuarios_online`.
17. Guardar un patrón de presencia de una semana en 7 claves bitmap.
18. Consultar qué días estuvo conectado el usuario 2 (`GETBIT`).
19. Crear un bitmap para votos en una encuesta y marcar los votos.
20. Contar el total de votos a favor y en contra con `BITCOUNT`.

---

## Ejercicios de HyperLogLog

1. Crear un HLL `visitas_web` y añadir 100 visitas únicas (`PFADD`).
2. Consultar la cardinalidad estimada (`PFCOUNT`).
3. Añadir 10 visitas repetidas y comprobar que `PFCOUNT` no aumenta mucho.
4. Crear otro HLL `visitas_app` y añadir 50 usuarios.
5. Consultar la cardinalidad estimada de `visitas_app`.
6. Unir `visitas_web` y `visitas_app` en `visitas_totales` con `PFMERGE`.
7. Consultar `PFCOUNT visitas_totales`.
8. Insertar 1 millón de valores en `visitas_web` y medir precisión.
9. Añadir elementos con nombres de usuarios en lugar de números (`PFADD`).
10. Comprobar el tamaño de memoria de un HLL (`MEMORY USAGE`).
11. Crear un HLL `emails_enviados` y añadir direcciones de correo.
12. Estimar cuántos correos únicos se enviaron (`PFCOUNT`).
13. Crear un HLL `clics_banner1` y `clics_banner2`.
14. Combinar ambos con `PFMERGE clics_total`.
15. Comparar resultados de `PFCOUNT clics_banner1`, `clics_banner2` y `clics_total`.
16. Añadir usuarios de diferentes países a HLLs separados (`PFADD`).
17. Combinar los HLLs de países europeos.
18. Estimar visitantes únicos de Europa con `PFCOUNT`.
19. Repetir el experimento con varios continentes.
20. Comparar estimación HLL con valores exactos en un SET.

## Ejercicios de Geo-Spatial

1. Crear un conjunto geoespacial `ciudades` con `GEOADD` (Madrid, París, Berlín).
2. Insertar Roma y Lisboa en `ciudades`.
3. Obtener las coordenadas de Madrid (`GEOPOS`).
4. Calcular la distancia entre Madrid y París (`GEODIST`).
5. Calcular la distancia entre Madrid y Berlín en millas.
6. Obtener todas las ciudades a 500 km de Madrid (`GEORADIUS`).
7. Obtener todas las ciudades a 1000 km de Roma.
8. Insertar Barcelona, Valencia y Sevilla en `ciudades`.
9. Listar todas las ciudades a 300 km de Barcelona (`GEORADIUS`).
10. Obtener las ciudades más cercanas a Lisboa (`GEOSEARCH`).
11. Ordenar los resultados de `GEOSEARCH` por distancia.
12. Insertar Nueva York y Los Ángeles.
13. Calcular la distancia entre Nueva York y Madrid.
14. Recuperar las coordenadas de todas las ciudades (`GEOPOS`).
15. Insertar Buenos Aires y calcular distancia con Madrid.
16. Buscar las 3 ciudades más cercanas a Berlín (`GEOSEARCH`).
17. Crear otro conjunto `playas` y añadir puntos geográficos.
18. Combinar consultas para `ciudades` y `playas`.
19. Obtener un hash geoespacial de París (`GEOHASH`).
20. Obtener los hashes de todas las ciudades almacenadas.



