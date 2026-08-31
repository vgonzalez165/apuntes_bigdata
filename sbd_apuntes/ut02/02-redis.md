```
------------- ESPECIALIZACIÓN EN INTELIGENCIA ARTIFICIAL Y BIG DATA -------------
---------------------------------------------------------------------------------

Módulo:                     SISTEMAS DE BIG DATA
Profesor:                   Víctor J. González
Unidad de Trabajo:          UT02. Almacenamiento de datos
Apartado:                   2.- Bases de datos clave-valor: Redis
Resultados de aprendizaje:  RA3
```


# UT02. ALMACENAMIENTO DE DATOS


## 2.- Bases de datos clave-valor: Redis

### 2.1. ¿Qué es Redis?

**Redis** (*REmote Dictionary Server*) es una base de datos en memoria, no relacional (NoSQL), basada en el modelo clave-valor. Se caracteriza principalmente por su **velocidad y ejecución** ya que trabaja principalmente sobre memoria RAM, garantizando una latencia mínima, aunque permite persistencia opcional en disco. 

Sus principales características son:

1. **Almacenamiento en memoria:** operaciones extremadamente veloces al residir los datos en RAM.
2. **Simplicidad y rendimiento:** arquitectura monohilo (un solo hilo) que facilita la predictibilidad de su rendimiento.
3. **Estructuras de datos avanzadas:** no se limita a texto plano; soporta cadenas, listas, conjuntos, hashes, conjuntos ordenados, streams, bitmaps, etc.
4. **Persistencia opcional:** permite volcar la información a disco mediante mecanismos como RDB o AOF.
5. **Alta disponibilidad y escalabilidad:** soporte para replicación maestro-esclavo, clústeres y Redis Sentinel.
6. **Soporte Pub/Sub:** sistema integrado de mensajería mediante canales de publicación y suscripción.

Redis es ampliamente utilizado, destacando los siguientes casos de uso:

* **Caché de alto rendimiento:** almacenamiento temporal de datos de consulta frecuente e invariables para descargar la base de datos principal y acelerar las respuestas web.
* **Almacenamiento de sesiones:** gestión de tokens, IDs de usuario y preferencias con tiempos de expiración automáticos.
* **Contadores y estadísticas en tiempo real:** uso de operaciones atómicas para métricas inmediatas (visitas, clics, "likes").
* **Colas de trabajo:** procesamiento de tareas asíncronas en segundo plano (emails, generación de PDFs, redimensionado de imágenes) para desacoplar servicios.
* **Sistemas Pub/Sub:** comunicación en tiempo real entre procesos (chats, notificaciones push, videojuegos multijugador).
* **Rankings y puntuaciones:** tablas de clasificación con *Sorted Sets* ordenadas automáticamente por puntuación.
* **Almacenamiento temporal:** gestión de elementos volátiles con tiempo de vida (TTL), como códigos OTP o tokens.


### 2.2. Instalación y administración de Redis

En las prácticas desplegaremos Redis en Docker, a continuación tienes la definición del servicio `docker-compose.yml` para desplegar Redis 7.2 con persistencia AOF y conectado a una red compartida:

```yaml
services:
  redis:
    image: redis:7.2
    container_name: redis-server
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data
    command: ["redis-server", "--appendonly", "yes"]
    restart: unless-stopped
    networks:
      - bigdata-network

volumes:
  redis-data:

networks:
  bigdata-network:
    external: true
```

Una vez desplegado Redis, podrás interactuar con la base de datos mediante los comandos CLI ejecutando la siguiente sentencia:

```bash
docker exec -it redis-server redis-cli
```

Algunos comandos de administración general de Redis son:

- `PING`: Comprueba si el servidor está activo. Responde `PONG`.
- `QUIT`: Cierra la conexión activa con el servidor.
- `INFO [sección]`: Muestra información interna y métricas del servidor (ej. `INFO memory`).
- `CONFIG GET <parámetro>`: Consulta valores de configuración en ejecución. Algunos parámetros son: `server_threads`, `maxclients`, `timeout`, `tcp-keepalive`, `maxmemory` ($0 = \text{sin límite}$), `maxmemory-policy` (`noeviction`, `allkeys-lru`, `volatile-lru`, etc.), `maxmemory-samples`, `hash-max-ziplist-entries` / `hash-max-ziplist-value`, `bind`, `port` (6379 por defecto), `unixsocket`, `logfile`.
- `CONFIG SET <parámetro> <valor>`: Modifica la configuración en tiempo real (ej. `CONFIG SET maxclients 100`).
- `SELECT <índice>`: Cambia a una base de datos específica (índices numéricos de 0 a 15). Solo afecta a la conexión actual (en producción se prefieren prefijos).
- `DBSIZE`: Devuelve la cantidad de claves almacenadas en la base de datos actual.
- `FLUSHDB`: Elimina todas las claves de la base de datos seleccionada.
- `FLUSHALL`: Borra absolutamente todas las claves de todas las bases de datos (0-15).
- `CLIENT LIST`: Enumera los clientes conectados y sus propiedades.
- `CLIENT KILL <id>`: Finaliza la conexión de un cliente específico según su ID.


Si prefieres conectarte a Redis desde un **entorno gráfico**, dispones de **Redis Insight:**, una interfaz visual oficial descargable (`https://redis.io/insight/`) para administrar, depurar y visualizar bases de datos locales o remotas.

Por último, también se puede interactuar con Redis desde algún lenguaje de programación, en nuestro caso lo haremos desde Python usando la librería `redis-py`. Para ello, primero debemos instalar esta librería:

```bash
pip install redis
```

Una vez instalada ya podremos conectarnos a la base de datos e interactuar con ella tal como se ve en el siguiente código:

```python
import redis

# Conexión al servicio Redis (usando resolución DNS del contenedor)
r = redis.Redis(
    host='redis',
    port=6379,
    db=0,
    decode_responses=True # Decodifica automáticamente los datos a strings (no bytes)
)

# Comprobar la conexión
print(r.ping()) # Retorna True

# Guardar y recuperar
r.set("nombre", "Victor")
print(r.get("nombre")) # Imprime 'Victor'
```



### 2.3. Primeros pasos con Redis y gestión de claves

Redis sigue una estructura clave-valor donde la clave (*key*) siempre es una cadena de texto (*string*) y el valor puede ser de múltiples tipos. Por convención, las claves siguen una nomenclatura jerárquica usando dos puntos (`:`) como separador lógico:

$$\text{objeto:id:atributo} \quad \longrightarrow \quad \texttt{usuario:100:apellidos}$$



#### Comandos generales de claves (CLI y Python):

| Comando CLI | Método Python equivalente | Descripción |
| ---------------------------------------- | ------------------------- | ----------- |
| `SET key value [EX s] [PX ms] [NX\|XX]`  | `r.set(name, value, ex=None, px=None, nx=False, xx=False)` | <br>**EX:** expira en segundos<br>**PX:** expira en milisegundos<br>**NX:** solo guarda si la clave NO existe<br>**XX:** solo guarda si la clave YA existe |
| `GET key`                                | `r.get(name)` | Recupera el valor de la clave |
| `KEYS patrón`                            | `r.keys(pattern="*")` | Busca claves por patrón *(¡Bloqueante! No recomendado en producción)* |
| `EXISTS key`                             | `r.exists(key)` | Comprueba la existencia de la clave (devuelve 1 o 0)|
| `DEL key`                                | `r.delete(*keys)` | Elimina una o más claves|
| `EXPIRE key segundos`                    | `r.expire(name, time)` | Asigna un tiempo de vida (TTL) en segundos|
| `TTL key`                                | `r.ttl(name)` | Tiempo de vida restante:<br>**$\ge 0$:** segundos restantes<br>**-1:** existe pero no tiene expiración fijada<br>**-2:** la clave no existe|
| `TYPE key`                               | `r.type(name)` | Devuelve el tipo de dato asignado a la clave|


### 2.4. Tipos de Datos en Redis

Redis soporta diversas estructuras optimizadas para propósitos concretos.

#### 1. Cadenas (*Strings*)

Son el tipo de dato más elemental. Admite **texto, valores numéricos, JSON o datos binarios** (imágenes, serializaciones) con un límite de hasta **512 MB**. Son ideales para almacenar valores simples como texto, números o JSON. 

Algunos casos de uso para las cadenas en Redis son: 

