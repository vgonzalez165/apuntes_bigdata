```
------------- ESPECIALIZACIÓN EN INTELIGENCIA ARTIFICIAL Y BIG DATA -------------
---------------------------------------------------------------------------------

Módulo:                     BIG DATA APLICADO
Profesor:                   Víctor J. González
Unidad de Trabajo:          UT01. Introducción al Big Data y paradigmas distribuidos
Apartado:                   1.1.- ¿Qué es Apache? Historia
Resultados de aprendizaje:  RA2
```

# UT01: INTRODUCCIÓN A BIG DATA Y PARADIGMAS DISTRIBUIDOS

## 1. Contexto y motivación

### 1.1.- El crecimiento del Big Data

En las últimas décadas, el volumen de datos a nivel global ha crecido de manera exponencial. La información se origina a partir de múltiples fuentes heterogéneas, entre las que destacan:

- Redes sociales.
- Sensores de Internet de las Cosas (IoT).
- Registros de transacciones y datos financieros.
- Sistemas empresariales (ERP como SAP u Oracle).
- Datos multimedia (vídeos, imágenes y audios).
- Aplicaciones móviles y registros (*logs*) de servidores.

Este fenómeno se denomina **Big Data** y se define técnicamente mediante las **3V**:

- **Volumen:** Generación masiva y constante de ingentes cantidades de información, transitando de rangos de Gigabytes (GB) a Terabytes (TB), Petabytes (PB) y Zetabytes (ZB).
- **Velocidad:** Los datos se producen con alta celeridad y demandan procesamiento continuo, abarcando desde procesamiento por lotes (*batch*) o periódico, hasta tiempo casi real (*near real-time*) y tiempo real.
- **Variedad:** Coexistencia de múltiples formatos que comprenden datos estructurados (tablas relacionales), semiestructurados (archivos JSON, XML) y no estructurados (texto plano, vídeo, imágenes).


### 1.2.- Limitaciones de los sistemas tradicionales

Las soluciones tradicionales, como las bases de datos relacionales (RDBMS) y las arquitecturas monolíticas centralizadas, fueron concebidas para operar en entornos controlados, con volúmenes moderados, esquemas muy estructurados y baja concurrencia masiva. En el contexto del Big Data, presentan cinco limitaciones críticas:

1. **Escalabilidad vertical limitada (*Scale Up*):** Para incrementar el rendimiento, los sistemas tradicionales dependen de ampliar la capacidad del único servidor existente (añadiendo CPU, RAM o almacenamiento en disco). Este enfoque es sumamente costoso y no es viable a largo plazo frente a la escalabilidad horizontal (*Scale Out*).
2. **Procesamiento centralizado:** Los datos se almacenan y procesan en un único nodo central, convirtiéndose en el cuello de botella del sistema.
3. **Falta de tolerancia a fallos:** La dependencia de un nodo centralizado implica que la caída o fallo de este servidor provoca la interrupción total del servicio.
4. **Dificultad ante datos semiestructurados o no estructurados:** Los RDBMS exigen esquemas relacionales rígidos. Puesto que cerca del 80% de los datos corporativos actuales son no estructurados, su gestión mediante soluciones heredadas resulta ineficiente.
5. **Procesamiento por lotes lento:** El análisis de grandes volúmenes de datos mediante arquitecturas tradicionales requiere tiempos de ejecución prolongados (horas o días).


### 1.3.- Nuevos enfoques: Sistemas Distribuidos

Frente a las limitaciones de los sistemas convencionales, el paradigma distribuido adoptado por soluciones como Apache Hadoop introduce un nuevo marco de trabajo:

- **Almacenamiento distribuido (HDFS):** Los archivos de gran tamaño se dividen en bloques y se reparten entre múltiples servidores o nodos del clúster, aprovechando la capacidad acumulada de muchas máquinas.
- **Procesamiento distribuido (MapReduce, Spark):** Las tareas computacionales se dividen y se ejecutan en paralelo directamente sobre los distintos nodos del clúster, reduciendo sensiblemente los tiempos de ejecución.
- **Tolerancia a fallos:** Los datos se replican en diferentes nodos físicos y las tareas fallidas se reasignan automáticamente, garantizando alta disponibilidad sin requerir respaldos manuales constantes.
- **Escalabilidad horizontal:** Es posible incrementar la capacidad de cómputo y almacenamiento añadiendo nuevos nodos estándar (*commodity hardware*) al clúster sin necesidad de interrumpir el servicio.






