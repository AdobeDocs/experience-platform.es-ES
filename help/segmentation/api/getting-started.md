---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;api;
solution: Experience Platform
title: Introducción a la API del servicio de segmentación
topic-legacy: developer guide
description: La siguiente documentación proporciona información adicional que debe conocer para trabajar correctamente con la API de segmentación.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Introducción a la API del servicio de segmentación {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite crear segmentos y generar audiencias en Adobe Experience Platform a partir de su [!DNL Real-Time Customer Profile] datos.

La guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Experience Platform] servicios implicados en el uso de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permite crear segmentos de audiencia a partir de [!DNL Real-Time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para trabajar con el [!DNL Segmentation] API.

## Leer llamadas de API de ejemplo

La variable [!DNL Segmentation Service] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados requeridos

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general de entornos limitados](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas con la función [!DNL Segmentation Service] , seleccione una de las guías de punto final disponibles, ya sea en el panel de navegación izquierdo o en el [información general sobre la guía para desarrolladores](./overview.md)
