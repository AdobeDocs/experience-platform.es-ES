---
title: Notas de la versión de Adobe Experience Platform, junio de 2022
description: Notas de la versión de junio de 2022 para Adobe Experience Platform.
source-git-commit: 4edd2042234149ab8836da4fc58eb4d6084ae205
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 22 de junio de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations es ahora más inteligente y rápido. Las nuevas comprobaciones de validación reducen considerablemente los errores de asignación más comunes, lo que reduce el tiempo de respuesta al valor. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para liberar perspectivas de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe. Una de las formas en que Data Science Workspace lo consigue es mediante el uso de JupyterLab. JupyterLab es una interfaz de usuario basada en web para <a href="https://jupyter.org/" target="_blank">Júpiter del proyecto</a> y está estrechamente integrado en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con portátiles, código y datos de Jupyter.

| Función | Descripción |
| --- | --- |
| JupyterLab Launcher | El JupyterLab Launcher ahora incluye el inicio de las laptops Spark 3.2. Los inicios de los portátiles Spark 2.4 ahora se sustituyen por portátiles Spark 3.2 y formarán parte de esta versión. |
| Spark 3.2 | Las nuevas recetas Scala (Spark) y PySpark ahora utilizan Spark 3.2 |
| Kernels | Los portátiles Scala (Spark) ahora se crean a través del núcleo Scala. Los portátiles PySpark ahora se crean a través del núcleo Python. El núcleo Spark y PySpark están en desuso y configurados para ser eliminados en una versión posterior. |
| Fórmulas | Las nuevas fórmulas PySpark y Spark ahora siguen el flujo de trabajo Docker de forma similar a las recetas Python y R. |

{style=&quot;table-layout:auto&quot;}

Para obtener información más general sobre Data Science Workspace, consulte la [documentación general](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| (Beta) compatibilidad con Destination SDK para [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) destinos basados en archivos y [nombres de archivo configurables](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | Ahora puede utilizar el Destination SDK para crear destinos de Google Cloud Storage y definir nombres de archivo personalizados para archivos exportados mediante macros de nombre de archivo. <br><br> La compatibilidad con destinos basados en archivos en Adobe Experience Platform Destination SDK actualmente está en versión beta. La documentación y la funcionalidad están sujetas a cambios. |

{style=&quot;table-layout:auto&quot;}

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | La variable [!DNL Google Ad Manager 360] la conexión habilita la carga por lotes para [!DNL publisher provided identifiers] (PPID) en [!DNL Google Ad Manager 360], a través de [!DNL Google Cloud Storage] <br><br>Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la [!DNL Google Ad Manager 360] conexión, póngase en contacto con su representante de Adobe y proporcione su [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Active perfiles para encuestas de Medallia dirigidas y recopilación de comentarios para comprender mejor las necesidades y expectativas de los clientes. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) el destino le permite compartir segmentos de origen autenticados con anunciantes y usuarios aprobados para la activación de campañas con DSP. |

{style=&quot;table-layout:auto&quot;}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Etiquetado de esquemas ad hoc | Administre el acceso a los datos confidenciales aplicando etiquetas a los campos de datos de esquemas ad hoc que se generan automáticamente a través de las cuotas de servicio de consulta. Puede restringir el uso de ciertos campos o conjuntos de datos de esquemas específicos para controlar el acceso a datos personales confidenciales e información personal identificable. Mediante la capacidad de control de acceso basado en atributos puede etiquetar campos de esquema específicos a través de la interfaz de usuario de Platform. |
| `FLATTEN` configuración | Al conectarse a una base de datos mediante herramientas de BI de terceros, la variable `FLATTEN` esta configuración aplana las estructuras de datos anidadas en columnas independientes, donde el nombre del atributo se convierte en el nombre de columna que contiene los valores de fila. Esto mejora la facilidad de uso de los esquemas específicos y reduce la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos en herramientas de BI que no admiten estructuras de datos anidadas. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los servicios de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Lanzamiento beta de [!DNL Mixpanel] source | Ahora puede usar la variable [!DNL Mixpanel] fuente para introducir datos de análisis de su [!DNL Mixpanel] cuenta al Experience Platform. Consulte la [[!DNL Mixpanel] documentación de origen](../../sources/connectors/analytics/mixpanel.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
