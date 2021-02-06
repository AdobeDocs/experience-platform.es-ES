---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;consulta
solution: Experience Platform
title: Guía de API de servicio de consulta
topic: query templates
description: La API de servicio de Consulta permite a los desarrolladores realizar consultas de sus datos de Adobe Experience Platform mediante SQL estándar. Siga esta guía para aprender a realizar operaciones clave mediante la API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# [!DNL Query Service] Guía de API

Esta guía para desarrolladores proporciona pasos para realizar diversas operaciones en la API de Adobe Experience Platform [!DNL Query Service].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los diversos servicios de Adobe Experience Platform que se utilizan con [!DNL Query Service].

- [[!DNL Query Service]](../home.md):: Proporciona la capacidad de consulta de conjuntos de datos y capturar las consultas resultantes como nuevos conjuntos de datos en  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md)::  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para utilizar con éxito [!DNL Query Service] mediante la API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en esta documentación para ver ejemplos de llamadas de API, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Experience Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Platform] API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la [documentación general de entornos limitados](../../sandboxes/home.md).

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API [!DNL Query Service]. Los siguientes documentos recorren las distintas llamadas de API que puede realizar mediante la API [!DNL Query Service]. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

- [Consultas](queries.md)
- [Parámetros de conexión](connection-parameters.md)
- [Consultas programadas](scheduled-queries.md)
- [Ejecuta para consultas programadas](runs-scheduled-queries.md)
- [Plantillas de consulta](query-templates.md)

## Pasos siguientes

Ahora que ha aprendido a realizar llamadas mediante la API [!DNL Query Service], puede crear sus propias consultas no interactivas. Para obtener más información sobre cómo crear consultas, lea la [guía de referencia de SQL](../sql/overview.md).