---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;catálogo;servicio de catálogo;catálogo
solution: Experience Platform
title: Guía de API del servicio de catálogo
topic-legacy: developer guide
description: La API del servicio de catálogo permite a los desarrolladores administrar metadatos de conjuntos de datos en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# [!DNL Catalog Service] Guía de API

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. [!DNL Catalog] actúa como un almacén de metadatos o un &quot;catálogo&quot; donde puede encontrar información sobre sus datos dentro de  [!DNL Experience Platform], sin necesidad de acceder a los datos en sí. Consulte [[!DNL Catalog] overview](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona pasos para ayudarle a empezar a utilizar la API [!DNL Catalog]. A continuación, la guía proporciona ejemplos de llamadas de API para realizar operaciones clave mediante [!DNL Catalog].

## Requisitos previos

[!DNL Catalog] rastrea metadatos para varios tipos de recursos y operaciones dentro de  [!DNL Experience Platform]. Esta guía para desarrolladores requiere comprender bien los distintos [!DNL Experience Platform] servicios relacionados con la creación y administración de estos recursos:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.
* [Ingesta por lotes](../../ingestion/batch-ingestion/overview.md): Cómo  [!DNL Experience Platform] se introducen y almacenan datos de archivos de datos, como CSV y Parquet.
* [ingesta](../../ingestion/streaming-ingestion/overview.md) de transmisión: Cómo  [!DNL Experience Platform] ingesta y almacena datos de dispositivos del lado del cliente y del servidor en tiempo real.

Las secciones siguientes proporcionan información adicional que debe conocer o tener disponible para realizar llamadas correctamente a la API [!DNL Catalog Service] .

## Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Prácticas recomendadas para llamadas de API [!DNL Catalog]

Al realizar solicitudes de GET a la API [!DNL Catalog], se recomienda incluir parámetros de consulta en las solicitudes para devolver solo los objetos y las propiedades que necesite. Las solicitudes sin filtrar pueden hacer que las cargas de respuesta superen los 3 GB de tamaño, lo que puede ralentizar el rendimiento general.

Puede ver objetos específicos incluyendo su ID en la ruta de la solicitud o utilizando parámetros de consulta como `properties` y `limit` para filtrar las respuestas. Los filtros se pueden pasar como encabezados y como parámetros de consulta, con prioridad para los que se pasan como parámetros de consulta. Consulte el documento sobre [filtrado de datos del catálogo](filter-data.md) para obtener más información.

Dado que algunas consultas pueden suponer una carga pesada para la API, se han implementado límites globales en las [!DNL Catalog] consultas para admitir más prácticas recomendadas.

## Pasos siguientes

Este documento abarcaba los conocimientos previos necesarios para realizar llamadas a la API [!DNL Catalog]. Ahora puede continuar con las llamadas de ejemplo que se proporcionan en esta guía para desarrolladores y seguir junto con sus instrucciones.

La mayoría de los ejemplos de esta guía utilizan el extremo `/dataSets` , pero los principios se pueden aplicar a otros extremos dentro de [!DNL Catalog] (como `/batches` y `/accounts`). Consulte la [Referencia de la API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para obtener una lista completa de todas las llamadas y operaciones disponibles para cada extremo.

Para ver un flujo de trabajo paso a paso que muestre cómo la API [!DNL Catalog] está implicada en la ingesta de datos, consulte el tutorial sobre la [creación de un conjunto de datos](../datasets/create.md).
