---
keywords: Experience Platform;servicio de consultas;servicio de consultas;consulta
title: Introducción al servicio de consultas de Adobe Experience Platform
description: Un desglose de los pasos necesarios para utilizar completamente Adobe Experience Platform Query Service
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Introducción a Adobe Experience Platform [!DNL Query Service] {#getting-started}

Utilice el servicio de consulta de Adobe Experience Platform para ejecutar consultas SQL en conjuntos de datos ingeridos, unir datos de varios orígenes y generar conjuntos de datos derivados para análisis, flujos de trabajo de aprendizaje automático o el perfil del cliente en tiempo real. Después de la ingesta de datos, acceda al servicio de consulta a través de la interfaz de usuario para realizar análisis interactivos y colaborar, o a través de la API para ejecutar consultas de forma automatizada y programática.

## Requisitos previos {#prerequisites}

Antes de empezar a consultar datos, asegúrese de lo siguiente:

- **Permisos necesarios**: su cuenta de usuario tiene acceso al servicio de consultas en Experience Platform. Si el servicio no está disponible en la interfaz de usuario, revise la [documentación de permisos](../../access-control/home.md#permissions) y póngase en contacto con el administrador del sistema.
- **Ingesta de datos**: Se han ingerido datos en Experience Platform.

Si necesita ingerir datos, consulte el [tutorial sobre ingesta de datos en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) para obtener una descripción general de la creación del conjunto de datos, la asignación de esquemas, la ingesta y la validación. Lea la [documentación de información general sobre la ingesta](../../ingestion/home.md) para obtener información detallada y vínculos a otros recursos de aprendizaje.

## Rutas de inicio rápido

Una vez que haya ingerido los datos en Experience Platform, puede empezar a trabajar con el servicio de consultas mediante [!DNL Query Editor] en Experience Platform o la API del servicio de consultas.

### [!DNL Query Editor]

Use [!DNL Query Editor] para análisis, exploración de datos y desarrollo de consultas de colaboración. Para obtener información general sobre la funcionalidad de la interfaz de usuario, consulte la [documentación de la interfaz de usuario del servicio de consultas](../ui/overview.md). Para obtener información sobre cómo escribir y ejecutar consultas en la interfaz de usuario, lea la [[!DNL Query Editor user guide]](../ui/user-guide.md).

### API del servicio de consultas

Utilice la API del servicio de consulta para flujos de trabajo automatizados, administración de plantillas de consulta e integraciones programáticas. Consulte la [Guía para desarrolladores de Query Service](../api/getting-started.md) para obtener instrucciones detalladas sobre el uso de la API de Query Service.

## Pasos siguientes

Este documento cubre los requisitos previos necesarios para usar las características de [!DNL Query Service] en Experience Platform. Para empezar a utilizar rápidamente las funciones del servicio de consultas, se recomienda leer los siguientes documentos:

- [Directrices generales para la ejecución de consultas](../best-practices/writing-queries.md)
- [Sintaxis SQL en el servicio de consultas](../sql/syntax.md)
- [Crear conjuntos de datos derivados con SQL](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

Si lo prefiere, puede obtener más información sobre cómo Query Service beneficia al procesamiento de datos en Experience Platform y ver la [presentación del caso de uso del explorador abandonado](../use-cases/abandoned-browse.md#video-example).

Los siguientes recursos son útiles para que entienda mejor [!DNL Query Service]:

- [[!DNL Query Service] Información general de IU](../ui/overview.md)
- [Credenciales de [!DNL Query Service]](../ui/credentials.md)
- [Información general sobre las conexiones de cliente](../clients/overview.md)