## 2. Apache Hadoop: ¿Qué es?

### 2.1.- Definición

**Apache Hadoop** es un *framework* de software de código abierto que permite el almacenamiento distribuido y el procesamiento paralelo de grandes volúmenes de datos utilizando clústeres de ordenadores convencionales.

- **Framework de software:** Conjunto estructurado de librerías, servicios y herramientas diseñadas para construir aplicaciones analíticas distribuidas sin necesidad de programar la infraestructura de bajo nivel desde cero.
- **Código abierto:** Proyecto auspiciado por la *Apache Software Foundation* bajo licencia Open Source, lo que permite su uso, personalización y redistribución sin costes de adquisición de licencias.
- **Grandes volúmenes de datos:** Diseñado específicamente para procesar volúmenes masivos de datos (del orden de Terabytes o Petabytes) que desbordan la capacidad de los sistemas tradicionales.
- **Clústeres de ordenadores convencionales (*Commodity Hardware*):** Opera sobre agrupaciones de máquinas estándar conectadas en red que funcionan de forma coordinada, evitando la necesidad de recurrir a supercomputadores costosos.


### 2.2.- Componentes principales

Hadoop resuelve las necesidades de almacenamiento masivo y procesamiento eficiente mediante dos componentes fundamentales:

- **HDFS (Hadoop Distributed File System):** Sistema de archivos distribuido que divide los ficheros de gran tamaño en bloques y los almacena a lo largo de los nodos del clúster. Proporciona alta disponibilidad mediante la replicación automática de bloques y está optimizado para operaciones secuenciales de lectura y escritura.
- **YARN (Yet Another Resource Negotiator):** Gestor centralizado de recursos del clúster introducido en Hadoop 2.x. Desacopla la gestión de hardware del modelo de ejecución, permitiendo que múltiples motores de procesamiento compartan los recursos del entorno.

### 2.3.- Características de Hadoop

- **Escalabilidad:** Crecimiento horizontal ágil y transparente mediante la adición de nuevos nodos al clúster.
- **Tolerancia a fallos:** Replicación de bloques en nodos físicos independientes para prevenir la pérdida de datos ante incidentes de hardware.
- **Portabilidad:** Desarrollado íntegramente en Java, lo que posibilita su despliegue sobre diversas plataformas y sistemas operativos.
- **Eficiencia:** Procesamiento paralelo masivo que explota el principio de localidad de los datos.
- **Ecosistema en expansión:** Amplia comunidad que proporciona un ecosistema continuo de herramientas complementarias.


### 2.4.- Historia de Hadoop

- **Inicios de los 2000:** Google requiere indexar y procesar miles de millones de páginas web de forma eficiente.
- **2003:** Google publica el artículo científico *"The Google File System"* (GFS), describiendo su arquitectura de sistema de archivos distribuido.
- **2004:** Jeffrey Dean y Sanjay Ghemawat (Google) publican el artículo *"MapReduce: simplified data processing on large clusters"*, sentando las bases del procesamiento paralelo distribuido.
- **2004:** Doug Cutting y Mike Cafarella desarrollan el proyecto de motor de búsqueda de código abierto **Nutch** en Yahoo! y deciden implementar estas especificaciones para superar sus cuellos de botella de escalabilidad.
- **2005:** La tecnología de almacenamiento y cómputo de Nutch se independiza bajo el nombre de **Hadoop**, llamado así en homenaje al elefante de juguete del hijo de Doug Cutting.
- **2006:** Hadoop se convierte en un proyecto independiente de primer nivel dentro de la *Apache Software Foundation*, con Yahoo! como patrocinador principal.
- **2012:** Aparición de **Hadoop 2.0**, incorporando **YARN**. Esto desacopló la gestión de recursos de MapReduce, permitiendo la integración de otros motores de procesamiento dentro del mismo clúster.
- **Actualidad:** Hadoop engloba un ecosistema completo de herramientas de código abierto orientadas a cubrir todas las fases del ciclo de vida del dato.


### 2.5.- Herramientas del ecosistema Hadoop

El ecosistema de Hadoop dispone de decenas de herramientas que cubren prácticamente cualquier necesidad surgida al trabajar en Big Data. En la siguiente tabla se muestran algunas de las más destacables.

