---
solution: Experience Platform
title: Introducción a la API de etiquetas unificadas
description: La siguiente documentación proporciona información adicional que necesita conocer para trabajar correctamente con la API de etiquetas unificadas.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 9%

---

# Introducción a la API de etiquetas unificadas {#getting-started}

La API de etiquetas unificadas le permite categorizar y administrar sus objetos empresariales en Adobe Experience Platform.

Las secciones siguientes proporcionan información adicional que deberá conocer para trabajar correctamente con la API de etiquetas unificadas.

## Lectura de llamadas de API de muestra

La documentación de la API de Etiquetas unificadas proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de Experience Platform.

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para poder realizar llamadas a los extremos de Experience Platform correctamente. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifica el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con zonas protegidas en [!DNL Experience Platform], consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

## Pasos siguientes

Para realizar llamadas mediante la API de etiquetas unificadas, seleccione una de las guías de extremos disponibles mediante la navegación izquierda o en la [descripción general de la guía para desarrolladores](./overview.md)
