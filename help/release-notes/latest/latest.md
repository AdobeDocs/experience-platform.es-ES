---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 56d43d93be7aca059a38e9428ad5680dd52ad6f9
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 22 de junio de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

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
