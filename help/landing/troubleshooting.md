---
keywords: Experience Platform;home;popular topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Guía de solución de problemas y preguntas más frecuentes de Adobe Experience Platform
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform, así como una guía de solución de problemas de alto nivel para los errores comunes que se pueden encontrar en cualquier API de Experience Platform.
topic: getting started
user-guide-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
translation-type: tm+mt
source-git-commit: 9981c5e34d675f7fcb767a097af3b2d3c56ec091
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 3%

---


# [!DNL Platform] Preguntas más frecuentes y guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform, así como una guía de solución de problemas de alto nivel para los errores comunes que se pueden encontrar en cualquier [!DNL Experience Platform] API. Para obtener guías de solución de problemas sobre [!DNL Platform] servicios individuales, consulte el directorio [de solución de problemas del](#service-troubleshooting-directory) servicio más abajo.

## Preguntas más frecuentes {#faq}

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre Adobe Experience Platform.

## ¿Qué son [!DNL Experience Platform] las API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] oferta varias API de RESTful que utilizan solicitudes HTTP para acceder a [!DNL Platform] los recursos. Cada una de estas API de servicio expone varios extremos y le permite realizar operaciones de lista (GET), búsqueda (GET), edición (PUT y/o PATCH) y eliminación (DELETE) de recursos. Para obtener más información sobre los extremos específicos y las operaciones disponibles para cada servicio, consulte la documentación [de referencia de la](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API sobre la E/S de Adobe.

## ¿Cómo se formatea una solicitud de API? {#how-do-i-format-an-api-request}

Los formatos de solicitud varían en función de la [!DNL Platform] API utilizada. La mejor manera de aprender a estructurar las llamadas de API es seguir los ejemplos que se proporcionan en la documentación del [!DNL Platform] servicio concreto que se utiliza.

### Leer llamadas de API de ejemplo

La documentación de [!DNL Experience Platform] muestra las llamadas de API de ejemplo de dos maneras diferentes. En primer lugar, la llamada se presenta en su formato **** API, una representación de plantilla que muestra únicamente la operación (GET, POST, PUT, PATCH, DELETE) y el punto final que se utiliza (por ejemplo, `/global/classes`). Algunas plantillas también muestran la ubicación de las variables para ilustrar cómo se debe formular una llamada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

