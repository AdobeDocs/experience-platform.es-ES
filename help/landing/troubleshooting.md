---
keywords: Experience Platform;inicio;temas populares;códigos de error de API;código de error de API;código de error API;códigos de error API;códigos de error API;error de solicitud de API;solución de problemas de API;error de API
solution: Experience Platform
title: Guía de preguntas frecuentes y resolución de problemas de Adobe Experience Platform
description: Encuentre respuestas a las preguntas más frecuentes y una guía para solucionar errores comunes en Experience Platform.
landing-page-description: Encuentre respuestas a las preguntas más frecuentes y una guía para solucionar errores comunes en Experience Platform.
short-description: Encuentre respuestas a las preguntas más frecuentes y una guía para solucionar errores comunes en Experience Platform.
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 4%

---

# [!DNL Platform] preguntas frecuentes y guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes acerca de Adobe Experience Platform, así como una guía de solución de problemas de alto nivel para los errores comunes que se pueden encontrar en cualquier API de [!DNL Experience Platform]. Para obtener guías de solución de problemas sobre los servicios individuales de [!DNL Platform], consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) que aparece a continuación.

## Preguntas frecuentes {#faq}

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca de Adobe Experience Platform.

## ¿Qué son las API de [!DNL Experience Platform]? {#what-are-experience-platform-apis}

