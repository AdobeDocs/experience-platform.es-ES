---
keywords: Experience Platform;inicio;temas populares;área de nombres de identidad;área de nombres de identidad
solution: Experience Platform
title: Guía de resolución de problemas del servicio de identidad
description: Este documento proporciona respuestas a las preguntas frecuentes sobre el servicio de identidad de Adobe Experience Platform, así como una guía de solución de problemas para errores comunes.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---

# Guía de solución de problemas del servicio de identidad

Este documento proporciona respuestas a las preguntas frecuentes acerca de Adobe Experience Platform [!DNL Identity Service], así como una guía de solución de problemas para errores comunes. Si tiene alguna pregunta o pregunta sobre [!DNL Platform] API en general, consulte las [Guía de solución de problemas de API de Adobe Experience Platform](../landing/troubleshooting.md).

Los datos que identifican a un único cliente suelen estar fragmentados entre los distintos dispositivos y sistemas que utilizan para interactuar con su marca. [!DNL Identity Service] recopila estas identidades fragmentadas, lo que facilita una comprensión completa del comportamiento de los clientes para que pueda ofrecer experiencias digitales impactantes en tiempo real. Para obtener más información, consulte la [Introducción al servicio de identidad](./home.md).

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca de [!DNL Identity Service].

## ¿Qué son los datos de identidad?

Los datos de identidad son cualquier dato que pueda utilizarse para identificar a una persona individual. Según el contexto de uso de los datos en su organización, los datos de identidad pueden incluir nombres de usuario, direcciones de correo electrónico e ID de sistemas CRM. Los datos de identidad no se limitan a los usuarios registrados de su sitio web o servicio, ya que los usuarios anónimos también pueden identificarse por su ID de dispositivo o cookie.

## ¿Cuál es la ventaja de etiquetar campos de datos como identidades?

El etiquetado de determinados campos de datos como identidades en los datos de registros y series temporales le permite asignar relaciones de identidad dentro de la estructura natural de los datos y reconciliar los datos duplicados entre canales. Consulte la [Introducción al servicio de identidad](./home.md) para obtener más información.

## ¿Qué son las identidades conocidas y anónimas?

Una identidad conocida hace referencia a un valor de identidad que puede utilizarse, tanto por sí solo como con otra información, para identificar, contactar o localizar a una persona individual. Algunos ejemplos de identidades conocidas son direcciones de correo electrónico, números de teléfono e ID de CRM.

Una identidad anónima hace referencia a un valor de identidad que no se puede utilizar, ni por sí solo ni con otra información, para identificar, contactar o localizar a una persona individual (como un ID de cookie).

## ¿Qué es un gráfico de identidad privada?

Un gráfico de identidad privada es un mapa privado de relaciones entre identidades vinculadas y vinculadas, visible solo para su organización.

Cuando se incluye más de una identidad en cualquier dato introducido desde un extremo de flujo continuo o enviado a un conjunto de datos habilitado para [!DNL Identity Service], esas identidades están vinculadas en el gráfico de identidad privada. [!DNL Identity Service] aprovecha este gráfico para recopilar identidades de un consumidor o entidad determinados, lo que permite la unión de identidades y la combinación de perfiles.

## ¿Cómo se crean varios campos de identidad dentro de un esquema XDM?

[Modelo de datos de experiencia (XDM)](../xdm/home.md) los esquemas admiten varios campos de identidad. Cualquier campo de datos de tipo `string` dentro de un esquema que implementa la clase XDM Individual Profile o XDM ExperienceEvent se puede etiquetar como un campo de identidad. Una vez etiquetados, los datos contenidos en estos campos se añaden al mapa de identidad del perfil.

Para ver los pasos sobre cómo etiquetar un campo XDM como campo de identidad mediante la interfaz de usuario, consulte la [Sección de identidad](../xdm/tutorials/create-schema-ui.md) en el tutorial Editor de esquemas. Si utiliza la API, consulte la [Sección del descriptor de identidad](../xdm/tutorials/create-schema-api.md) en el tutorial API de Registro de esquemas.

