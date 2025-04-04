---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consulta
solution: Experience Platform
title: Guía de API del servicio de consultas
description: La API del servicio de consultas permite a los desarrolladores consultar sus datos de Adobe Experience Platform mediante SQL estándar. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# Guía de la API de [!DNL Query Service]

Esta guía para desarrolladores proporciona pasos para realizar diversas operaciones en la API de Adobe Experience Platform [!DNL Query Service].

## Introducción

Esta guía requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform involucrados con el uso de [!DNL Query Service].

- [[!DNL Query Service]](../home.md): proporciona la capacidad de consultar conjuntos de datos y capturar las consultas resultantes como nuevos conjuntos de datos en [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para usar correctamente [!DNL Query Service] mediante la API.

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en esta documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifica el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con zonas protegidas en [!DNL Experience Platform], consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

## Llamadas de API de muestra

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API [!DNL Query Service]. Los siguientes documentos explican las distintas llamadas de API que puede realizar mediante la API [!DNL Query Service]. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

- [Consultas](queries.md)
- [Parámetros de conexión](connection-parameters.md)
- [Consultas programadas](scheduled-queries.md)
- [Ejecuta para consultas programadas](runs-scheduled-queries.md)
- [Plantillas de consulta](query-templates.md)
- [Consultas aceleradas](./accelerated-queries.md)
- [Suscripciones de alerta](./alert-subscriptions.md)

## Pasos siguientes

Ahora que ha aprendido a hacer llamadas usando la API [!DNL Query Service], puede crear sus propias consultas no interactivas. Para obtener más información sobre cómo crear consultas, lea la [guía de referencia de SQL](../sql/overview.md).