[!DNL Experience Platform] ofrece varias API RESTful que utilizan solicitudes HTTP para acceder a recursos de [!DNL Platform]. Cada una de estas API de servicio expone varios extremos y le permite realizar operaciones para enumerar (GET), buscar (GET), editar (PUT o PATCH) y eliminar (DELETE) recursos. Para obtener más información sobre los extremos específicos y las operaciones disponibles para cada servicio, consulte la [documentación de referencia de la API](https://www.adobe.com/go/platform-api-reference-en) en Adobe I/O.

## ¿Cómo se da formato a una solicitud de API? {#how-do-i-format-an-api-request}

Los formatos de solicitud varían según la API [!DNL Platform] que se utilice. La mejor manera de aprender a estructurar las llamadas de API es siguiendo los ejemplos proporcionados en la documentación del servicio [!DNL Platform] en particular que está utilizando.

Para obtener más información sobre cómo dar formato a las solicitudes de API, visite la sección Guía de introducción a la API de Platform [leyendo llamadas de API de ejemplo](./api-guide.md#sample-api).

## ¿Cuál es mi organización? {#what-is-my-ims-organization}

Una organización es una representación de Adobe de un cliente. Cualquier solución de Adobe con licencia está integrada con esta organización del cliente. Cuando una organización tiene derecho a [!DNL Experience Platform], puede asignar acceso a los desarrolladores. El identificador de organización (`x-gw-ims-org-id`) representa la organización para la que se debe ejecutar una llamada de API y, por lo tanto, es necesario como encabezado en todas las solicitudes de API. Este identificador se puede encontrar a través de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): en la ficha **Integraciones**, vaya a la sección **Información general** para que cualquier integración en particular encuentre el identificador en **Credenciales del cliente**. Para obtener un tutorial paso a paso sobre cómo autenticarse en [!DNL Platform], consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Dónde puedo encontrar mi clave de API? {#where-can-i-find-my-api-key}

Se requiere una clave de API como encabezado en todas las solicitudes de API. Se puede encontrar a través de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). En la consola, en la ficha **Integraciones**, vaya a la sección **Información general** para una integración específica y encontrará la clave en **Credenciales del cliente**. Para obtener un tutorial paso a paso sobre cómo autenticarse en [!DNL Platform], consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Cómo obtengo un token de acceso? {#how-do-i-get-an-access-token}

Se requieren tokens de acceso en el encabezado Autorización de todas las llamadas a la API. Se pueden generar mediante un comando CURL, siempre que tenga acceso a una integración para una organización. Los tokens de acceso solo son válidos durante 24 horas, después de lo cual se debe generar un nuevo token para seguir utilizando la API. Para obtener más información sobre cómo generar tokens de acceso, consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Cómo se utilizan los parámetros de consulta? {#how-do-i-user-query-parameters}

Algunos extremos de API [!DNL Platform] aceptan parámetros de consulta para localizar información específica y filtrar los resultados devueltos en la respuesta. Los parámetros de consulta se anexan a las rutas de solicitud con un signo de interrogación (`?`), seguido de uno o más parámetros de consulta con el formato `paramName=paramValue`. Al combinar varios parámetros en una sola llamada, debe utilizar un signo &amp; (`&`) para separar los parámetros individuales. En el siguiente ejemplo se muestra cómo se representa en la documentación una solicitud que utiliza varios parámetros de consulta.

Algunos ejemplos de parámetros de consulta utilizados con frecuencia son:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obtener información detallada sobre los parámetros de consulta disponibles para un servicio o extremo específico, consulte la documentación específica del servicio.

## ¿Cómo se indica un campo JSON para actualizar en una solicitud de PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muchas operaciones del PATCH en las API [!DNL Platform] utilizan cadenas del [puntero JSON](https://tools.ietf.org/html/rfc6901) para indicar que se actualizarán las propiedades JSON. Normalmente se incluyen en las cargas útiles de solicitud utilizando el formato [JSON Patch](https://tools.ietf.org/html/rfc6902). Consulte la [guía de aspectos básicos de la API](api-fundamentals.md) para obtener información detallada sobre la sintaxis necesaria para estas tecnologías.

## ¿Puedo usar Postman para hacer llamadas a las API de [!DNL Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) es una herramienta útil para visualizar llamadas a API RESTful. La guía de introducción a la API de [Platform](api-guide.md) contiene un vídeo con instrucciones para importar colecciones de Postman. Además, se proporciona una lista de colecciones Postman para cada servicio.

## ¿Cuáles son los requisitos del sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependiendo de si utiliza la interfaz de usuario o la API, se aplican los siguientes requisitos del sistema:

**Para operaciones basadas en la IU:**
- Un navegador web estándar y moderno. Aunque se recomienda la versión más reciente de [!DNL Chrome], también se admiten las versiones principales actuales y anteriores de [!DNL Firefox], [!DNL Internet Explorer] y Safari.
   - Cada vez que se lanza una nueva versión principal, [!DNL Platform] comienza a admitir la versión más reciente, mientras que se abandona la compatibilidad con la tercera versión más reciente.
- Todos los exploradores deben tener habilitadas las cookies y JavaScript.

**Para interacciones de API y desarrollador:**
- Un entorno de desarrollo para desarrollar integraciones de REST, streaming y webhook.

## Errores y solución de problemas {#errors-and-troubleshooting}

A continuación se muestra una lista de errores que pueden producirse al utilizar cualquier servicio de [!DNL Experience Platform]. Para obtener guías de solución de problemas sobre los servicios individuales de [!DNL Platform], consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) que aparece a continuación.

## Códigos de estado de API {#api-status-codes}

Se pueden encontrar los siguientes códigos de estado en cualquier API [!DNL Experience Platform]. Cada uno tiene una variedad de causas, por lo tanto las explicaciones dadas en esta sección son de naturaleza general. Para obtener más información sobre errores específicos en servicios individuales de [!DNL Platform], consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) que se encuentra a continuación.

| Código de estado | Descripción | Posibles causas |
|--- | --- | ---|
| 400 | Solicitud incorrecta | La solicitud se construyó incorrectamente, faltaba información clave o contenía una sintaxis incorrecta. |
| 401 | Error de autenticación | La solicitud no pasó una comprobación de autenticación. Puede que falte el token de acceso o que no sea válido. Consulte la sección [Errores de token de OAuth](#oauth-token-is-missing) a continuación para obtener más información. |
| 403 | Prohibido | Se ha encontrado el recurso, pero no tiene las credenciales adecuadas para verlo. <br> Una causa probable de este error es que es posible que no tenga los [permisos de control de acceso](/help/access-control/home.md) necesarios para acceder o editar el recurso. Lea cómo [obtener los permisos de control de acceso basados en atributos necesarios](/help/landing/api-authentication.md#get-abac-permissions) para usar las API de Platform. </p> |
| 404 | No encontrado | No se encontró el recurso solicitado en el servidor. Es posible que el recurso se haya eliminado o que la ruta solicitada se haya introducido incorrectamente. |
| 500 | Error interno del servidor | Se trata de un error del lado del servidor. Si realiza muchas llamadas simultáneas, es posible que esté alcanzando el límite de la API y necesite filtrar los resultados. (Consulte la subguía [!DNL Catalog Service] API developer guide (Guía para desarrolladores de API) sobre [filtrado de datos](../catalog/api/filter-data.md) para obtener más información). Espere un momento antes de volver a intentar la solicitud y, si el problema persiste, póngase en contacto con el administrador. |

## Errores de encabezado de solicitud {#request-header-errors}

Todas las llamadas API de [!DNL Platform] requieren encabezados de solicitud específicos. Para ver qué encabezados son necesarios para servicios individuales, consulte la [documentación de referencia de la API](https://www.adobe.com/go/platform-api-reference-en). Para encontrar los valores de los encabezados de autenticación requeridos, consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Si falta alguno de estos encabezados o no es válido al realizar una llamada de API, pueden producirse los siguientes errores.

### Falta el token de OAuth {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Este mensaje de error se muestra cuando falta un encabezado `Authorization` en una solicitud de API. Asegúrese de que el encabezado Autorización se incluya con un token de acceso válido antes de intentarlo de nuevo.

### El token de OAuth no es válido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Este mensaje de error se muestra cuando el token de acceso proporcionado en el encabezado `Authorization` no es válido. Asegúrese de que el token se haya escrito correctamente o [genere un nuevo token](https://www.adobe.com/go/platform-api-authentication-en) en la consola de Adobe I/O.

### La clave API es obligatoria {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Este mensaje de error se muestra cuando falta un encabezado de clave de API (`x-api-key`) en una solicitud de API. Asegúrese de que el encabezado esté incluido con una clave de API válida antes de intentarlo de nuevo.

### Clave de API no válida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Este mensaje de error se muestra cuando el valor del encabezado de clave de API proporcionado (`x-api-key`) no es válido. Asegúrese de haber introducido la clave correctamente antes de intentarlo de nuevo. Si no conoce su clave de API, puede encontrarla en la [Consola de Adobe I/O](https://console.adobe.io): en la pestaña **Integraciones**, vaya a la sección **Información general** para obtener una integración específica y encontrar la clave de API en **Credenciales del cliente**.

### Falta el encabezado {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Este mensaje de error se muestra cuando falta un encabezado de organización (`x-gw-ims-org-id`) en una solicitud de API. Asegúrese de que el encabezado esté incluido con el ID de su organización antes de intentarlo de nuevo.

### El perfil no es válido. {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Este mensaje de error se muestra cuando el usuario o la integración de Adobe I/O (identificada por el [token de acceso](#how-do-i-get-an-access-token) en el encabezado `Authorization`) no tiene derecho a realizar llamadas a las API [!DNL Experience Platform] para la organización proporcionada en el encabezado `x-gw-ims-org-id`. Asegúrese de haber proporcionado el ID correcto para su organización en el encabezado antes de intentarlo de nuevo. Si no conoce su identificador de organización, puede encontrarlo en [Consola de Adobe I/O](https://console.adobe.io): en la ficha **Integraciones**, vaya a la sección **Información general** para obtener una integración específica y encontrar el identificador en **Credenciales de cliente**.

### Error de actualización de etiqueta {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Puede recibir un error de etiqueta si otro llamador de API realizó un cambio en cualquier entidad de origen o destino, como flujo, conexión, conector de origen o conexión de destino. Debido a la falta de coincidencia de versiones, el cambio que intenta realizar no se aplicaría a la última versión de la entidad.

Para resolver esto, debe recuperar la entidad de nuevo, asegurarse de que los cambios sean compatibles con la nueva versión de la entidad, luego colocar la nueva etiqueta en el encabezado `If-Match` y finalmente realizar la llamada de API.

### Tipo de contenido válido no especificado {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Este mensaje de error se muestra cuando una solicitud de POST, PUT o PATCH tiene un encabezado `Content-Type` no válido o falta. Asegúrese de que el encabezado esté incluido en la solicitud y que su valor sea `application/json`.

### Falta la región del usuario {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Este mensaje de error se muestra en cualquiera de los dos casos siguientes:
- Cuando se pasa un encabezado de identificador de organización incorrecto o mal formado (`x-gw-ims-org-id`) en una solicitud de API. Asegúrese de que se incluye el ID correcto de su organización antes de intentarlo de nuevo.
- Cuando su cuenta (representada por las credenciales de autenticación proporcionadas) no esté asociada a un perfil de producto para Experience Platform. Siga los pasos de [generación de credenciales de acceso](./api-authentication.md#authentication-for-each-session) en el tutorial de autenticación de la API de Platform para agregar Platform a su cuenta y actualizar las credenciales de autenticación según corresponda.

## Directorio de resolución de problemas del servicio {#service-troubleshooting-directory}

A continuación se muestra una lista de guías de solución de problemas y documentación de referencia de API para las API [!DNL Experience Platform]. Cada guía de solución de problemas proporciona respuestas a las preguntas más frecuentes y soluciones a problemas específicos de los servicios individuales de [!DNL Platform]. Los documentos de referencia de la API proporcionan una guía completa de todos los extremos disponibles para cada servicio y muestran cuerpos de solicitudes, respuestas y códigos de error de muestra que puede recibir.

| Servicio | Referencia de API | Resolución de problemas |
| --- | --- | --- |
| Control de acceso | [API de control de acceso](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guía de solución de problemas de control de acceso](../access-control/troubleshooting-guide.md) |
| Ingesta de datos de Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guía de solución de problemas de ingesta por lotes](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingesta de datos de Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guía de solución de problemas de ingesta por transmisión](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | [[!DNL Data Science Workspace] guía de solución de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Gobernanza de datos de Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Servicio de identidad de Adobe Experience Platform | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guía de solución de problemas](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guía de solución de problemas](../query-service/troubleshooting-guide.md) |
| Segmentación de Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Guía de preguntas frecuentes y solución de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] y [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guía de solución de problemas](../profile/troubleshooting.md) |
| Zonas protegidas | [API de espacio aislado](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guía de solución de problemas de zonas protegidas](../sandboxes/troubleshooting-guide.md) |
