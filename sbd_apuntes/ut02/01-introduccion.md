```
------------- ESPECIALIZACIÓN EN INTELIGENCIA ARTIFICIAL Y BIG DATA -------------
---------------------------------------------------------------------------------

Módulo:                     SISTEMAS DE BIG DATA
Profesor:                   Víctor J. González
Unidad de Trabajo:          UT02. Almacenamiento de datos
Apartado:                   1.- Introducción al almacenamiento en Big Data
Resultados de aprendizaje:  RA3
```


# UT02. ALMACENAMIENTO DE DATOS


## 1. Introducción al almacenamiento en Big Data

### 1.1. ¿Qué es el Almacenamiento en Big Data?

El almacenamiento en Big Data comprende el conjunto de arquitecturas, sistemas y tecnologías concebidas para almacenar, administrar y procesar volúmenes masivos de datos que superan la capacidad de gestión de los sistemas de bases de datos tradicionales.

#### Soluciones comunes:

- **Almacenamiento en la nube:** Ejemplos como AWS S3 o Azure Blob Storage.
- **Sistemas de archivos distribuidos:** Hadoop.
- **Bases de datos NoSQL:** Especializadas en el tratamiento de datos no estructurados.


### 1.2. Comparativa: almacenamiento tradicional vs. Big Data

| Criterio            | Almacenamiento Tradicional | Almacenamiento en Big Data |
| ------------------- | --- | --- |
| **Esquema**         | **Fijo y rígido (*Schema-on-Write*):** La estructura de la tabla se debe definir antes de insertar los datos.           | **Flexible o dinámico (*Schema-on-Read*):** La estructura se interpreta en el momento de la lectura, admitiendo variedad. |
| **Escalabilidad**   | **Vertical (*Scale-Up*):** Incremento de recursos (CPU, RAM, disco) en un único servidor. Costosa y con límites físicos. | **Horizontal (*Scale-Out*):** Incorporación de múltiples servidores *commodity* (económicos) al clúster. Casi ilimitada y económica. |
| **Arquitectura**    | **Centralizada:** Un solo servidor gestiona todos los datos y operaciones. | **Distribuida:** El almacenamiento y cómputo se reparte entre decenas, cientos o miles de nodos. |
| **Tipos de Datos**  | Principalmente **estructurados** (tablas con filas y columnas bien definidas). | **Todo tipo de datos:** estructurados, semiestructurados (JSON, logs) y no estructurados (imágenes, vídeos). |
| **Modelo de Datos** | **Relacional:** Basado en tablas, claves primarias/foráneas y lenguaje SQL. | **No relacional (NoSQL)** o sistemas de archivos distribuidos optimizados para patrones de acceso específicos. |
| **Rendimiento**     | Optimizado para transacciones complejas (**OLTP**) y cumplimiento estricto de propiedades **ACID**. | Optimizado para procesamiento por lotes (**batch**) y, en ocasiones, tiempo real. Prioriza el *throughput* sobre la latencia. |
| **Costo**           | **Alto:** Requiere frecuentemente hardware propietario y de alta gama. | **Bajo:** Emplea hardware *commodity* estándar y software de código abierto. |

