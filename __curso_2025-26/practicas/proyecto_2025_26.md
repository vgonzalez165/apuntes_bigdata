
# Proyecto Integrador: Predictor de demanda para redes eléctricas

**Curso de Especialización en IA y Big Data - IES San Andrés - Curso 2025-26**

**Primera fecha de entrega**: 07/05/2026
**Segunda fecha de entrega**: 15/06/2026


## 1. Contexto del Proyecto

La transición energética depende de la capacidad de predecir la demanda eléctrica para optimizar el uso de fuentes renovables. Tu misión en este proyecto será construir un **pipeline de datos híbrido** que recoja información de la Red Eléctrica de España (REE), datos meteorológicos históricos y factores socio-económicos para entrenar un modelo capaz de predecir el consumo eléctrico nacional.

## 2. Objetivos Técnicos

- **Sistemas de Big Data:** configurar una arquitectura de nube híbrida (AWS + Local) gestionando la seguridad y el flujo de datos.
- **Big Data Aplicado:** aplicar la metodología **CRISP-DM** para transformar datos brutos en un modelo predictivo funcional.


## 3. Requisitos de las fuentes de datos

El proyecto debe integrar obligatoriamente tres fuentes:

1. **API ESIOS (Red Eléctrica):** en la [API de Red Eléctrica Nacional](https://www.ree.es/es/datos/apidatos) podrás obtener los datos de demanda real (granularidad horaria).
2. **Histórico climático:** desde la página [datosclima.es](https://datosclima.es/Aemet2013/DescargaDatos.html) podrás obtener históricos en formato **Excel** de los datos publicados por la AEMET desde el año 2013 hasta la actualidad con información sobre temperatura, viento y precipitación.
3. **Fuente de contexto (A elección):** debes buscar e integrar una tercera fuente de datos a tu proyecto, algunas sugerencias de fuentes son:
   1. Datos de calendarios y festivos, ya que el consumo eléctrico cae drásticamente los fines de semana y festivos.
   2. Precios del mercado eléctrico: en la misma API de ESIOS puedes obtener el histórico de precios. Esto te puede ayudar para predecir, no solo la demanda, sino también si el precio subirá cuando la demanda sea alta y la generación de renovable sea baja.
   3. Datos históricos de contaminación atmosférica, hay una correlación indirecta ya que el uso de calefacciones y del tráfico aumenta tanto el consumo energético como la contaminación.


## 4. Fases del proyecto (Metodología CRISP-DM)

En este proyecto seguirás la **metodología CRISP-DM** tal como hemos visto en clase. Con objeto de abarcar diferentes tecnologías vistas en el curso, trabajarás en un entorno híbrido donde la capa bronce se almacenará en un Data Lake en Amazon AWS y las capas plata y oro las gestionarás en local.

Debes seguir todas las fases especificadas en CRISP-DM, aunque las más relevantes para los módulos de Big Data son las tres primeras fases (comprensión de negocio, comprensión de los datos y preparación de los datos), así como la última (despliegue).

Algunos consejos respecto a estas fases:

### Fase I: Comprensión del negocio

Asegúrate de entender bien lo que quieres hacer, cuál es el objetivo final y qué métrica o resultado vas a tener en cuenta para considerarlo un éxito o un fracaso.

### Fase II: Comprensión de los datos

Estudia bien los datos con los que vas a trabajar, determina cuáles te van a ser útiles y cuáles no, identifica las relaciones entre los diferentes datos y, en definitiva, entiende con qué vas a trabajar.


### Fase III: Preparación de los datos

En esta fase es cuando te pondrás ya manos a la obra. Vamos a trabajar utilizandola arquitectura medallón, así que tienes varios pasos:

#### Capa bronce

La capa bronce la implementaremos en Amazon AWS, la idea es que:

- Crees un bucket s3 para alojar los datos
- Desarrolles un **AWS Lambda** en Python que consuma la API de ESIOS y deposite el JSON original en este bucket
- Cargues en este bucket también los datos del clima (manualmente o automatizándolo con un script en Python), así como la tercera fuente de datos que hayas escogido.

#### Capa plata

Esta capa ya la implementaremos en local en nuestro equipo. Sería interesante, aunque no obligatorio, implementar un entorno HSFS para alojar los datos con contenedores.
 Algunas cosas a tener en cuenta:

- **Conexión local-cloud**: utiliza la librería `boto3` para recoger los datos de AWS
- **Almacenamiento**: sería interesante, aunque no obligatorio, que despliegues un entorno HDFS co Docker para alojar los datos de esta capa y de la capa oro.
- **Limpieza y normalización**: a medida que vayas leyendo los datos realiza todas las operaciones de limpieza, normalización y estandarización de los datos.
- **Formato**: no es necesario decir que en esta capa los datos se deben guardar en un formato adecuado, como puede ser Parquet.


#### Capa oro

Una vez que tenemos los datos listos, nos queda la fase de **combinación de fuente** y de **generación de nuevas características**, tras lo cual los almacenaremos en la capa oro.


### Fases IV y V: Modelado y Evaluación

Estas fases se salen del ámbito de los módulos de Big Data, por lo que las omitirás en tu proyecto.



### Fase VI: Despliegue

Aunque no realices las fases anteriores, sí deberás realizar algún tipo de despliegue. Como no hay predicciones el despliegue consistirá en crear un **Dashboard interactivo** con los datos ya limpios.

El contenido exacto de este dashboard os lo diré más adelante.


## 5. Entrega

En este proyecto deberás entregar:

1. **Memoria del proyecto:** documento PDF siguiendo las fases de CRISP-DM.
2. **Código fuente:** repositorio (GitHub/GitLab) con los scripts de AWS Lambda, los notebooks de procesamiento local y el código del Dashboard.
3. **Diccionario de datos:** documentación de las columnas finales de la capa *Gold*.
4. Eventualmente , se podrá realizar una **defensa en clase** del proyecto.



## 6. Criterios de Evaluación


## Módulo: Big Data Aplicado

| Resultado de Aprendizaje (RA) | Criterio de Evaluación (Ítems) | Insuficiente (0-4) | Suficiente/Notable (5-8) | Sobresaliente (9-10) |
| :--- | :--- | :--- | :--- | :--- |
| **RA1. Gestión de soluciones y almacenamiento** | Configuración de la capa Bronce en AWS S3 y uso de herramientas como AWS Lambda para la ingesta. | No usa S3 o la ingesta es manual sin automatización. | Usa S3 y Lambda de forma funcional, aunque con configuración básica. | Configuración óptima de S3 y Lambdas eficientes con gestión de permisos. |
| | Implementación de almacenamiento local (HDFS/Contenedores). | No implementa almacenamiento local estructurado. | Implementa almacenamiento local funcional (Docker/HDFS) de forma básica. | Estructura local robusta, bien documentada y escalable. |
| **RA2. Sistemas de almacenamiento y ecosistema** | Implementación de la arquitectura de Medallón (Bronce, Plata, Oro). | No se distingue el flujo de datos entre capas. | Flujo de datos claro entre capas, aunque con solapamientos menores. | Arquitectura de Medallón perfectamente definida y automatizada. |
| | Uso de formatos eficientes (Parquet) y herramientas del ecosistema (Boto3). | Los formatos no son adecuados (solo CSV/JSON) o no usa Boto3. | Usa Parquet y Boto3 correctamente para el flujo nube-local. | Optimización avanzada de esquemas y particionado en Parquet. |
| **RA4. Seguimiento y monitorización** | Gestión de errores y fiabilidad en el flujo de datos (Logs en Lambda/Scripts). | El sistema falla frecuentemente y no tiene control de errores. | Incluye control de errores básico y logs que permiten trazabilidad. | Sistema altamente fiable con manejo de excepciones y logs detallados. |
| | Estabilidad de la conexión híbrida local-nube. | La conexión es inestable o requiere intervención manual constante. | Conexión funcional y estable mediante credenciales seguras. | Automatización total de la sincronización con alta estabilidad. |
| **RA5. Transformación en información significativa** | Aplicación de la metodología CRISP-DM (Fases I, II y III). | No sigue la metodología o las fases están incompletas. | Sigue las fases correctamente, documentando la comprensión del negocio/datos. | Aplicación rigurosa de CRISP-DM con análisis crítico de los datos. |
| | Calidad de la capa Oro para la toma de decisiones. | La capa Oro no aporta valor o los datos están sucios. | La capa Oro combina fuentes y genera variables útiles. | Capa Oro optimizada con ingeniería de variables (features) de alto valor. |



## Módulo: Sistemas de Big Data

| Resultado de Aprendizaje (RA) | Criterio de Evaluación (Ítems) | Insuficiente (0-4) | Suficiente/Notable (5-8) | Sobresaliente (9-10) |
| :--- | :--- | :--- | :--- | :--- |
| **RA1. Técnicas de análisis e integración** | Integración de las tres fuentes obligatorias (ESIOS, AEMET, 3ª fuente). | Falta alguna fuente obligatoria o no están integradas. | Integra las tres fuentes de forma coherente en un mismo pipeline. | Integración fluida y lógica de múltiples fuentes con alta heterogeneidad. |
| | Procesamiento, limpieza y normalización de datos brutos. | Datos con nulos, duplicados o formatos inconsistentes. | Limpieza adecuada: gestión de nulos, tipos de datos y escalas. | Pipeline de limpieza avanzado (estandarización, imputación técnica). |
| **RA2. Configuración de cuadros de mando** | Conexión del Dashboard con la capa de datos (Gold). | El dashboard usa datos estáticos o manuales. | Dashboard conectado a la capa Oro que se actualiza correctamente. | Arquitectura de visualización profesional y eficiente. |
| | Entorno de ejecución del Dashboard. | El entorno no es adecuado o es difícil de desplegar. | Entorno bien configurado (Streamlit, Dash, etc.) y funcional. | Despliegue impecable con configuración de entorno optimizada. |
| **RA3. Gestión y almacenamiento para búsqueda** | Estructura del Diccionario de Datos de la capa Oro. | No hay diccionario o es ininteligible. | Diccionario completo con nombres de columnas, tipos y descripción. | Documentación técnica exhaustiva de cada variable y su origen. |
| | Organización de los datos para facilitar consultas/análisis. | Los datos están desorganizados y dificultan la visualización. | Datos organizados que permiten consultas rápidas para el dashboard. | Estructura de datos optimizada para analítica (tablas de hechos/dimensiones). |
| **RA4. Herramientas de visualización y presentación** | Calidad visual e interactividad del Dashboard. | Gráficos confusos, sin etiquetas o no interactivos. | Visualización clara con filtros funcionales y leyendas adecuadas. | Dashboard profesional, intuitivo y con gran capacidad de storytelling. |
| | Capacidad de análisis y presentación de resultados en la defensa. | No explica bien el flujo de datos o los resultados. | Explica con claridad el proceso técnico y el valor de los datos. | Defensa brillante con justificación técnica de cada decisión tomada. |
