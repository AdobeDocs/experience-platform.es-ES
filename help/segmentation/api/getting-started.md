---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador del servicio de segmentación
topic: developer guide
translation-type: tm+mt
source-git-commit: e25ce403034a94d7024e8c244cb438bd9dfe0c5f
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Guía del desarrollador del servicio de segmentación

La segmentación le permite crear segmentos y generar audiencias en Adobe Experience Platform a partir de los datos de Perfil del cliente en tiempo real.

## Primeros pasos

Esta guía requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform relacionados con el uso de la segmentación.

- [Segmentación](../home.md): Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para utilizar la segmentación con éxito mediante la API.

### Leer llamadas de API de muestra

La documentación de la API del servicio de segmentación proporciona llamadas de API de ejemplo para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a extremos de plataforma. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre cómo trabajar con entornos limitados en la plataforma de experiencia, consulte la documentación [general de los](../../sandboxes/home.md)entornos limitados.

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos previamente establecidas para generar un segmento de audiencia. Puede utilizar el extremo para recuperar una lista de trabajos de segmentos, crear un nuevo trabajo de segmento, recuperar detalles de un trabajo de segmento específico o eliminar un trabajo de segmento específico. `/segment/jobs`

Para obtener más información sobre el uso de este extremo, lea la guía para desarrolladores de trabajos de [segmentos](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar e indexar campos configurables contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para empezar a trabajar con la búsqueda de segmentos, consulte la guía para desarrolladores de [búsquedas](segment-search.md)

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de segmentación, seleccione una de las subguías para aprender a utilizar los extremos específicos relacionados con la segmentación. Para obtener más información sobre cómo trabajar con segmentos mediante la interfaz de usuario de la plataforma, consulte la guía [del usuario](../ui/overview.md)Segmentación.