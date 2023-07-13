---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;api;
solution: Experience Platform
title: Introducción a la API del servicio de segmentación
description: La siguiente documentación proporciona información adicional que necesita conocer para trabajar correctamente con la API de segmentación.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Introducción a la API del servicio de segmentación {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite crear audiencias a través de definiciones de segmentos u otras fuentes en Adobe Experience Platform desde su [!DNL Real-Time Customer Profile] datos.

La guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Experience Platform] servicios relacionados con el uso de [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): le permite crear audiencias a partir de [!DNL Real-Time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para trabajar correctamente con [!DNL Segmentation] API.

## Leer llamadas de API de muestra

El [!DNL Segmentation Service] La documentación de la API proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados obligatorios

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Platform] puntos finales. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general sobre zonas protegidas](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas utilizando [!DNL Segmentation Service] API, seleccione una de las guías de extremos disponibles mediante la navegación izquierda o dentro de la variable [información general sobre guía para desarrolladores](./overview.md)
