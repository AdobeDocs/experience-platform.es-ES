---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de Consulta Service
topic: query templates
translation-type: tm+mt
source-git-commit: 91104399e50bce03fed7c9196e6e83fc48a54d1c

---


# Guía para desarrolladores de Consulta Service

Esta guía para desarrolladores proporciona pasos para realizar varias operaciones en la API de servicio de Consulta de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform relacionados con el uso del servicio de Consulta.

- [Servicio](../home.md)de Consulta: Proporciona la capacidad de consulta de conjuntos de datos y capturar las consultas resultantes como nuevos conjuntos de datos en la plataforma de experiencia.
- [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
- [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para utilizar correctamente el servicio de Consulta mediante la API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en esta documentación para ver ejemplos de llamadas a API, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) a API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de la plataforma de experiencia, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de plataforma, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre cómo trabajar con entornos limitados en la plataforma de experiencia, consulte la documentación [general de los](../../sandboxes/home.md)entornos limitados.

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API del servicio de Consulta. Los siguientes documentos atraviesan las distintas llamadas de API que puede realizar mediante la API de servicio de Consulta. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

- [Consultas](queries.md)
- [Parámetros de conexión](connection-parameters.md)
- [consultas programadas](scheduled-queries.md)
- [Ejecuta para consultas programadas](runs-scheduled-queries.md)
- [Plantillas de Consulta](query-templates.md)

## Pasos siguientes

Ahora que ha aprendido a realizar llamadas mediante la API de servicio de Consulta, puede crear sus propias consultas no interactivas. Para obtener más información sobre cómo crear consultas, lea la guía de referencia [SQL](../sql/overview.md).