| Herramienta | Tipo / Propósito | Descripción funcional |
| :--- | :--- | :--- |
| **Apache Hive** | *Data Warehousing* / SQL | Permite realizar consultas y análisis sobre datos en HDFS utilizando el lenguaje declarativo **HiveQL** (similar a SQL). |
| **Apache Pig** | Procesamiento / Scripting | Plataforma de alto nivel para diseñar tareas complejas de MapReduce mediante el lenguaje de scripting procedural **Pig Latin**. |
| **Apache Spark** | Motor de Cómputo en Memoria | Motor de cómputo en memoria para análisis en tiempo real, procesos *batch* y *Machine Learning*, compatible con Scala, Java, Python y R. |
| **Apache HBase** | Base de Datos NoSQL | Base de datos NoSQL distribuida, columnar y escalable que se ejecuta sobre HDFS. |
| **Apache Kafka** | Ingesta / *Streaming* | Plataforma distribuida de mensajería y publicación/suscripción para la transmisión de flujos de eventos en tiempo real. |
| **Apache Flume** | Ingesta de Logs | Servicio orientado a la recolección, agregación y movimiento masivo de datos de *logs* hacia HDFS. |
| **Apache ZooKeeper** | Coordinación de Clúster | Servicio centralizado para el mantenimiento de configuraciones, sincronización y alta disponibilidad en sistemas distribuidos. |
| **Apache Sqoop** | Transferencia de Datos | Herramienta de transferencia bidireccional eficiente entre Hadoop y bases de datos relacionales (MySQL, Oracle, etc.). |
| **Apache Oozie** | Orquestación / *Workflow* | Sistema para programar y orquestar flujos de trabajo (*workflows*) complejos entre múltiples componentes de Hadoop. |
| **Apache Mahout** | *Machine Learning* | Biblioteca escalable de algoritmos de aprendizaje automático para clasificación, recomendación y agrupamiento. |
| **Apache Storm** | *Streaming* en Tiempo Real | Sistema distribuido enfocado en el procesamiento de flujos continuos de datos en tiempo real. |
| **Apache NiFi** | Automatización de Flujos | Plataforma con interfaz gráfica para diseñar, automatizar y controlar el flujo y transformación de datos entre sistemas. |
| **Apache Tez** | Motor de Ejecución de Tareas | *Framework* optimizado para la ejecución de grafos de procesamiento dirigidos, con mayor rendimiento que MapReduce. |
| **Apache Drill** | Motor SQL Interactivo | Motor de consultas SQL distribuidas sobre datos no estructurados o semiestructurados (JSON, Parquet, CSV) sin esquema previo. |
| **Apache Atlas** | Gobernanza de Datos | Marco de gobernanza, catalogación y seguimiento del linaje de metadatos en entornos Hadoop. |
| **Apache Zeppelin** | Cuadernos Interactivos | *Notebook* interactivo colaborativo para análisis exploratorio, visualización y desarrollo con Spark, Hive, Python, etc. |
| **Apache Ranger** | Seguridad y Auditoría | *Framework* de seguridad para la administración centralizada de directivas de control de acceso y auditoría. |
| **Apache Ambari** | Gestión y Monitorización | Herramienta visual orientada al aprovisionamiento, gestión, configuración y supervisión operativa del clúster. |
| **Apache Kylin** | Motor OLAP | Motor analítico en línea (OLAP) de baja latencia diseñado para procesar consultas multidimensionales sobre Hadoop. |
| **Apache Phoenix** | Capa SQL sobre HBase | Motor relacional SQL de baja latencia que opera de forma nativa sobre tablas HBase. |
| **Apache Flink** | Procesamiento de *Streams* | Framework para el procesamiento de flujos continuos (*streaming*) en tiempo real y por lotes a gran escala. |
| **Apache Knox** | Pasarela de Seguridad | *Gateway* perimetral que centraliza y securiza el acceso web y API a los servicios del clúster. |
| **Apache Superset** | Visualización de Datos | Plataforma moderna de exploración y visualización de datos para la confección de cuadros de mando interactivos. |



### 2.6.- Problemas que resuelve Apache Hadoop

Apache Hadoop soluciona las limitaciones tradicionales del procesamiento de datos abordando los siguientes aspectos clave:

