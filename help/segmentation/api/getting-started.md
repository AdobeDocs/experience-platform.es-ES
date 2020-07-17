---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador del servicio de segmentación
topic: developer guide
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

El servicio de segmentación por Adobe Experience Platform le permite crear segmentos y generar audiencias en Adobe Experience Platform a partir de sus [!DNL Real-time Customer Profile] datos.

La guía para desarrolladores requiere una comprensión práctica de los distintos servicios de Experience Platform que se utilizan [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md):: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md):: El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
- [!DNL Real-time Customer Profile](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Simuladores](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para trabajar con la [!DNL Segmentation] API de forma satisfactoria.

## Leer llamadas de API de muestra

La documentación de la [!DNL Segmentation Service] API proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a extremos de Platform. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API de Experience Platform, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la documentación [general de los](../../sandboxes/home.md)entornos limitados.

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

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## Definiciones de segmentos

Las definiciones de segmentos definen qué perfiles formarán parte de cada segmento de audiencia. Puede utilizar el extremo para recuperar una lista de definiciones de segmentos, crear una nueva definición de segmento, recuperar detalles de una definición de segmento específica, eliminar una definición de segmento específica o sobrescribir detalles de una definición de segmento específica. `/segment/definitions`

Para obtener más información sobre el uso de este extremo, lea la guía para desarrolladores de definiciones de [segmentos](./segment-definitions.md).

## Trabajos de segmentos

Los trabajos de segmentos procesan definiciones de segmentos previamente establecidas para generar un segmento de audiencia. Puede utilizar el extremo para recuperar una lista de trabajos de segmentos, crear un nuevo trabajo de segmento, recuperar detalles de un trabajo de segmento específico o eliminar un trabajo de segmento específico. `/segment/jobs`

Para obtener más información sobre el uso de este extremo, lea la guía para desarrolladores de trabajos de [segmentos](./segment-jobs.md).

## Búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar e indexar campos configurables contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Para empezar a trabajar con la búsqueda de segmentos, consulte la guía para desarrolladores de [búsquedas](segment-search.md)

## Pasos siguientes

Para realizar llamadas mediante la [!DNL Segmentation Service] API, seleccione una de las guías de punto final disponibles mediante el panel de navegación izquierdo o en la información general de la guía del [desarrollador](./overview.md)