A continuación, las llamadas se muestran como comandos cURL en una **solicitud**, que incluye los encabezados necesarios y la &quot;ruta base&quot; completa necesaria para interactuar correctamente con la API. La ruta de acceso base se debe anteponer a todos los extremos. Por ejemplo, el punto final mencionado `/global/classes` pasa a ser `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Verá el formato de API / patrón de solicitud en toda la documentación y se espera que utilice la ruta completa que se muestra en la solicitud de ejemplo al realizar sus propias llamadas a las API de plataforma.

### Ejemplo de solicitud de API

A continuación se muestra un ejemplo de solicitud de API que muestra el formato que encontrará en la documentación.

**Formato API**

El formato de la API muestra la operación (GET) y el punto final que se está utilizando. Las variables se indican mediante llaves (en este caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Solicitud**

En esta solicitud de ejemplo, las variables del formato de API reciben valores reales en la ruta de solicitud. También se muestran todos los encabezados requeridos, ya sea valores de encabezado de ejemplo o variables en las que se debe incluir información confidencial (como tokens de seguridad e ID de acceso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta ilustra lo que esperaría recibir tras una llamada correcta a la API, según la solicitud que se envió. Ocasionalmente, la respuesta se trunca en el espacio, lo que significa que puede ver más información o información adicional a la que se muestra en la muestra.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

Para obtener más información sobre los extremos específicos en las API de plataforma, incluidos los encabezados y los cuerpos de solicitud requeridos, consulte la documentación [de referencia de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API.

## ¿Cuál es mi organización IMS? {#what-is-my-ims-organization}

Una organización de IMS es una representación Adobe de un cliente. Cualquier solución de Adobe con licencia se integra con esta organización de clientes. Cuando una organización de IMS tiene derecho a [!DNL Experience Platform], puede asignar acceso a los desarrolladores. El ID de organización de IMS (`x-gw-ims-org-id`) representa la organización para la que se debe ejecutar una llamada de API y, por lo tanto, se requiere como encabezado en todas las solicitudes de API. Este ID se puede encontrar en la consola [de desarrolladores de](https://www.adobe.com/go/devs_console_ui)Adobe: en la ficha **Integraciones** , vaya a la sección **Información general** de cualquier integración concreta para encontrar el ID en Credenciales de **cliente**. Para obtener una descripción paso a paso de cómo autenticarse en [!DNL Platform], consulte el tutorial [de](../tutorials/authentication.md)autenticación.

## ¿Dónde puedo encontrar mi clave de API? {#where-can-i-find-my-api-key}

Se requiere una clave de API como encabezado en todas las solicitudes de API. Se puede encontrar a través de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). En la consola, en la ficha **Integraciones** , vaya a la sección **Información general** de una integración específica y encontrará la clave en Credenciales de **cliente**. Para obtener una descripción paso a paso de cómo autenticarse [!DNL Platform], consulte el tutorial [de](../tutorials/authentication.md)autenticación.

## ¿Cómo consigo un token de acceso? {#how-do-i-get-an-access-token}

Se requieren tokenes de acceso en el encabezado Autorización de todas las llamadas de API. Pueden generarse mediante un `curl` comando, siempre que tenga acceso a una integración para una organización de IMS. Las tokenes de acceso solo son válidas durante 24 horas, tras las cuales se debe generar un nuevo token para continuar usando la API. Para obtener más información sobre la generación de tokenes de acceso, consulte el tutorial [de](../tutorials/authentication.md)autenticación.

## ¿Cómo se utilizan los parámetros de consulta? {#how-do-i-user-query-parameters}

Algunos extremos [!DNL Platform] de API aceptan parámetros de consulta para localizar información específica y filtrar los resultados devueltos en la respuesta. Los parámetros de consulta se anexan para solicitar rutas con un símbolo de interrogación (`?`), seguido de uno o varios parámetros de consulta con el formato `paramName=paramValue`. Al combinar varios parámetros en una sola llamada, debe utilizar un símbolo (`&`) para separar parámetros individuales. En el siguiente ejemplo se muestra cómo se representa en la documentación una solicitud que utiliza varios parámetros de consulta.

Algunos ejemplos de parámetros de consulta que se utilizan con frecuencia son:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obtener información detallada sobre los parámetros de consulta disponibles para un servicio o extremo específico, consulte la documentación específica del servicio.

## ¿Cómo se indica un campo JSON para actualizar en una solicitud de PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muchas operaciones de PATCH en [!DNL Platform] API utilizan cadenas de [puntero](https://tools.ietf.org/html/rfc6901) JSON para indicar las propiedades de JSON que se van a actualizar. Normalmente, se incluyen en las cargas de solicitud con el formato de parche [](https://tools.ietf.org/html/rfc6902) JSON. Consulte la guía [de aspectos fundamentales de la](api-fundamentals.md) API para obtener información detallada sobre la sintaxis requerida para estas tecnologías.

## ¿Puedo usar Postman para realizar llamadas a [!DNL Platform] las API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) es una herramienta útil para visualizar llamadas a las API de RESTful. Esta publicación [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Media describe cómo configurar Postman para que realice automáticamente la autenticación y la utilice para consumir [!DNL Experience Platform] API.

## ¿Cuáles son los requisitos del sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Según si utiliza la interfaz de usuario o la API, se aplican los siguientes requisitos del sistema:

**Para operaciones basadas en la interfaz de usuario:**
- Un navegador web moderno y estándar. Aunque se recomienda la versión más reciente de [!DNL Chrome] , también se admiten las versiones principales actuales y anteriores de [!DNL Firefox], [!DNL Internet Explorer]y Safari.
   - Cada vez que se lanza una nueva versión principal, se eliminan [!DNL Platform] los inicios que admiten la versión más reciente y la compatibilidad con la tercera versión más reciente.
- Todos los exploradores deben tener habilitadas las cookies y JavaScript.

**Para interacciones entre API y desarrollador:**
- Un entorno de desarrollo para desarrollar integraciones de REST, flujo continuo y Weblink.

## Errores y solución de problemas {#errors-and-troubleshooting}

A continuación se muestra una lista de errores que puede encontrar al utilizar cualquier [!DNL Experience Platform] servicio. Para obtener guías de solución de problemas sobre [!DNL Platform] servicios individuales, consulte el directorio [de solución de problemas del](#service-troubleshooting-directory) servicio más abajo.

## Códigos de estado de API {#api-status-codes}

Los siguientes códigos de estado pueden encontrarse en cualquier [!DNL Experience Platform] API. Cada uno de ellos tiene una variedad de causas, por lo que las explicaciones dadas en esta sección son de carácter general. Para obtener más información sobre errores específicos en [!DNL Platform] servicios individuales, consulte el directorio [de solución de problemas del](#service-troubleshooting-directory) servicio más abajo.

| Código de estado | Descripción | Causas posibles |
--- | --- | ---
| 400 | Solicitud incorrecta | La solicitud se construyó incorrectamente, falta información de clave o contenía sintaxis incorrecta. |
| 401 | Error de autenticación | La solicitud no pasó una comprobación de autenticación. Es posible que falte el token de acceso o que no sea válido. Consulte la sección de errores [del token de](#oauth-token-is-missing) OAuth más abajo para obtener más detalles. |
| 403 | Prohibido | Se encontró el recurso, pero no tiene las credenciales correctas para vista. |
| 404 | No encontrado | No se encontró el recurso solicitado en el servidor. Es posible que el recurso se haya eliminado o que la ruta solicitada se haya introducido incorrectamente. |
| 500 | Error interno del servidor | Se trata de un error del lado del servidor. Si realiza muchas llamadas simultáneas, puede que esté llegando al límite de la API y necesite filtrar los resultados. (Para obtener más información, consulte la [!DNL Catalog Service] guía para desarrolladores de API sobre el [filtrado de datos](../catalog/api/filter-data.md) ). Espere un momento antes de volver a intentar la solicitud y póngase en contacto con el administrador si el problema persiste. |

## Errores de encabezado de solicitud {#request-header-errors}

Todas las llamadas de API de [!DNL Platform] requieren encabezados de solicitud específicos. Para ver qué encabezados son necesarios para servicios individuales, consulte la documentación [de referencia de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API. Para buscar los valores de los encabezados de autenticación necesarios, consulte el tutorial [](../tutorials/authentication.md)Autenticación. Si alguno de estos encabezados falta o no es válido al realizar una llamada de API, pueden producirse los siguientes errores.

### Falta el token de OAuth {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Este mensaje de error se muestra cuando falta un `Authorization` encabezado de una solicitud de API. Asegúrese de que el encabezado Autorización se incluye con un token de acceso válido antes de intentarlo de nuevo.

### El token de OAuth no es válido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Este mensaje de error se muestra cuando el token de acceso proporcionado en el `Authorization` encabezado no es válido. Asegúrese de que el token se ha introducido correctamente o [genere un nuevo token](../tutorials/authentication.md) en la consola de E/S de Adobe.

### Se requiere la clave de API

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Este mensaje de error se muestra cuando falta un encabezado de clave de API (`x-api-key`) en una solicitud de API. Asegúrese de que el encabezado se incluye con una clave de API válida antes de intentarlo de nuevo.

### La clave de API no es válida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Este mensaje de error se muestra cuando el valor del encabezado de clave de API proporcionado (`x-api-key`) no es válido. Asegúrese de haber introducido la clave correctamente antes de intentarlo de nuevo. Si no conoce la clave de API, puede encontrarla en la consola [de E/S de](https://console.adobe.io)Adobe: en la ficha **Integraciones** , vaya a la sección **Información general** de una integración específica para encontrar la clave de API en Credenciales **de cliente**.


### Falta el encabezado

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Este mensaje de error se muestra cuando falta un encabezado de organización de IMS (`x-gw-ims-org-id`) en una solicitud de API. Asegúrese de que el encabezado se incluye con el ID de su organización de IMS antes de intentarlo de nuevo.

### Perfil no válido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Este mensaje de error se muestra cuando el usuario o la integración de E/S de Adobe (identificada por el [token de acceso](#how-do-i-get-an-access-token) en el `Authorization` encabezado) no tiene derecho a realizar llamadas a [!DNL Experience Platform] API para la organización IMS proporcionada en el `x-gw-ims-org-id` encabezado. Asegúrese de que ha proporcionado el ID correcto para su organización de IMS en el encabezado antes de intentarlo de nuevo. Si no conoce el ID de organización, puede encontrarlo en la consola [de E/S de](https://console.adobe.io)Adobe: en la ficha **Integraciones** , vaya a la sección **Información general** de una integración específica para buscar el ID en Credenciales de **cliente**.

### No se especificó un tipo de contenido válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Este mensaje de error se muestra cuando una solicitud de POST, PUT o PATCH tiene un `Content-Type` encabezado no válido o que falta. Asegúrese de que el encabezado esté incluido en la solicitud y de que su valor sea `application/json`.


## Directorio de solución de problemas del servicio {#service-troubleshooting-directory}

La siguiente es una lista de guías de solución de problemas y documentación de referencia de API para [!DNL Experience Platform] las API. Cada guía de solución de problemas proporciona respuestas a las preguntas más frecuentes y soluciones a problemas específicos de [!DNL Platform] servicios individuales. Los documentos de referencia de API proporcionan una guía completa de todos los extremos disponibles para cada servicio y muestran los cuerpos de solicitud de muestra, las respuestas y los códigos de error que puede recibir.

| Service | Referencia de API | Resolución de problemas |
| --- | --- | --- |
| Control de acceso | [API de control de acceso](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guía de solución de problemas de control de acceso](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform Data Ingestion | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guía de resolución de problemas de ingestión por lotes](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guía de solución de problemas de ingestión por flujo continuo](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei API de aprendizaje automático]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guía de solución de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Administración de datos de Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Servicio de ID de Adobe Experience Platform | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guía de solución de problemas](../identity-service/troubleshooting-guide.md) |
| Servicio de Consulta de Adobe Experience Platform | [[!DNL API de servicio de Consulta]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guía de solución de problemas](../query-service/troubleshooting-guide.md) |
| Segmentación de Adobe Experience Platform | [[!API de segmentación DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL API de registro de Esquema]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Preguntas más frecuentes y guía de solución de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] y [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Perfil API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guía de solución de problemas](../profile/troubleshooting.md) |
| Sandboxes | [API de Simulador para pruebas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guía de solución de problemas de Simuladores para pruebas](../sandboxes/troubleshooting-guide.md) |