## ¿Hay contextos en los que algunos campos no deben etiquetarse como identidades?

Los campos de identidad deben reservarse para valores que sean únicos para cada individuo. Por ejemplo, considere un conjunto de datos para un programa de lealtad de clientes. El campo &quot;nivel de lealtad&quot; (oro, plata, bronce) no sería un campo de identidad útil, mientras que el ID de lealtad (un valor único) sí lo sería.

Los campos como códigos postales y direcciones IP no deben etiquetarse como identidades de personas, ya que estos valores pueden aplicarse a más de una persona individual. Estos tipos de campos solo deben etiquetarse como identidades para las estrategias de marketing del hogar.

## ¿Por qué mis campos de identidad no se vinculan de la forma esperada?

Uso del [`/cluster/members` punto final](./api/list-cluster-identites.md) en la API del servicio de identidad, puede ver las identidades asociadas para uno o varios campos de identidad. Si la respuesta no devuelve las identidades vinculadas esperadas, asegúrese de proporcionar la información de identidad adecuada en los datos XDM. Consulte la sección sobre [suministro de datos XDM al servicio de identidad](./home.md) en el Resumen del servicio de identidad para obtener más información.

## ¿Qué es un área de nombres de identidad?

Un área de nombres de identidad proporciona contexto para la relación entre los campos de identidad y la identidad de un cliente. Por ejemplo, los campos de identidad del área de nombres &quot;Correo electrónico&quot; deben ajustarse a un formato de correo electrónico estándar (nombre<span>@emailprovider.com), mientras que los campos que utilizan el área de nombres &quot;Phone&quot; deben ajustarse a un número de teléfono estándar (como 987-555-1234 en Norteamérica).

Las áreas de nombres distinguen valores de identidad similares entre sistemas CRM diferentes. Por ejemplo, piense en un perfil que contenga un ID de fidelidad numérico asociado al programa de recompensas de su empresa. Un área de nombres de &quot;Fidelidad&quot; separaría este valor de un ID numérico similar para su sistema de comercio electrónico que también aparece en el mismo perfil.

Consulte la [información general del área de nombres de identidad](./home.md) para obtener más información.

## ¿Cómo asocio una identidad con un área de nombres de identidad?