- **Escalabilidad Horizontal:** Permite escalar la infraestructura añadiendo nodos económicos convencionales al clúster, absorbiendo grandes volúmenes de datos sin requerir hardware vertical privativo.
- **Almacenamiento Distribuido:** HDFS divide los ficheros en bloques y los almacena en los nodos de datos (*DataNodes*) bajo la gestión del nodo maestro (*NameNode*), garantizando redundancia y alta disponibilidad.
- **Procesamiento Paralelo:** El nodo maestro (*Master*) coordina la división de tareas entre múltiples nodos de trabajo (*Workers*), ejecutando las operaciones computacionales de forma concurrente.
- **Tolerancia a Fallos:** Mediante la replicación automática de bloques y la reasignación de tareas que presenten errores, el sistema garantiza continuidad sin requerir procesos tradicionales de copia de seguridad continua.
- **Flexibilidad en el Tratamiento de Datos:** Capacidad nativa para procesar simultáneamente datos estructurados, semiestructurados (JSON, XML) y no estructurados (vídeo, imágenes, logs, texto).
- **Reducción de Costes:** Al basarse en código abierto y apoyarse sobre *commodity hardware*, democratiza el análisis masivo de datos reduciendo la inversión frente a soluciones propietarias.


## 3. Amazon Web Services (AWS): ¿Qué es?

### 3.1.- Definición y concepto

**Amazon Web Services (AWS)** es la plataforma de computación en la nube más adoptada del mundo. Consiste en una infraestructura global de centros de datos repartidos por todo el planeta que Amazon ofrece bajo un modelo de alquiler a empresas y particulares. AWS funciona como un ecosistema integral de servicios gestionados que permite almacenar y procesar petabytes de información sin necesidad de invertir en hardware local.


### 3.2.- Pilares del modelo Cloud

La computación en la nube en AWS se fundamenta en tres principios esenciales:

1. **Pago por uso (*Pay-as-you-go*):** Los costes se facturan estrictamente en función de los recursos utilizados (por ejemplo, segundos de computación o Gigabytes de almacenamiento). Se debe tener en cuenta que los recursos encendidos consumen saldo de manera continuada aun cuando permanezcan inactivos.
2. **Elasticidad:** Capacidad de escalar (sumar potencia o instancias) o desescalar (reducir recursos) de manera automática e instantánea en respuesta a la demanda.
3. **Agilidad:** Permite el despliegue de infraestructuras complejas (como clústeres de bases de datos) en cuestión de minutos a través de la consola web o mediante Infraestructura como Código (IaC), sustituyendo las semanas o meses del método de adquisición tradicional.


### 3.3.- Infraestructura global de AWS

La infraestructura física de AWS se organiza en tres niveles conceptuales:

- **Regiones:** Zonas geográficas aisladas e independientes en diferentes partes del mundo, delimitadas para garantizar proximidad a los usuarios y cumplir con normativas de protección de datos.
- **Zonas de Disponibilidad (AZ - *Availability Zones*):** Conjunto de uno o varios centros de datos físicos ubicados dentro de una región, distanciados geográficamente pero enlazados mediante fibra de muy baja latencia. La alta disponibilidad exige replicar los servicios en al menos dos AZs distintas.
- **Puntos de Presencia (*Edge Locations*):** Centros de datos de menor envergadura distribuidos mundialmente para almacenar contenido en caché y mitigar la latencia de acceso.


### 3.4.- Modelo de responsabilidad compartida

Marco que define los límites de seguridad y cumplimiento legal entre el proveedor y el cliente:

- **Seguridad DE la nube (Responsabilidad de AWS):** Protección de la infraestructura física (servidores, cableado, centros de datos) y del software fundamental (hipervisores, capa de virtualización).
- **Seguridad EN la nube (Responsabilidad del usuario):** Todo aquello que el cliente despliega y configura dentro de la plataforma. Incluye:
  * Gestión de identidades y accesos mediante AWS IAM.
  * Cifrado de datos en reposo y en tránsito (por ejemplo, en S3).
  * Configuración, mantenimiento y actualización del sistema operativo y aplicaciones en máquinas virtuales (EC2).



### 3.5.- Historia de AWS

