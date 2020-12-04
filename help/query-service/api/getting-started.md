---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guía para desarrolladores de consulta Service
topic: query templates
description: Esta guía para desarrolladores proporciona pasos para realizar varias operaciones en la API de servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# [!DNL Query Service] guía para desarrolladores

Esta guía para desarrolladores proporciona pasos para realizar varias operaciones en la API de Adobe Experience Platform [!DNL Query Service] .

## Primeros pasos

Esta guía requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que se utilizan [!DNL Query Service].

- [[!DNL Query Service]](../home.md):: Proporciona la capacidad de consulta de conjuntos de datos y capturar las consultas resultantes como nuevos conjuntos de datos en [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md):: [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para poder utilizar [!DNL Query Service] con éxito la API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en esta documentación para ver ejemplos de llamadas a API, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) a API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Experience Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Platform] de API, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con entornos limitados en [!DNL Experience Platform], consulte la documentación [general de los](../../sandboxes/home.md)entornos limitados.

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la [!DNL Query Service] API. Los siguientes documentos atraviesan las distintas llamadas de API que puede realizar mediante la [!DNL Query Service] API. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

- [Consultas](queries.md)
- [Parámetros de conexión](connection-parameters.md)
- [Consultas programadas](scheduled-queries.md)
- [Ejecuta para consultas programadas](runs-scheduled-queries.md)
- [Plantillas de consulta](query-templates.md)

## Pasos siguientes

Ahora que ha aprendido a realizar llamadas mediante la [!DNL Query Service] API, puede crear sus propias consultas no interactivas. Para obtener más información sobre cómo crear consultas, lea la guía de referencia [SQL](../sql/overview.md).