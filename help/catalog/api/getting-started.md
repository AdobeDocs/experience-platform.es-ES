---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;catálogo
solution: Experience Platform
title: Guía de API del servicio de catálogo
description: La API del servicio de catálogo permite a los desarrolladores administrar los metadatos del conjunto de datos en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 23%

---

# Guía de la API de [!DNL Catalog Service]

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. [!DNL Catalog] actúa como un almacén de metadatos o &quot;catálogo&quot; en el que puede encontrar información acerca de sus datos en [!DNL Experience Platform], sin necesidad de tener acceso a los propios datos. Consulte la [[!DNL Catalog] descripción general](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de [!DNL Catalog]. A continuación, la guía proporciona llamadas de API de ejemplo para realizar operaciones clave mediante [!DNL Catalog].

## Requisitos previos

[!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones dentro de [!DNL Experience Platform]. Esta guía para desarrolladores requiere una comprensión práctica de los distintos servicios de [!DNL Experience Platform] implicados en la creación y administración de estos recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.
* [Ingesta por lotes](../../ingestion/batch-ingestion/overview.md): Cómo [!DNL Experience Platform] ingiere y almacena datos de archivos de datos, como CSV y Parquet.
* [Ingesta de transmisión](../../ingestion/streaming-ingestion/overview.md): Cómo [!DNL Experience Platform] ingiere y almacena datos de dispositivos del lado del cliente y del lado del servidor en tiempo real.

Las secciones siguientes proporcionan información adicional que necesitará saber o tener disponible para realizar llamadas correctamente a la API [!DNL Catalog Service].

## Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

## Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Prácticas recomendadas para llamadas a la API [!DNL Catalog]

Al realizar solicitudes de GET a la API [!DNL Catalog], se recomienda incluir parámetros de consulta en las solicitudes para devolver únicamente los objetos y las propiedades que necesite. Las solicitudes sin filtrar pueden hacer que las cargas de respuesta superen los 3 GB de tamaño, lo que puede ralentizar el rendimiento general.

Puede ver objetos específicos incluyendo su ID en la ruta de solicitud o usar parámetros de consulta como `properties` y `limit` para filtrar las respuestas. Los filtros se pueden pasar como encabezados y como parámetros de consulta, y los que se pasan como parámetros de consulta tienen prioridad. Consulte el documento sobre [filtrado de datos de catálogo](filter-data.md) para obtener más información.

Dado que algunas consultas pueden cargar gravemente la API, se han implementado límites globales en [!DNL Catalog] consultas para admitir aún más las prácticas recomendadas.

## Pasos siguientes

Este documento cubría los conocimientos previos necesarios para realizar llamadas a la API de [!DNL Catalog]. Ahora puede continuar con las llamadas de muestra que se proporcionan en esta guía para desarrolladores y seguir junto con sus instrucciones.

La mayoría de los ejemplos de esta guía utilizan el extremo `/dataSets`, pero los principios se pueden aplicar a otros extremos dentro de [!DNL Catalog] (como `/batches`). Consulte la [Referencia de la API del servicio de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/) para obtener una lista completa de todas las llamadas y operaciones disponibles para cada extremo.

Para obtener un flujo de trabajo paso a paso que muestra cómo la API [!DNL Catalog] está implicada en la ingesta de datos, consulte el tutorial sobre [creación de un conjunto de datos](../datasets/create.md).
