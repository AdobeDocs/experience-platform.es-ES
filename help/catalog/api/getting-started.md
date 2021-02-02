---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;Catálogo
solution: Experience Platform
title: Guía del desarrollador del servicio de catálogo
topic: developer guide
description: En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio mediante la API de catálogo. A continuación, la guía proporciona llamadas de API de muestra para realizar operaciones clave mediante el catálogo.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# [!DNL Catalog Service] guía para desarrolladores

[!DNL Catalog Service] es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. [!DNL Catalog] actúa como un almacén de metadatos o un &quot;catálogo&quot; donde puede encontrar información sobre sus datos dentro de  [!DNL Experience Platform], sin necesidad de acceder a los datos mismos. Consulte la [[!DNL Catalog] información general](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona pasos para ayudarle a realizar inicios mediante la API [!DNL Catalog]. A continuación, la guía proporciona ejemplos de llamadas de API para realizar operaciones clave mediante [!DNL Catalog].

## Requisitos previos

[!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones dentro de  [!DNL Experience Platform]. Esta guía para desarrolladores requiere una comprensión práctica de los diversos [!DNL Experience Platform] servicios que intervienen en la creación y administración de estos recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
* [Ingesta](../../ingestion/batch-ingestion/overview.md) por lotes: Cómo  [!DNL Experience Platform] ingesta y almacena datos de archivos de datos, como CSV y Parquet.
* [Transmisión por secuencias](../../ingestion/streaming-ingestion/overview.md): Cómo  [!DNL Experience Platform] ingesta y almacena datos desde dispositivos del lado del cliente y del servidor en tiempo real.

Las siguientes secciones proporcionan información adicional que deberá conocer o tener disponible para realizar llamadas exitosas a la API [!DNL Catalog Service].

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Prácticas recomendadas para llamadas de API [!DNL Catalog]

Al realizar solicitudes de GET a la API [!DNL Catalog], se recomienda incluir parámetros de consulta en las solicitudes para devolver solo los objetos y las propiedades que necesite. Las solicitudes sin filtrar pueden hacer que las cargas de respuesta superen los 3 GB de tamaño, lo que puede ralentizar el rendimiento general.

Puede realizar la vista de objetos específicos incluyendo su ID en la ruta de la solicitud o utilizando parámetros de consulta como `properties` y `limit` para filtrar las respuestas. Los filtros se pueden pasar como encabezados y como parámetros de consulta, y los que se pasan como parámetros de consulta tienen prioridad. Consulte el documento sobre [filtrado de datos del catálogo](filter-data.md) para obtener más información.

Dado que algunas consultas pueden suponer una carga pesada para la API, se han implementado límites globales en las [!DNL Catalog] consultas para seguir soportando las mejores prácticas.

## Pasos siguientes

Este documento cubría los conocimientos previos necesarios para realizar llamadas a la API [!DNL Catalog]. Ahora puede continuar con las llamadas de muestra que se proporcionan en esta guía para desarrolladores y seguir sus instrucciones.

La mayoría de los ejemplos de esta guía utilizan el extremo `/dataSets`, pero los principios pueden aplicarse a otros extremos dentro de [!DNL Catalog] (como `/batches` y `/accounts`). Consulte la [referencia de API de servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para obtener una lista completa de todas las llamadas y operaciones disponibles para cada extremo.

Para ver un flujo de trabajo paso a paso que muestra cómo la API [!DNL Catalog] está involucrada con la ingestión de datos, consulte el tutorial sobre [la creación de un conjunto de datos](../datasets/create.md).
