---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador del servicio de catálogo
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Guía del desarrollador del servicio de catálogo

El servicio de catálogo es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. El catálogo actúa como almacén de metadatos o &quot;catálogo&quot;, donde puede encontrar información sobre sus datos en Experience Platform, sin necesidad de acceder a los datos en sí. Consulte la información general [del](../home.md) catálogo para obtener más información.

En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio mediante la API de catálogo. A continuación, la guía proporciona llamadas de API de muestra para realizar operaciones clave mediante el catálogo.

## Requisitos previos

El catálogo realiza un seguimiento de los metadatos de varios tipos de recursos y operaciones dentro del Experience Platform. Esta guía para desarrolladores requiere un conocimiento práctico de los diversos servicios de Experience Platform que intervienen en la creación y administración de estos recursos:

* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [Ingesta](../../ingestion/batch-ingestion/overview.md)por lotes: Cómo el Experience Platform ingesta y almacena datos de archivos de datos, como CSV y Parquet.
* [Transmisión por secuencias](../../ingestion/streaming-ingestion/overview.md): Cómo el Experience Platform ingiere y almacena datos desde dispositivos del lado del cliente y del servidor en tiempo real.

Las secciones siguientes proporcionan información adicional que deberá conocer o tener disponible para realizar llamadas correctamente a la API del servicio de catálogo.

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de Platform, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Prácticas recomendadas para llamadas de API de catálogo

Al realizar solicitudes GET a la API de catálogo, se recomienda incluir parámetros de consulta en las solicitudes para devolver solo los objetos y las propiedades que necesite. Las solicitudes sin filtrar pueden hacer que las cargas de respuesta superen los 3 GB de tamaño, lo que puede ralentizar el rendimiento general.

Puede realizar la vista de objetos específicos incluyendo su ID en la ruta de la solicitud o utilizando parámetros de consulta como `properties` y `limit` para filtrar las respuestas. Los Filtros se pueden pasar como encabezados y como parámetros de consulta, y los que se pasan como parámetros de consulta tienen prioridad. Consulte el documento sobre el [filtrado de datos](filter-data.md) del catálogo para obtener más información.

Dado que algunas consultas pueden suponer una carga pesada para la API, se han implementado límites globales en las consultas del catálogo para admitir más prácticas recomendadas.

## Pasos siguientes

Este documento cubría los conocimientos previos necesarios para realizar llamadas a la API de catálogo. Ahora puede continuar con las llamadas de muestra que se proporcionan en esta guía para desarrolladores y seguir sus instrucciones.

La mayoría de los ejemplos de esta guía utilizan el `/dataSets` punto final, pero los principios pueden aplicarse a otros puntos finales del catálogo (como `/batches` y `/accounts`). Consulte la referencia [de la API del servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catálogo para obtener una lista completa de todas las llamadas y operaciones disponibles para cada extremo.

Para ver un flujo de trabajo paso a paso que muestra cómo la API de catálogo participa en la ingestión de datos, consulte el tutorial sobre la [creación de un conjunto de datos](../datasets/create.md).
