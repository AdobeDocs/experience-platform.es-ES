---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;api;
solution: Experience Platform
title: Introducción a la API del servicio de segmentación
description: La siguiente documentación proporciona información adicional que necesita conocer para trabajar correctamente con la API de segmentación.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# Introducción a la API del servicio de segmentación {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] le permite crear audiencias a través de definiciones de segmentos u otras fuentes en Adobe Experience Platform a partir de sus datos de [!DNL Real-Time Customer Profile].

La guía para desarrolladores requiere una comprensión práctica de los distintos servicios de [!DNL Experience Platform] implicados en el uso de [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite crear audiencias a partir de los datos de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente. Para utilizar la segmentación de la mejor manera posible, asegúrate de que tus datos se incorporen como perfiles y eventos según las [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para poder trabajar correctamente con la API [!DNL Segmentation].

## Lectura de llamadas de API de muestra

La documentación de la API [!DNL Segmentation Service] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifica el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con zonas protegidas en [!DNL Experience Platform], consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas mediante la API [!DNL Segmentation Service], seleccione una de las guías de extremos disponibles mediante la navegación izquierda o en la [descripción general de la guía para desarrolladores](./overview.md)
