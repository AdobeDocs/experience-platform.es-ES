---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador del servicio de segmentación
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
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

## Pasos siguientes

Para realizar llamadas mediante la [!DNL Segmentation Service] API, seleccione una de las guías de punto final disponibles mediante el panel de navegación izquierdo o en la información general de la guía del [desarrollador](./overview.md)