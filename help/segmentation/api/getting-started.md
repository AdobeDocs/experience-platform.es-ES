---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;api;
solution: Experience Platform
title: Introducción a la API del servicio de segmentación
topic: developer guide
description: La siguiente documentación proporciona información adicional que debe conocer para trabajar correctamente con la API de segmentación.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Introducción a la API de servicio de segmentación {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite generar segmentos y audiencias en Adobe Experience Platform a partir de sus [!DNL Real-time Customer Profile] datos.

La guía para desarrolladores requiere una comprensión práctica de los diversos [!DNL Experience Platform] servicios que implican el uso de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md):: Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para trabajar con la API [!DNL Segmentation] de manera satisfactoria.

## Leer llamadas de API de muestra

La documentación de la API [!DNL Segmentation Service] proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas a [!DNL Platform] extremos de forma satisfactoria. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general de entornos limitados](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas mediante la API [!DNL Segmentation Service], seleccione una de las guías de punto final disponibles mediante el menú de navegación izquierdo o en la [información general de guía para desarrolladores](./overview.md)