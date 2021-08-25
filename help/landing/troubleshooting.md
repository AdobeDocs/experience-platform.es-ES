---
keywords: Experience Platform;inicio;temas populares;códigos de error de API;código de error de API;API de código de error;API de códigos de error;error de solicitud de API;solución de problemas de API;error de API
solution: Experience Platform
title: Guía de preguntas frecuentes y solución de problemas de Adobe Experience Platform
description: Encuentre respuestas a las preguntas más frecuentes y una guía para solucionar errores comunes en Experience Platform.
landing-page-description: Encuentre respuestas a las preguntas más frecuentes y una guía para solucionar errores comunes en Experience Platform.
topic-legacy: getting started
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: a0f4e49192a54075ce7c48620c9729e61ecdfdac
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 4%

---

# [!DNL Platform] Guía de preguntas frecuentes y solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform, así como una guía de solución de problemas de alto nivel para detectar errores comunes que se puedan encontrar en cualquier API [!DNL Experience Platform]. Para obtener guías de solución de problemas sobre los servicios [!DNL Platform] individuales, consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) a continuación.

## Preguntas frecuentes {#faq}

A continuación encontrará una lista de las respuestas a las preguntas más frecuentes sobre Adobe Experience Platform.

## ¿Qué son las [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] ofrece varias API de RESTful que utilizan solicitudes HTTP para acceder a los  [!DNL Platform] recursos. Cada una de estas API de servicio expone varios puntos finales y le permite realizar operaciones de lista (GET), búsqueda (GET), edición (PUT y/o PATCH) y eliminación (DELETE) de recursos. Para obtener más información sobre los extremos específicos y las operaciones disponibles para cada servicio, consulte la [documentación de referencia de la API](https://www.adobe.com/go/platform-api-reference-en) en Adobe I/O.

## ¿Cómo se da formato a una solicitud de API? {#how-do-i-format-an-api-request}

Los formatos de solicitud varían según la API [!DNL Platform] que se esté utilizando. La mejor manera de estructurar las llamadas de API es seguir los ejemplos que se proporcionan en la documentación del servicio [!DNL Platform] que está utilizando.

