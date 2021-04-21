---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;api;
solution: Experience Platform
title: Introducción a la API del servicio de segmentación
topic-legacy: developer guide
description: La siguiente documentación proporciona información adicional que debe conocer para trabajar correctamente con la API de segmentación.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introducción a la API del servicio de segmentación {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite generar segmentos y audiencias en Adobe Experience Platform a partir de sus datos [!DNL Real-time Customer Profile].

La guía para desarrolladores requiere comprender bien los distintos [!DNL Experience Platform] servicios que se usan en el uso de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para trabajar correctamente con la API [!DNL Segmentation].

## Leer llamadas de API de ejemplo

La documentación de la API [!DNL Segmentation Service] proporciona ejemplos de llamadas de API para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] llamadas a la API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general de entornos limitados](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas con la API [!DNL Segmentation Service] , seleccione una de las guías de punto final disponibles, ya sea con la navegación izquierda o en la [información general de la guía para desarrolladores](./overview.md)