- **1994:** Jeff Bezos funda Amazon (inicialmente llamada Cadabra) en Seattle, operando exclusivamente como una tienda online de libros.
- **Principios de 2000:** El rápido crecimiento comercial genera problemas operativos en su infraestructura, requiriendo diseñar arquitecturas tecnológicas desde cero en cada proyecto.
- **Reorganización interna:** La compañía rediseñó sus sistemas desacoplando los equipos y las aplicaciones, pasando a comunicarse exclusivamente mediante interfaces de programación (APIs) documentadas.
- **2006:** Tras dominar la operativa de infraestructuras distribuidas masivas, Amazon lanza comercialmente **AWS** para ofrecer almacenamiento y computación bajo un modelo de servicio público. En la actualidad, cuenta con más de 200 servicios que abarcan computación, bases de datos, analítica, redes, inteligencia artificial y herramientas de desarrollo.



### 3.6.- Servicios de AWS para Big Data

Amazon AWS ha ido creciendo a lo largo de los años hasta tener decenas de servicios de todo tipo. En la siguiente tabla se muestran algunos de los más relevantes.


| Servicio | Tipo / Propósito | Descripción funcional |
| --- | --- | --- |
| **Amazon S3** *(Simple Storage Service)* | Almacenamiento de Objetos / *Data Lake* | Almacenamiento virtualmente infinito y de bajo coste con durabilidad del 99,999999999% (11 nueves). Admite datos estructurados y no estructurados, sirviendo de base para los *Data Lakes* al desvincular el almacenamiento del cómputo. |
| **Amazon EC2** *(Elastic Cloud Compute)* | Computación / Máquinas Virtuales | Alquiler de instancias virtuales bajo demanda en minutos. Dispone de gran variedad de configuraciones (CPU, RAM, GPU) y escalado automático (*Auto Scaling*) para absorber cargas de trabajo masivas. |
| **Amazon EMR** *(Elastic MapReduce)* | Procesamiento Distribuido Gestionado | Automatiza el despliegue de clústeres de Hadoop y Spark sobre instancias EC2 utilizando Amazon S3 como capa de almacenamiento. Permite crear clústeres efímeros y destruirlos tras la ejecución a muy bajo coste. |
| **Amazon DynamoDB** | Base de Datos NoSQL (Clave-Valor) | Base de datos NoSQL gestionada con latencia de milisegundos a cualquier escala. Distribuye los datos en particiones físicas mediante una clave de partición y escala horizontalmente sin administrar servidores. |
| **Amazon Redshift** | *Data Warehouse* / Base de Datos Columnar | Base de datos relacional columnar optimizada para operaciones analíticas complejas (OLAP) y consultas SQL sobre miles de millones de filas mediante procesamiento paralelo en clúster. |
| **AWS Lambda** | Computación *Serverless* / FaaS *(Function as a Service)* | Ejecuta código ante eventos sin necesidad de aprovisionar ni administrar servidores, facturando por los milisegundos de cómputo utilizados. En Big Data se aplica a flujos ligeros en tiempo real, validación y limpieza en pipelines. |
| **Amazon Athena** | Motor de Consultas SQL *Serverless* | Motor interactivo para realizar consultas SQL estándar directamente sobre datos almacenados en S3 (en formatos como CSV, JSON, Parquet u ORC) sin aprovisionar clústeres. |
| **AWS Glue** | Integración de Datos / ETL *Serverless* | Servicio administrado para la preparación, transformación y movimiento de datos (ETL). Integra el *Glue Data Catalog* (metadatos), *Glue Crawlers* (inferencia automática de esquemas) y *ETL Jobs* (procesamiento masivo basado en Apache Spark).|



## 4. Preparación del Entorno

### 4.1. Entorno Cloud: AWS Academy

Para las prácticas de laboratorio en la nube se utiliza la plataforma **AWS Academy** mediante el entorno formativo **Learners Lab**:

- **Saldo:** Cada curso asigna un crédito de **50 $** para el uso de servicios de AWS.
- **Sesiones temporales:** Los laboratorios cuentan con un tiempo máximo de sesión continuada de **4 horas**; superado ese límite, el entorno se pausa automáticamente.
- **Credenciales de acceso:** La sección *AWS Details* suministra los tokens temporales (`aws_access_key_id`, `aws_secret_access_key` y `aws_session_token`) necesarios para autenticar la consola de comandos AWS CLI y SDKs de desarrollo.


### 4.2. Entorno Local: Docker y Repositorios

La configuración del entorno de trabajo local requiere:

- **Cuenta en GitHub:** Necesaria para la gestión y entrega de prácticas.
- **Docker / Docker Desktop:** Plataforma de contenedores para instanciar servidores y bases de datos locales.
