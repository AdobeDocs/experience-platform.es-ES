---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;consulta
solution: Experience Platform
title: Guía de API del servicio de consulta
description: La API del servicio de consulta permite a los desarrolladores consultar sus datos de Adobe Experience Platform mediante SQL estándar. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---

# Guía de la API de [!DNL Query Service]

Esta guía para desarrolladores proporciona los pasos para realizar varias operaciones en Adobe Experience Platform [!DNL Query Service] API.

## Primeros pasos

Esta guía requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en el uso de [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Proporciona la capacidad de consultar conjuntos de datos y capturar las consultas resultantes como nuevos conjuntos de datos en [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para utilizar correctamente [!DNL Query Service] usando la API .

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en esta documentación para ver ejemplos de llamadas de API, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Experience Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Platform] Llamadas de API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general de entornos limitados](../../sandboxes/home.md).

## Ejemplo de llamadas a API

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas al [!DNL Query Service] API. Los siguientes documentos recorren las distintas llamadas de API que puede realizar mediante el [!DNL Query Service] API. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

- [Consultas](queries.md)
- [Parámetros de conexión](connection-parameters.md)
- [Consultas programadas](scheduled-queries.md)
- [Ejecuta para consultas programadas](runs-scheduled-queries.md)
- [Plantillas de consulta](query-templates.md)
- [Consultas aceleradas](./accelerated-queries.md)
- [Suscripciones de alertas](./alert-subscriptions.md)

## Pasos siguientes

Ahora que ha aprendido a realizar llamadas utilizando la variable [!DNL Query Service] API, puede crear sus propias consultas no interactivas. Para obtener más información sobre cómo crear consultas, lea la [Guía de referencia SQL](../sql/overview.md).
