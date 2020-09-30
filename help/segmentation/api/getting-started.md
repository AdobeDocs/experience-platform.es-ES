---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Guía para desarrolladores del servicio de segmentación
topic: developer guide
description: La siguiente documentación proporciona información adicional que debe conocer para trabajar correctamente con la API de segmentación.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite crear segmentos y generar audiencias en Adobe Experience Platform a partir de sus [!DNL Real-time Customer Profile] datos.

La guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Experience Platform] servicios que se utilizan [!DNL Segmentation Service].

- [[!Segmentación DNL]](../home.md): Permite generar segmentos de audiencia a partir de [!DNL Real-time Customer Profile] datos.
- [Sistema de modelo de datos de experiencia (XDM) [!DNL]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Simuladores](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para trabajar con la [!DNL Segmentation] API de forma satisfactoria.

## Leer llamadas de API de muestra

La documentación de la [!DNL Segmentation Service] API proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

## Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar llamadas a [!DNL Platform] extremos correctamente. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

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