Los campos de identidad deben asociarse con un área de nombres de identidad existente cuando se crean. Cualquier área de nombres nueva debe ser [creado con la API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de asociarlos a campos de identidad.

Para obtener instrucciones paso a paso sobre cómo definir un área de nombres al crear un descriptor de identidad mediante la API, consulte la sección sobre [creación de un descriptor](../xdm/tutorials/create-schema-ui.md) en la guía para desarrolladores de Schema Registry. Para marcar un campo de esquema como identidad en la interfaz de usuario, siga los pasos en la [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-api.md).

## ¿Cuáles son las áreas de nombres de identidad estándar proporcionadas por Experience Platform? {#standard-namespaces}

Las áreas de nombres de identidad estándar son áreas de nombres disponibles para todas las organizaciones. Consulte la [Información general sobre áreas de nombres de identidad](./features/namespaces.md) para obtener una lista completa de las áreas de nombres estándar disponibles.

## ¿Dónde puedo encontrar la lista de áreas de nombres de identidad disponibles para mi organización?

Uso del [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service), puede enumerar todas las áreas de nombres de identidad disponibles para su organización realizando una solicitud de GET a `/idnamespace/identities` punto final. Consulte la sección sobre [listar áreas de nombres disponibles](./api/list-namespaces.md) en la Información general de la API del servicio de ID para obtener más información.

## ¿Cómo se crea un área de nombres personalizada para la organización?

Uso del [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service), puede crear un área de nombres de identidad personalizada para su organización realizando una solicitud de POST a `/idnamespace/identities` punto final. Consulte la sección sobre [crear un área de nombres personalizada](./api/create-custom-namespace.md) en la Información general de la API del servicio de ID para obtener más información.

## ¿Qué son las identidades compuestas y los XID?

En las llamadas a API se hace referencia a las identidades por su identidad compuesta o XID. Una identidad compuesta es una representación de una identidad que contiene un valor de ID y un área de nombres. Un XID es un identificador de un solo valor que representa la misma construcción que una identidad compuesta (un ID y un área de nombres) y se asigna automáticamente a nuevas identidades cuando el servicio de identidad las mantiene. Consulte la [Resumen de API del servicio de identidad](./home.md) para obtener más información.

## ¿Cómo gestiona el servicio de identidad la información de identificación personal (PII)?

El servicio de identidad tiene áreas de nombres estándar para admitir la ingesta de valores de identidad con hash para números de teléfono y correos electrónicos. Sin embargo, usted es responsable del hash de los valores. Para obtener más información sobre los datos hash introducidos en Platform, consulte la [[!DNL Data Prep] guía de funciones de asignación](../data-prep/functions.md#hashing).

## ¿Hay alguna consideración al hash de las identidades basadas en PII?

Si está enviando valores PII con hash al servicio de identidad, debe utilizar el mismo método de cifrado en todos los conjuntos de datos. Esto garantiza que el mismo valor de identidad en todos los conjuntos de datos genere los mismos valores hash y que puedan coincidir y vincularse correctamente en el gráfico de identidad.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## ¿Por qué no puedo acceder a la página o las API del gráfico de identidad?

El administrador de la plataforma debe proporcionarle el `view-identity-graph` para ver los datos del gráfico de identidad. Sin este permiso, recibirá un mensaje de permiso denegado en la página del visor de gráficos de identidades y al llamar a las API de Platform. Consulte la [información general de control de acceso](../access-control/home.md) para obtener más información sobre los permisos.

## Resolución de problemas

En la siguiente sección se proporcionan sugerencias para la resolución de problemas con códigos de error específicos y comportamiento inesperado que puede encontrar al trabajar con [!DNL Identity Service] API.

## [!DNL Identity Service] mensajes de error

A continuación se muestra una lista de mensajes de error que pueden aparecer al utilizar el [!DNL Identity Service] API.

### Falta un parámetro de consulta obligatorio

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Este error se muestra cuando un parámetro de consulta requerido no se incluyó en la ruta de solicitud. El `detail` del mensaje de error proporciona el nombre del parámetro que falta. Las variaciones de este mensaje de error incluyen:

- Falta el parámetro de consulta necesario - nsId
- Falta el parámetro de consulta necesario - id
- Falta el parámetro de consulta necesario: xid o (nsid,id)
- Falta el parámetro de consulta necesario - targetNs
- Falta el parámetro de consulta necesario: xids o compoundXids

Compruebe que está incluyendo correctamente el parámetro indicado en la ruta de solicitud antes de intentarlo de nuevo.

### La marca de tiempo debe estar entre los últimos 180 días

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] purga los datos con más de 180 días. Este mensaje de error se muestra cuando intenta acceder a datos anteriores a este.

### Hay un límite de 1000 XID en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad durante más del número máximo de [XID](#what-are-composite-identities-and-xids) en una sola llamada de API. Reduzca el número de XID de la solicitud por debajo del límite mostrado para resolver este problema.


### Hay un límite de 1000 compositesXids en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad durante más del número máximo de [identidades compuestas](#what-are-composite-identities-and-xids) en una sola llamada de API. Reduzca la cantidad de identidades compuestas en la solicitud por debajo del límite mostrado para resolver este problema.

### El tipo de gráfico especificado no es válido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Este mensaje de error se muestra cuando `graph-type` El parámetro de consulta recibe un valor no válido en la ruta de solicitud. Consulte la sección sobre [gráficos de identidad](./home.md) en el [!DNL Identity Service] información general para conocer qué tipos de gráficos son compatibles.

### El token de servicio no tiene un ámbito válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Este mensaje de error se muestra cuando su organización no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### El token del servicio de puerta de enlace no es válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

En el caso de este error, el token de acceso no es válido. Los tokens de acceso caducan cada 24 horas y deben regenerarse para seguir utilizando [!DNL Platform] API. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre cómo generar nuevos tokens de acceso.

### El token del servicio de autorización no es válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

En el caso de este error, el token de acceso no es válido. Los tokens de acceso caducan cada 24 horas y deben regenerarse para seguir utilizando [!DNL Platform] API. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre cómo generar nuevos tokens de acceso.

### El token de usuario no tiene un contexto de producto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Este mensaje de error se muestra cuando el token de acceso no se ha generado a partir de una [!DNL Experience Platform] integración. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre la generación de nuevos tokens de acceso para una [!DNL Experience Platform] integración.

### Error interno al obtener XID nativo desde el código de identidad y área de nombres

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Cuándo [!DNL Identity Service] Si persiste una identidad, el ID de la identidad y el ID del área de nombres asociado se asignan a un identificador único denominado XID. Este mensaje se muestra cuando se produce un error durante el proceso de búsqueda del XID para un valor de ID y un área de nombres determinados.

### La organización de IMS no está aprovisionada para [!DNL Identity Service] uso

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Este mensaje de error se muestra cuando su organización no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### Error interno del servidor

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Este error se muestra cuando se produce una excepción inesperada en la ejecución de una [!DNL Platform] llamada de servicio. La práctica recomendada es programar las llamadas automatizadas para que reintenten sus solicitudes unas cuantas veces a intervalos cronometrados cuando reciban este error. Si el problema persiste, póngase en contacto con el administrador del sistema.

## Códigos de error de ingesta por lotes

[!DNL Identity Service] ingiere datos de identidad a partir de datos de registros y series temporales cargados en [!DNL Platform] Uso de la ingesta por lotes. Como la ingesta por lotes es un proceso asincrónico, debe ver los detalles de un lote para ver los errores. Los errores se acumulan a medida que el lote progresa hasta que se complete.

A continuación se muestra una lista de mensajes de error relacionados con [!DNL Identity Service] puede encontrar al usar el [API de ingesta por lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Esquema XDM desconocido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] solo consume identidades para datos de registros o series temporales que se ajustan a la [!DNL Profile] o [!DNL ExperienceEvent] clases, respectivamente. Intentando ingerir datos para [!DNL Identity Service] que no se adhiera a ninguna clase almacenará en déclencheur este error.

### Había 0 identidades válidas en las primeras 100 filas del lote procesado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Este error se muestra cuando las primeras 100 filas de un lote no presentan identidades. Sin embargo, este error no indica de forma concluyente que no se encontraran identidades en registros posteriores.

### Registros omitidos, ya que solo tenían 1 identidad por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] solo vincula identidades cuando los registros únicos presentan dos o más valores de identidad. Este mensaje de error se produce una vez por cada lote ingerido y muestra el número de registros en los que solo se pudo encontrar una identidad, sin que se haya producido ningún cambio en el gráfico de identidades.

### El código de área de nombres no está registrado para esta organización de IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Este error se muestra cuando un registro ingerido presenta una identidad cuyo área de nombres asociada no existe o su organización no puede acceder a ella.

### Omitiendo la ingesta por lotes, ya que la organización de IMS no está aprovisionada para el gráfico de identidad privada

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Al ingerir datos por lotes, este mensaje de error se muestra cuando su organización no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### Error interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Este error se muestra cuando se produce una excepción inesperada durante una ingesta por lotes. La práctica recomendada es programar las llamadas automatizadas para que reintenten sus solicitudes unas cuantas veces a intervalos cronometrados cuando reciban este error. Si el problema persiste, póngase en contacto con el administrador del sistema.
