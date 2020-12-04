---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: Guía del desarrollador del servicio de catálogo
topic: developer guide
description: En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio mediante la API de catálogo. A continuación, la guía proporciona llamadas de API de muestra para realizar operaciones clave mediante el catálogo.
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# [!DNL Catalog Service] guía para desarrolladores

[!DNL Catalog Service] es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. [!DNL Catalog] actúa como un almacén de metadatos o un &quot;catálogo&quot; donde puede encontrar información sobre sus datos dentro de [!DNL Experience Platform], sin necesidad de acceder a los datos mismos. See the [[!DNL Catalog] overview](../home.md) for more information.

En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio del uso de la [!DNL Catalog] API. A continuación, la guía proporciona ejemplos de llamadas de API para realizar operaciones clave mediante [!DNL Catalog].

## Requisitos previos 

[!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones dentro de [!DNL Experience Platform]. Esta guía para desarrolladores requiere un conocimiento práctico de los distintos [!DNL Experience Platform] servicios que se utilizan para crear y administrar estos recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
* [Ingesta](../../ingestion/batch-ingestion/overview.md)por lotes: Cómo [!DNL Experience Platform] ingesta y almacena datos de archivos de datos, como CSV y Parquet.
* [Transmisión por secuencias](../../ingestion/streaming-ingestion/overview.md): Cómo [!DNL Experience Platform] ingesta y almacena datos de dispositivos del lado del cliente y del servidor en tiempo real.

Las siguientes secciones proporcionan información adicional que deberá conocer o tener disponible para realizar llamadas a la [!DNL Catalog Service] API correctamente.

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

## Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Prácticas recomendadas para llamadas [!DNL Catalog] de API

Al realizar solicitudes de GET a la [!DNL Catalog] API, se recomienda incluir parámetros de consulta en las solicitudes para devolver solo los objetos y las propiedades que necesite. Las solicitudes sin filtrar pueden hacer que las cargas de respuesta superen los 3 GB de tamaño, lo que puede ralentizar el rendimiento general.

Puede realizar la vista de objetos específicos incluyendo su ID en la ruta de la solicitud o utilizando parámetros de consulta como `properties` y `limit` para filtrar las respuestas. Los filtros se pueden pasar como encabezados y como parámetros de consulta, y los que se pasan como parámetros de consulta tienen prioridad. Consulte el documento sobre el [filtrado de datos](filter-data.md) del catálogo para obtener más información.

Dado que algunas consultas pueden suponer una carga pesada para la API, se han implementado límites globales en [!DNL Catalog] consultas para admitir más prácticas recomendadas.

## Pasos siguientes

Este documento cubría los conocimientos previos necesarios para realizar llamadas a la [!DNL Catalog] API. Ahora puede continuar con las llamadas de muestra que se proporcionan en esta guía para desarrolladores y seguir sus instrucciones.

La mayoría de los ejemplos de esta guía utilizan el `/dataSets` punto final, pero los principios pueden aplicarse a otros puntos finales dentro de [!DNL Catalog] (como `/batches` y `/accounts`). Consulte la referencia [de la API del servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catálogo para obtener una lista completa de todas las llamadas y operaciones disponibles para cada extremo.

Para ver un flujo de trabajo paso a paso que muestra cómo la [!DNL Catalog] API participa en la ingestión de datos, consulte el tutorial sobre la [creación de un conjunto de datos](../datasets/create.md).