- **Caching**: almacenar resultados de consultas a bases de datos o APIs.
- **Contadores**: contadores de visitas, "me gusta", etc.
- **Almacenamiento de sesiones**: guardar datos de sesión de usuario serializados.
- **Banderas (flags)**: almacenar estados simples (ej. "activo", "inactivo").

En la siguiente tabla se muestran los principales comandos para trabajar con cadenas:

| Comando CLI                                 | Equivalente Python (`redis-py`) | Descripción |
| ------------------------------------------- | --- | --- |
| `SET key value [EX s] [PX ms] [NX\|XX]`     | `r.set(name, value, ex=None, px=None, nx=False, xx=False)` | Guarda un par clave-valor. Permite fijar expiración en segundos (`ex`), milisegundos (`px`), o condicionar según no exista (`nx=True`) o ya exista (`xx=True`).|
| `GET key`                                   | `r.get(name)`                                              | Recupera el valor asignado a la clave.|
| `DEL key`                                   | `r.delete(*keys)`                                          | Elimina una o más claves.|
| `INCR key`                                  | `r.incr(name)`                                             | Incrementa en 1 el valor numérico de una clave.|
| `DECR key`                                  | `r.decr(name)`                                             | Decrementa en 1 el valor numérico de una clave.|
| `EXPIRE key seconds`                        | `r.expire(name, time)`                                     | Establece un tiempo de vida (TTL) en segundos para la clave.|
| `TTL key`                                   | `r.ttl(name)`                                              | Devuelve el tiempo de vida restante en segundos ($-1$ si no tiene expiración, $-2$ si no existe).|

A continuación se puede ver un ejemplo de manipulación de cadenas en Redis con Python.

```python
import redis
import time

r = redis.Redis(host='redis', port=6379, db=0, decode_responses=True)

# Guardar un valor simple y recuperarlo
r.set("nombre", "Victor")
print(r.get("nombre"))  # 'Victor'

# Guardar con condición NX (solo si no existe)
r.set("contador", 1, nx=True)
print(r.get("contador"))  # '1'
r.set("contador", 100, nx=True)  # No tendrá efecto porque ya existe
print(r.get("contador"))  # '1'

# Guardar con tiempo de expiración (TTL)
r.set("mensaje", "Hola mundo", ex=10)
print("TTL inicial:", r.ttl("mensaje"))  # 10
time.sleep(3)
print("TTL tras 3s:", r.ttl("mensaje"))  # 7

```


#### 2. Listas (*Lists*)

Las listas son una **colección ordenada** de cadenas. Se implementan como listas enlazadas, lo que permite operaciones de inserción y eliminación muy rápidas en los extremos. Son ideales para implementar colas o pilas.

Se utilizan habitualmente para:

- **Colas de mensajes**: implementar colas de tareas para procesadores en segundo plano.
- **Pilas (stacks)**: historial de acciones recientes.
- **Feeds de redes sociales**: almacenar los últimos N elementos de un feed.
- **Listas de reproducción**: mantener el orden de elementos.

Los principales comandos con listas son:

| Comando CLI                       | Equivalente Python           | Descripción |
| --------------------------------- | ---------------------------- | --- |
| `LPUSH key value [value ...]`     | `r.lpush(name, *values)`     | Inserta uno o más valores al inicio (izquierda) de la lis|
| `RPUSH key value [value ...]`     | `r.rpush(name, *values)`     | Inserta uno o más valores al final (derecha) de la lis|
| `LPOP key`                        | `r.lpop(name, count=None)`   | Extrae y elimina el primer elemento de la lis|
| `RPOP key`                        | `r.rpop(name, count=None)`   | Extrae y elimina el último elemento de la lis|
| `LRANGE key start stop`           | `r.lrange(name, start, end)` | Obtiene un rango de elementos según sus índices (ej. `0` a `-1` para todo|
| `LLEN key`                        | `r.llen(name)`               | Devuelve la longitud o número total de elementos en la lis|
| `BLPOP key [key ...] timeout`     | `r.blpop(keys, timeout=None)`| Versión bloqueante de `LPOP`; espera hasta que haya elementos disponibles o se agote el tiem|

Ejemplo de uso de listas.

```python
lista_nombre = "tareas"

# Añadir elementos al final de la lista
r.rpush(lista_nombre, "Estudiar Python")
r.rpush(lista_nombre, "Hacer ejercicio")
r.rpush(lista_nombre, "Comprar comida")

# Mostrar todos los elementos (de 0 a -1)
print("Lista completa:", r.lrange(lista_nombre, 0, -1))

# Extraer el primer elemento (comportamiento de cola / FIFO)
tarea_inicial = r.lpop(lista_nombre)
print("Tarea eliminada desde el inicio:", tarea_inicial)

# Extraer el último elemento (comportamiento de pila / LIFO)
tarea_final = r.rpop(lista_nombre)
print("Tarea eliminada desde el final:", tarea_final)

# Comprobar la longitud y la lista actualizada
print("Longitud:", r.llen(lista_nombre))
print("Lista actualizada:", r.lrange(lista_nombre, 0, -1))

```



#### 3. Conjuntos (*Sets*)

Un conjunto es una **colección desordenada de cadenas únicas**. Los conjuntos son ideales para almacenar elementos donde el orden no importa y se necesita asegurar la unicidad, o para realizar operaciones de teoría de conjuntos.

Los conjuntos se suelen utilizar para:

- **Etiquetas (tags)**: asociar tags a artículos, fotos, etc.
- **Miembros únicos**: lista de usuarios únicos en un chat, visitantes únicos.
- **Relaciones**: "usuarios que siguen a X", "productos en el carrito".
- **Operaciones de conjuntos**: amigos en común, usuarios con intereses compartidos

Los principales comandos son:

| Comando CLI                    | Comando Python             | Descripción |
| ------------------------------ | -------------------------- | --- |
| `SADD key member [member ...]` | `r.sadd(name, *values)`    | Añade uno o más miembros al conjunto.|
| `SREM key member [member ...]` | `r.srem(name, *values)`    | Elimina uno o más miembros del conjunto.|
| `SMEMBERS key`                 | `r.smembers(name)`         | Devuelve todos los miembros almacenados en el conjunto.|
| `SISMEMBER key member`         | `r.sismember(name, value)` | Comprueba si un miembro pertenece al conjunto (devuelve 1 si existe, 0 si no).|
| `SCARD key`                    | `r.scard(name)`            | Obtiene el número total de miembros (cardinalidad).|
| `SINTER key [key ...]`         | `r.sinter(keys, *args)`    | Devuelve la intersección entre dos o más conjuntos.|
| `SUNION key [key ...]`         | `r.sunion(keys, *args)`    | Devuelve la unión de dos o más conjuntos.|

Ejemplo de uso:

```python
# Crear conjuntos
r.sadd("users:online", "Alice", "Bob", "Charlie")
r.sadd("users:premium", "Alice", "David")

# Ver miembros y pertenencia
print("Usuarios online:", r.smembers("users:online"))
print("¿Está Alice online?:", r.sismember("users:online", "Alice"))  # 1 (True)
print("¿Está Edgar online?:", r.sismember("users:online", "Edgar"))  # 0 (False)

# Operaciones de conjuntos
online_y_premium = r.sinter("users:online", "users:premium")
print("Usuarios online que son premium (Intersección):", online_y_premium)  # {'Alice'}

todos_los_usuarios = r.sunion("users:online", "users:premium")
print("Todos los usuarios (Unión):", todos_los_usuarios)
```

### 4. Conjuntos ordenados (*Sorted Sets*)

Son similares a los conjuntos, pero **cada miembro único tiene un score (puntuación) asociado**, que es un valor numérico de coma flotante. Los elementos se mantienen ordenados por su score. Si varios miembros tienen el mismo score, se ordenan lexicográficamente.

Su uso más común es para:
- **Tablas de clasificación (leaderboards)**: rankings de juegos, puntuaciones.
- **Clasificación de elementos**: artículos más populares por votos, usuarios más activos.
- **Series temporales simples**: eventos con un timestamp como score.

Comandos con conjuntos

| Comando CLI                              | Comando Python | Descripción |
| ---------------------------------------- | --- | --- |
| `ZADD key score member [...]`            | `r.zadd(name, mapping, nx=False, xx=False, ch=False, incr=False)` | Añade uno o más miembros con sus puntuaciones (*scores*).|
| `ZRANGE key start stop [WITHSCORES]`     | `r.zrange(name, start, end, desc=False, withscores=False, score_cast_func=float)` | Obtiene un rango de elementos ordenados ascendentemente por score.|
| `ZREVRANGE key start stop [WITHSCORES]`  | `r.zrevrange(name, start, end, withscores=False, score_cast_func=float)` | Obtiene un rango de elementos en orden descendente (mayor a menor puntuación).|
| `ZRANGEBYSCORE key min max [WITHSCORES]` | `r.zrangebyscore(name, min, max, start=None, num=None, withscores=False, score_cast_func=float)` | Filtra los miembros que se encuentran dentro de un rango de puntuación.|
| `ZREM key member [member ...]`           | `r.zrem(name, *values)` | Elimina uno o más miembros del conjunto ordenado.|
| `ZSCORE key member`                      | `r.zscore(name, value)` | Consulta la puntuación (*score*) asignada a un miembro.|
| `ZCARD key`                              | `r.zcard(name)` | Obtiene la cantidad total de miembros.|

Ejemplo de uso.

```python
# Añadir miembros con sus puntuaciones mediante un diccionario mapping={miembro: score}
r.zadd("leaderboard", {"Alice": 100, "Bob": 85, "Charlie": 120})

# Consultar clasificación de menor a mayor puntuación
print("Orden ascendente:", r.zrange("leaderboard", 0, -1, withscores=True))
# [('Bob', 85.0), ('Alice', 100.0), ('Charlie', 120.0)]

# Consultar clasificación de mayor a menor puntuación (ranking)
print("Ranking descendente:", r.zrevrange("leaderboard", 0, -1, withscores=True))
# [('Charlie', 120.0), ('Alice', 100.0), ('Bob', 85.0)]

# Consultar el score de un miembro concreto
print("Score de Alice:", r.zscore("leaderboard", "Alice"))  # 100.0
```

---

### 5. Hashes (*Hash Maps*)

Un hash es un **mapa de campos a valores**. Cada hash puede almacenar hasta 232 - 1 pares campo-valor. Son perfectos para representar objetos o registros de datos donde cada campo tiene un nombre y un valor asociado.

Los hashes se suelen utilizar para:
- **Almacenamiento de objetos**: perfiles de usuario, detalles de productos.
- **Caché de objetos**: almacenar objetos complejos de forma estructurada.
- **Configuraciones**: guardar configuraciones de aplicaciones o usuarios.

Algunos comandos para trabajar con hashes son:

| Comando CLI | Comando Python | Descripción |
| ---------------------------- | --- | --- |
| `HSET key field value [...]` | `r.hset(name, key=None, value=None, mapping=None)` | Establece el valor de uno o varios campos dentro del hash.|
| `HGET key field`<            | `r.hget(name, key)` | Obtiene el valor de un campo específico.|
| `HGETALL key`                | `r.hgetall(name)` | Obtiene todos los campos y sus respectivos valores.|
| `HDEL key field [field ...]` | `r.hdel(name, *keys)` | Elimina uno o más campos del hash.|
| `HKEYS key`                  | `r.hkeys(name)` | Devuelve la lista con todos los nombres de los campos.|
| `HVALS key`                  | `r.hvals(name)` | Devuelve la lista con todos los valores almacenados.|
| `HLEN key`                   | `r.hlen(name)` | Devuelve el número total de campos contenidos en el hash.|

Ejemplo de uso

```python
# Guardar un objeto estructurado usando mapping
r.hset("ranking:1:user1", mapping={"name": "Clara", "score": "13250"})

# Obtener un campo específico
print("Nombre:", r.hget("ranking:1:user1", "name"))  # 'Clara'

# Obtener todo el objeto
print("Todo el registro:", r.hgetall("ranking:1:user1"))
# {'name': 'Clara', 'score': '13250'}

# Consultar claves y longitud
print("Campos existentes:", r.hkeys("ranking:1:user1"))  # ['name', 'score']
print("Número de campos:", r.hlen("ranking:1:user1"))    # 2
```



### 6. Streams

Son un tipo de dato de **solo anexar (append-only)** que representa un log de eventos. Cada entrada en un stream tiene un ID único y un conjunto de pares campo-valor. Los streams están diseñados para sistemas de procesamiento de eventos y colas de mensajes persistentes.

Algunos casos de uso comunes son:
- **Logs de eventos**: almacenar un historial inmutable de eventos.
- **Sistemas de mensajería**: colas de mensajes persistentes con procesamiento distribuido (grupos de consumidores).
- **Procesamiento de datos en tiempo real**: ingesta y análisis de datos de sensores o IoT


#### Comandos de CLI y Python:

| Comando CLI | Equivalente Python (`redis-py`) | Descripción |
| ----------------------------------- | --- | --- |
| `XADD key ID field value [...]` | `r.xadd(name, fields, id="*", maxlen=None, approximate=True, nomkstream=False)` | Añade una entrada al stream (usando `*` para generar el ID temporal automáticamente).|
| `XRANGE key start end`          | `r.xrange(name, min="-", max="+", count=None)` | Lee un rango de entradas comprendido entre dos IDs.|
| `XREAD [COUNT c] [BLOCK ms] STREAMS key... ID...` | `r.xread(streams, count=None, block=None)` | Lee entradas de uno o varios streams, con soporte de bloqueo reactivo.|
| `XGROUP CREATE key group ID [MKSTREAM]` | `r.xgroup_create(name, groupname, id="$", mkstream=False)` | Crea un grupo de consumidores para el procesamiento distribuido.|
| `XREADGROUP GROUP grp cname [COUNT c] [BLOCK ms] STREAMS key... ID...` | `r.xreadgroup(groupname, consumername, streams, count=None, block=None, noack=False)` | Lee entradas del stream a través de un consumidor de un grupo asignado.|

Ejemplo de uso:

```python
# Añadir eventos al stream con ID automático ("*")
id1 = r.xadd("stream_eventos", {"sensor": "temp", "valor": "22.5"})
id2 = r.xadd("stream_eventos", {"sensor": "humedad", "valor": "60%"})

# Leer todas las entradas del stream (desde el inicio "-" hasta el final "+")
eventos = r.xrange("stream_eventos", min="-", max="+")
for evento_id, datos in eventos:
    print(f"ID: {evento_id} -> Datos: {datos}")

# Crear un grupo de consumidores y leer eventos
r.xgroup_create("stream_eventos", "mi_grupo", id="0", mkstream=True)
entradas_grupo = r.xreadgroup("mi_grupo", "consumidor_1", {"stream_eventos": ">"}, count=1)
print("Leído por grupo:", entradas_grupo)
```


### 7. Bitmaps

Son un tipo de dato que permite tratar las cadenas de Redis como un **array de bits**. Puedes establecer o borrar bits individuales en un offset específico. Son extremadamente eficientes para almacenar información booleana a gran escala.

Los bitmaps se usan principalmente para:
- **Presencia de usuarios**: saber qué usuarios están online (cada offset es un ID de usuario).
- **Flags de características**: marcar si un usuario ha usado una característica específica.
- **Análisis de cohortes**: identificar usuarios que realizaron una acción en un día específico.
- **Votaciones binarias**: registrar votos "sí/no".

Algunos comandos para trabajar con bitmaps

| Comando CLI | Equivalente Python (`redis-py`) | Descripción |
| --- | --- | --- |
| `SETBIT key offset value` | `r.setbit(name, offset, value)` | Establece a `0` o `1` el bit en la posición (*offset*) indicada.|
| `GETBIT key offset` | `r.getbit(name, offset)` | Obtiene el valor (0 o 1) del bit en el offset dado.|
| `BITCOUNT key [start end]` | `r.bitcount(name, start=None, end=None)` | Cuenta el número total de bits fijados a `1`.|
| `BITPOS key bit [start] [end]` | `r.bitpos(name, bit, start=None, end=None)` | Encuentra la posición del primer bit establecido al valor indicado (`0` o `1`).|

Ejemplo de uso:

```python
# Marcar usuarios conectados (usando el ID del usuario como offset)
r.setbit("usuarios_conectados", 100, 1)  # Usuario 100 online
r.setbit("usuarios_conectados", 105, 1)  # Usuario 105 online

# Consultar el estado de un usuario
print("¿Usuario 100 online?:", r.getbit("usuarios_conectados", 100))  # 1
print("¿Usuario 101 online?:", r.getbit("usuarios_conectados", 101))  # 0

# Contar cuántos usuarios están activos en total
print("Total usuarios online:", r.bitcount("usuarios_conectados"))  # 2

# Encontrar la primera posición con bit a 1
print("Primer offset activo:", r.bitpos("usuarios_conectados", 1))  # 100
```


### 8. HyperLogLog

Es un algoritmo **probabilístico** para estimar la cardinalidad de un conjunto (el número de elementos únicos) con un uso de memoria muy bajo. Es ideal cuando necesitas **contar elementos únicos** en grandes volúmenes de datos y estás dispuesto a aceptar un **pequeño margen de error**.

Se usa habitualmente para:
- **Contadores de visitantes únicos**: en sitios web o aplicaciones.
- **Estimación de elementos únicos**: IPs únicas, IDs de productos vistos.
- **Análisis de tendencias**: ver la cardinalidad de eventos a lo largo del tiempo.

Algunos comandos son:

| Comando CLI                       | Comando Python              | Descripción |
| --------------------------------- | --------------------------- | --- |
| `PFADD key element [element ...]` | `r.pfadd(name, *values)`    | Añade uno o más elementos al registro HyperLogLog.|
| `PFCOUNT key [key ...]`           | `r.pfcount(*sources)`       | Estima la cardinalidad (cantidad de elementos únicos).|
| `PFMERGE destkey sourcekey [...]` | `r.pfmerge(dest, *sources)` | Combina múltiples HyperLogLogs en una única clave de destino.|

Ejemplo de uso:

```python
# Registrar accesos únicos (incluso con elementos repetidos)
r.pfadd("visitas:dia1", "192.168.1.1", "192.168.1.2", "192.168.1.1")
r.pfadd("visitas:dia2", "192.168.1.3", "192.168.1.2")

# Estimar elementos únicos del día 1
print("Visitas únicas día 1:", r.pfcount("visitas:dia1"))  # 2

# Unir registros y calcular el total global estimado
r.pfmerge("visitas:total", "visitas:dia1", "visitas:dia2")
print("Total global estimado de visitas únicas:", r.pfcount("visitas:total"))  # 3
```

### 9. Geo-Spatial (Datos Geoespaciales)

Permite almacenar coordenadas de latitud y longitud y realizar consultas basadas en la distancia.
Utiliza conjuntos ordenados internamente para almacenar los puntos geoespaciales, lo que permite operaciones eficientes de búsqueda por radio o por caja.

Se usa habitualmente para:

- **Búsqueda por radio o área geográfica**
- **Cálculo de distancias**
- **Ordenación por cercanía**

Comandos para datos geoespaciales

| Comando CLI                                   | Comando Python                                                  | Descripción |
| --------------------------------------------- | --------------------------------------------------------------- | --- |
| `GEOADD key lon lat member [...]`             | `r.geoadd(name, mapping, nx=False, xx=False, ch=False)`         | Registra uno o varios puntos geoespaciales (longitud, latitud y nombre del elemento). |
| `GEODIST key member1 member2 [unit]`          | `r.geodist(name, member1, member2, unit='m')`                   | Calcula la distancia entre dos miembros registrados en la unidad indicada (ej. `'m'`, `'km'`). |
| `GEORADIUS key lon lat rad unit [...]`        | `r.georadius(name, longitude, latitude, radius, unit='m', ...)` | Busca y lista los miembros ubicados dentro de un radio circular respecto a unas coordenadas. |
| `GEORADIUSBYMEMBER key member rad unit [...]` | `r.georadiusbymember(name, member, radius, unit='m', ...)`      | Busca miembros dentro de un radio tomando como centro la posición de otro miembro. |
| `GEOHASH key member [member ...]`             | `r.geohash(name, *members)`                                     | Devuelve la representación geohash alfanumérica de los miembros solicitados. |

Ejemplo de uso:

```python
# Añadir puntos de interés: mapping=[longitud, latitud, nombre]
r.geoadd("lugares", [-5.6635, 40.9688, "Salamanca", -5.5671, 42.5987, "Leon"])

# Calcular la distancia en kilómetros entre dos ubicaciones
distancia = r.geodist("lugares", "Salamanca", "Leon", unit="km")
print(f"Distancia: {distancia} km")

# Buscar ubicaciones en un radio de 200 km desde unas coordenadas concretas
cercanos = r.georadius("lugares", -5.6000, 41.5000, 200, unit="km", withdist=True)
print("Lugares dentro del radio:", cercanos)

# Obtener el geohash de una ubicación
print("Geohash de Leon:", r.geohash("lugares", "Leon"))
```