Para obtener más información sobre cómo dar formato a las solicitudes de API, visite la sección Guía de introducción a la API de plataforma [leer llamadas de API de ejemplo](./api-guide.md#sample-api) .

## ¿Qué es mi organización IMS? {#what-is-my-ims-organization}

Una organización IMS es una representación de Adobe de un cliente. Las soluciones de Adobe con licencia se integran con esta organización de clientes. Cuando una organización de IMS tiene derecho a [!DNL Experience Platform], puede asignar acceso a los desarrolladores. El ID de organización de IMS (`x-gw-ims-org-id`) representa la organización para la que se debe ejecutar una llamada de API y, por lo tanto, se requiere como encabezado en todas las solicitudes de API. Este ID se puede encontrar en la [Consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui): en la pestaña **Integrations**, vaya a la sección **Overview** para cualquier integración en particular para encontrar el ID en **Client Credentials**. Para obtener un tutorial paso a paso sobre cómo autenticarse en [!DNL Platform], consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Dónde puedo encontrar mi clave de API? {#where-can-i-find-my-api-key}

Se requiere una clave de API como encabezado en todas las solicitudes de API. Se puede encontrar a través de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Dentro de la consola, en la pestaña **Integrations**, vaya a la sección **Overview** para obtener una integración específica y encontrará la clave en **Client Credentials**. Para obtener un tutorial paso a paso sobre cómo autenticarse en [!DNL Platform], consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Cómo obtengo un token de acceso? {#how-do-i-get-an-access-token}

Los tokens de acceso son necesarios en el encabezado Autorización de todas las llamadas a la API. Pueden generarse mediante un comando `curl`, siempre que tenga acceso a una integración para una organización de IMS. Los tokens de acceso solo son válidos durante 24 horas, tras lo cual debe generarse un nuevo token para continuar usando la API. Para obtener más información sobre la generación de tokens de acceso, consulte el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

## ¿Cómo utilizo los parámetros de consulta? {#how-do-i-user-query-parameters}

Algunos [!DNL Platform] extremos de API aceptan parámetros de consulta para localizar información específica y filtrar los resultados devueltos en la respuesta. Los parámetros de consulta se agregan a las rutas de solicitud con un símbolo de interrogación (`?`) seguido de uno o más parámetros de consulta utilizando el formato `paramName=paramValue`. Al combinar varios parámetros en una sola llamada, debe utilizar un símbolo &amp; (`&`) para separar los parámetros individuales. El siguiente ejemplo muestra cómo se representa una solicitud que utiliza varios parámetros de consulta en la documentación.

Algunos ejemplos de parámetros de consulta usados comúnmente son:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obtener información detallada sobre qué parámetros de consulta están disponibles para un servicio o extremo específico, consulte la documentación específica del servicio.

## ¿Cómo puedo indicar un campo JSON para actualizar en una solicitud del PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muchas operaciones de PATCH en las API [!DNL Platform] utilizan cadenas [Puntero JSON](https://tools.ietf.org/html/rfc6901) para indicar las propiedades JSON que se deben actualizar. Estos suelen incluirse en las cargas de solicitud que utilizan el formato [JSON Patch](https://tools.ietf.org/html/rfc6902). Consulte la [guía de fundamentos de API](api-fundamentals.md) para obtener información detallada sobre la sintaxis necesaria para estas tecnologías.

## ¿Puedo usar Postman para realizar llamadas a las API [!DNL Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[](https://www.postman.com/) Postmanes una herramienta útil para visualizar llamadas a las API de RESTful. La [guía de introducción a la API de plataforma](api-guide.md) contiene un vídeo e instrucciones para importar colecciones Postman. Además, se proporciona una lista de colecciones Postman para cada servicio.

## ¿Cuáles son los requisitos del sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependiendo de si utiliza la interfaz de usuario o la API, se aplican los siguientes requisitos del sistema:

**Para operaciones basadas en la interfaz de usuario:**
- Un navegador web estándar y moderno. Aunque se recomienda la versión más reciente de [!DNL Chrome] , también se admiten las versiones principales actual y anterior de [!DNL Firefox], [!DNL Internet Explorer] y Safari.
   - Cada vez que se lanza una nueva versión principal, [!DNL Platform] comienza a admitir la versión más reciente, mientras que se abandona la compatibilidad con la tercera versión más reciente.
- Todos los exploradores deben tener habilitadas las cookies y JavaScript.

**Para interacciones de API y desarrollador:**
- Un entorno de desarrollo para desarrollar integraciones de REST, transmisión por secuencias y Weblock.

## Errores y solución de problemas {#errors-and-troubleshooting}

La siguiente es una lista de errores que puede encontrar al utilizar cualquier servicio [!DNL Experience Platform]. Para obtener guías de solución de problemas sobre los servicios [!DNL Platform] individuales, consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) a continuación.

## Códigos de estado de API {#api-status-codes}

Los siguientes códigos de estado se pueden encontrar en cualquier API [!DNL Experience Platform]. Cada uno tiene una variedad de causas, por lo que las explicaciones dadas en esta sección son de naturaleza general. Para obtener más información sobre errores específicos en servicios [!DNL Platform] individuales, consulte el [directorio de solución de problemas del servicio](#service-troubleshooting-directory) a continuación.

| Código de estado | Descripción | Posibles causas |
|--- | --- | ---|
| 400 | Solicitud incorrecta | La solicitud se ha construido incorrectamente, falta información de clave o contiene sintaxis incorrecta. |
| 401 | Error de autenticación | La solicitud no pasó una comprobación de autenticación. Puede que falte el token de acceso o que no sea válido. Consulte la sección [OAuth token errors](#oauth-token-is-missing) a continuación para obtener más información. |
| 403 | Prohibido | Se encontró el recurso, pero no tiene las credenciales adecuadas para verlo. |
| 404 | No encontrado | No se encontró el recurso solicitado en el servidor. Es posible que el recurso se haya eliminado o que la ruta solicitada se haya introducido incorrectamente. |
| 500 | Error interno del servidor | Este es un error del lado del servidor. Si realiza muchas llamadas simultáneas, es posible que esté alcanzando el límite de la API y tenga que filtrar los resultados. (Consulte la [!DNL Catalog Service] guía para desarrolladores de API en la subguía [filtrado de datos](../catalog/api/filter-data.md) para obtener más información). Espere un momento antes de volver a probar la solicitud y póngase en contacto con el administrador si el problema persiste. |

## Solicitar errores de encabezado {#request-header-errors}

Todas las llamadas de API en [!DNL Platform] requieren encabezados de solicitud específicos. Para ver qué encabezados son necesarios para servicios individuales, consulte la [documentación de referencia de API](https://www.adobe.com/go/platform-api-reference-en). Para encontrar los valores de los encabezados de autenticación necesarios, consulte el [Tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Si falta alguno de estos encabezados o no es válido al realizar una llamada a la API, pueden producirse los siguientes errores.

### Falta el token OAuth {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Este mensaje de error aparece cuando falta un encabezado `Authorization` en una solicitud de API. Asegúrese de que el encabezado Autorización esté incluido con un token de acceso válido antes de intentarlo de nuevo.

### El token de OAuth no es válido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Este mensaje de error se muestra cuando el token de acceso proporcionado en el encabezado `Authorization` no es válido. Asegúrese de que el token se ha introducido correctamente o [genera un nuevo token](https://www.adobe.com/go/platform-api-authentication-en) en la consola de Adobe I/O.

### Se requiere la clave de API

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Este mensaje de error aparece cuando falta un encabezado de clave de API (`x-api-key`) en una solicitud de API. Asegúrese de que el encabezado esté incluido con una clave de API válida antes de volver a intentarlo.

### La clave de API no es válida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Este mensaje de error se muestra cuando el valor del encabezado de clave de API proporcionado (`x-api-key`) no es válido. Asegúrese de haber introducido la clave correctamente antes de volver a intentarlo. Si no conoce su clave de API, puede encontrarla en la [Consola de Adobe I/O](https://console.adobe.io): en la pestaña **Integrations**, vaya a la sección **Overview** para obtener una integración específica para encontrar la clave de API en **Client Credentials**.


### Falta el encabezado

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Este mensaje de error aparece cuando falta un encabezado de organización de IMS (`x-gw-ims-org-id`) en una solicitud de API. Asegúrese de que el encabezado esté incluido con el ID de su organización IMS antes de intentarlo de nuevo.

### El perfil no es válido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Este mensaje de error se muestra cuando el usuario o la integración de Adobe I/O (identificados por el [token de acceso](#how-do-i-get-an-access-token) en el encabezado `Authorization`) no están autorizados a realizar llamadas a las API [!DNL Experience Platform] para la organización IMS proporcionada en el encabezado `x-gw-ims-org-id`. Asegúrese de proporcionar el ID correcto para su organización IMS en el encabezado antes de volver a intentarlo. Si no conoce su ID de organización, puede encontrarlo en la [Consola de Adobe I/O](https://console.adobe.io): en la pestaña **Integrations**, vaya a la sección **Overview** para obtener una integración específica para encontrar el ID en **Client Credentials**.

### No se ha especificado un tipo de contenido válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Este mensaje de error se muestra cuando una solicitud de POST, PUT o PATCH tiene un encabezado `Content-Type` no válido o que falta. Asegúrese de que el encabezado esté incluido en la solicitud y de que su valor sea `application/json`.

### Falta la región del usuario

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Este mensaje de error se muestra cuando su cuenta (representada por las credenciales de autenticación proporcionadas) no está asociada con un perfil de producto para Experience Platform. Siga los pasos de [generación de credenciales de acceso](./api-authentication.md#authentication-for-each-session) en el tutorial de autenticación de la API de plataforma para agregar Platform a su cuenta y actualizar sus credenciales de autenticación en consecuencia.

## Directorio de solución de problemas del servicio {#service-troubleshooting-directory}

A continuación se muestra una lista de guías de solución de problemas y documentación de referencia de API para las API [!DNL Experience Platform]. Cada guía de solución de problemas proporciona respuestas a las preguntas más frecuentes y soluciones a problemas específicos de los servicios individuales [!DNL Platform]. Los documentos de referencia de la API proporcionan una guía completa de todos los extremos disponibles para cada servicio y muestran los cuerpos de solicitud de muestra, las respuestas y los códigos de error que puede recibir.

| Service | Referencia de API | Resolución de problemas |
| --- | --- | --- |
| Control de acceso | [API de control de acceso](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guía de solución de problemas del control de acceso](../access-control/troubleshooting-guide.md) |
| Incorporación de datos de Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guía de solución de problemas de ingesta por lotes ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guía de solución de problemas de ingesta por transmisión](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guía de solución de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Administración de datos de Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Servicio de ID de Adobe Experience Platform | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guía de solución de problemas](../identity-service/troubleshooting-guide.md) |
| Servicio de consultas de Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guía de solución de problemas](../query-service/troubleshooting-guide.md) |
| Segmentación de Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Guía de preguntas frecuentes y solución de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] y [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guía de solución de problemas](../profile/troubleshooting.md) |
| Entornos aislados | [API de Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guía de solución de problemas de los Simuladores para pruebas](../sandboxes/troubleshooting-guide.md) |
