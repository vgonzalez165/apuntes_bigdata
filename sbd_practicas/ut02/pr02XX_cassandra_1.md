```
------------- ESPECIALIZACIÓN EN INTELIGENCIA ARTIFICIAL Y BIG DATA -------------
---------------------------------------------------------------------------------

Módulo:                     SISTEMAS DE BIG DATA
Profesor:                   Víctor J. González
Unidad de Trabajo:          UT02. Almacenamiento de datos
Práctica:                   PR02XX: Listas en Redis
Resultados de aprendizaje:  RA3
```


# PR02XX: Puesta en marcha de Cassandra

TODO: esto hay que revisarlo bien



### Paso 1: Levantar el contenedor de Cassandra

Ejecuta en la terminal el siguiente comando para crear un contenedor con Cassandra 4.x/5.x:

```bash
docker run --name cassandra-lab \
  -p 9042:9042 \
  -e MAX_HEAP_SIZE="1024M" \
  -e HEAP_NEWSIZE="256M" \
  -d cassandra:latest

```

* **`-p 9042:9042`:** Expone el puerto nativo del protocolo binario de Cassandra (utilizado por `cqlsh` y por los drivers de Python, Java, etc.).
* **`MAX_HEAP_SIZE` / `HEAP_NEWSIZE`:** Limita el consumo de memoria de la máquina virtual Java (JVM) para que funcione de forma fluida en equipos de laboratorio con recursos limitados.

### Paso 2: Verificar el arranque del nodo

Cassandra tarda aproximadamente entre **30 y 60 segundos** en inicializar la JVM y unirse al anillo local. Para comprobar si el servicio está listo:

```bash
# Ver los logs en tiempo real hasta ver "Startup complete"
docker logs -f cassandra-lab

```

Una vez iniciado, consulta el estado del nodo con la herramienta de administración `nodetool`:

```bash
docker exec -it cassandra-lab nodetool status

```

**Salida esperada:**

```text
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address     Load       Tokens  Owns (effective)  Host ID                               Rack
UN  127.0.0.1   104.5 KiB  16      100.0%            a1b2c3d4-e5f6-7890-abcd-ef1234567890  rack1

```

> **Significado del estado `UN`:**
> * **`U` (Up):** El nodo está encendido y operativo.
> * **`N` (Normal):** El nodo está en estado normal de servicio (ni arrancando ni dándose de baja).
> 
> 

### Paso 3: Conexión mediante la consola interactiva `cqlsh`

`cqlsh` (*Cassandra Query Language Shell*) es la interfaz de línea de comandos para interactuar con la base de datos:

```bash
docker exec -it cassandra-lab cqlsh

```

Aparecerá el prompt interactivo de CQL:

```text
Connected to Test Cluster at 127.0.0.1:9042
[cqlsh 6.2.0 | Cassandra 5.0.0 | CQL spec 3.4.7 | Native protocol v5]
Use HELP for help.
cqlsh> 

```

### Paso 4: Primeros comandos en `cqlsh`

Comprueba el entorno ejecutando los siguientes comandos de inspección:

```sql
-- 1. Ver la ayuda general
HELP;

-- 2. Consultar los keyspaces (esquemas) del sistema
DESCRIBE KEYSPACES;

-- 3. Ver el nivel de consistencia actual de la sesión (por defecto: ONE)
CONSISTENCY;

-- 4. Modificar el nivel de consistencia para las consultas de la sesión
CONSISTENCY QUORUM;

-- 5. Salir de cqlsh
EXIT;

```
