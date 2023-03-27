---
keywords: Experience Platform;inicio;temas populares;área de nombres de identidad;área de nombres de identidad
solution: Experience Platform
title: Guía de solución de problemas del servicio de identidad
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el servicio de identidad de Adobe Experience Platform, así como una guía de solución de problemas para errores comunes.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 0%

---

# Guía de solución de problemas del servicio de identidad

Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform [!DNL Identity Service], así como una guía de solución de problemas para errores comunes. Para preguntas y solución de problemas con [!DNL Platform] API en general, consulte la [Guía de solución de problemas de la API de Adobe Experience Platform](../landing/troubleshooting.md).

Los datos que identifican a un único cliente a menudo se fragmentan en los distintos dispositivos y sistemas que utilizan para interactuar con su marca. [!DNL Identity Service] recopila estas identidades fragmentadas, lo que facilita una comprensión completa del comportamiento del cliente para que pueda ofrecer experiencias digitales impactantes en tiempo real. Para obtener más información, consulte la [Información general del servicio de identidad](./home.md).

## Preguntas frecuentes

A continuación encontrará una lista de las respuestas a las preguntas más frecuentes sobre [!DNL Identity Service].

## ¿Qué son los datos de identidad?

Los datos de identidad son datos que se pueden utilizar para identificar a una persona. Según el contexto en el que se utilicen los datos en su organización, los datos de identidad pueden incluir nombres de usuario, direcciones de correo electrónico e ID de sistemas CRM. Los datos de identidad no se limitan a los usuarios registrados de su sitio web o servicio, ya que los usuarios anónimos también se pueden identificar mediante su ID de dispositivo o cookie.

## ¿Cuál es la ventaja de etiquetar campos de datos como identidades?

Etiquetar ciertos campos de datos como identidades en los datos de registro y series temporales permite asignar relaciones de identidad dentro de la estructura natural de los datos y reconciliar datos duplicados entre canales. Consulte la [Información general del servicio de identidad](./home.md) para obtener más información.

## ¿Qué son las identidades conocidas y anónimas?

Una identidad conocida se refiere a un valor de identidad que puede utilizarse por sí solo o con otra información para identificar a una persona, ponerse en contacto con ella o localizarla. Algunos ejemplos de identidades conocidas pueden ser direcciones de correo electrónico, números de teléfono e ID de CRM.

Una identidad anónima se refiere a un valor de identidad que no se puede usar, por sí solo o con otra información, para identificar o localizar a una persona individual (como un ID de cookie).

## ¿Qué es un gráfico de identidad privado?

Un gráfico de identidad privado es un mapa privado de las relaciones entre identidades vinculadas y vinculadas, visible únicamente para su organización.

Cuando se incluye más de una identidad en cualquier dato ingerido de un extremo de flujo continuo o enviado a un conjunto de datos habilitado para [!DNL Identity Service], esas identidades están vinculadas en el gráfico de identidad privada. [!DNL Identity Service] aprovecha este gráfico para comprender las identidades de un consumidor o entidad determinados, lo que permite la vinculación de identidades y la combinación de perfiles.

## ¿Cómo se crean varios campos de identidad dentro de un esquema XDM?

[Modelo de datos de experiencia (XDM)](../xdm/home.md) los esquemas admiten varios campos de identidad. Cualquier campo de datos de tipo `string` dentro de un esquema que implemente la clase XDM Individual Profile o XDM ExperienceEvent se puede etiquetar como campo de identidad. Una vez etiquetados, los datos contenidos en estos campos se añaden al mapa de identidad del perfil.

Para ver los pasos sobre cómo etiquetar un campo XDM como campo de identidad mediante la interfaz de usuario, consulte la [Sección de identidad](../xdm/tutorials/create-schema-ui.md) en el tutorial Editor de esquemas . Si utiliza la API, consulte la [Sección del descriptor de identidad](../xdm/tutorials/create-schema-api.md) en el tutorial API del Registro de esquemas .

## ¿Hay contextos en los que algunos campos no se deben etiquetar como identidades?

Los campos de identidad deben reservarse para valores que sean únicos para cada individuo. Por ejemplo, considere un conjunto de datos para un programa de fidelidad de cliente. El campo &quot;nivel de lealtad&quot; (oro, plata, bronce) no sería un campo de identidad útil, mientras que el ID de lealtad (un valor único) lo sería.

Los campos como códigos postales y direcciones IP no deben etiquetarse como identidades para individuos, ya que estos valores pueden aplicarse a más de una persona individual. Estos tipos de campos solo deben etiquetarse como identidades para estrategias de marketing a nivel de hogar.

## ¿Por qué mis campos de identidad no vinculan el modo esperado?

Al usar la variable [`/cluster/members` extremo](./api/list-cluster-identites.md) en la API del servicio de identidad, puede ver las identidades asociadas para uno o varios campos de identidad. Si la respuesta no devuelve las identidades vinculadas que espera, asegúrese de proporcionar la información de identidad adecuada en los datos XDM. Consulte la sección sobre [suministro de datos XDM al servicio de identidad](./home.md) en la descripción general del servicio de ID para obtener más información.

## ¿Qué es un área de nombres de identidad?

Un área de nombres de identidad proporciona contexto sobre cómo se relacionan los campos de identidad con la identidad de un cliente. Por ejemplo, los campos de identidad bajo el área de nombres &quot;Correo electrónico&quot; deben cumplir un formato de correo electrónico estándar (nombre<span>@emailprovider.com) mientras que los campos que utilizan el espacio de nombres &quot;Phone&quot; deben cumplir un número de teléfono estándar (como 987-555-1234 en Norteamérica).

Los espacios de nombres distinguen valores de identidad similares entre diferentes sistemas CRM. Por ejemplo, considere un perfil que contenga un ID de fidelidad numérico asociado con el programa de recompensas de su empresa. Un área de nombres de &quot;Lealtad&quot; separaría este valor de un ID numérico similar para su sistema de comercio electrónico que también aparece en el mismo perfil.

Consulte la [información general del área de nombres de identidad](./home.md) para obtener más información.

## ¿Cómo asocio una identidad con un área de nombres de identidad?

Los campos de identidad deben asociarse con un área de nombres de identidad existente cuando se crean. Cualquier área de nombres nueva debe ser [creada mediante la API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de asociarlos con campos de identidad.

Para obtener instrucciones paso a paso sobre la definición de un área de nombres al crear un descriptor de identidad mediante la API, consulte la sección de [creación de un descriptor](../xdm/tutorials/create-schema-ui.md) en la guía para desarrolladores de Schema Registry. Para marcar un campo de esquema como una identidad en la interfaz de usuario, siga los pasos de la sección [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-api.md).

## ¿Cuáles son las áreas de nombres de identidad estándar proporcionadas por el Experience Platform? {#standard-namespaces}

Las áreas de nombres de identidad estándar son áreas de nombres disponibles para todas las organizaciones. Consulte la [Información general sobre áreas de nombres de identidad](./namespaces.md) para obtener una lista completa de los espacios de nombres estándar disponibles.

## ¿Dónde puedo encontrar la lista de áreas de nombres de identidad disponibles para mi organización?

Al usar la variable [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service), puede enumerar todas las áreas de nombres de identidad disponibles para su organización realizando una solicitud de GET al `/idnamespace/identities` punto final. Consulte la sección sobre [listar espacios de nombres disponibles](./api/list-namespaces.md) en la descripción general de la API del servicio de identidad para obtener más información.

## ¿Cómo creo un espacio de nombres personalizado para mi organización?

Al usar la variable [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service), puede crear un área de nombres de identidad personalizada para su organización realizando una solicitud de POST al `/idnamespace/identities` punto final. Consulte la sección sobre [creación de un espacio de nombres personalizado](./api/create-custom-namespace.md) en la descripción general de la API del servicio de identidad para obtener más información.

## ¿Qué son las identidades compuestas y los XID?

Se hace referencia a las identidades en las llamadas API por su identidad compuesta o XID. Una identidad compuesta es una representación de una identidad que contiene un valor de ID y un área de nombres. Un XID es un identificador de un valor único que representa la misma construcción que una identidad compuesta (un ID y un área de nombres) y se asigna automáticamente a nuevas identidades cuando el servicio de identidad las persiste. Consulte la [Información general sobre la API del servicio de identidad](./home.md) para obtener más información.

## ¿Cómo gestiona Identity Service la información de identificación personal (PII)?

El servicio de identidad tiene áreas de nombres estándar para admitir la ingesta de valores de identidad con hash para números de teléfono y correos electrónicos. Sin embargo, usted es responsable del hash de los valores. Para obtener más información sobre los datos hash incorporados a Platform, consulte la [[!DNL Data Prep] guía de funciones de asignación](../data-prep/functions.md#hashing).

## ¿Hay alguna consideración al hash de las identidades basadas en PII?

Si está enviando valores PII con hash al servicio de identidad, debe utilizar el mismo método de codificación en todos los conjuntos de datos. Esto garantiza que el mismo valor de identidad en todos los conjuntos de datos genere los mismos valores hash y que sea posible hacer coincidir y vincular correctamente en el gráfico de identidad.

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

## ¿Por qué no puedo acceder a la página del gráfico de identidad o a las API?

El administrador de Platform debe proporcionarle la variable `view-identity-graph` para que pueda ver los datos del gráfico de identidad. Sin este permiso, recibirá un mensaje de permiso denegado en la página del visor del gráfico de identidad y al llamar a las API de Platform. Consulte la [información general sobre el control de acceso](../access-control/home.md) para obtener más información sobre los permisos.

## Resolución de problemas

La siguiente sección proporciona sugerencias para la resolución de problemas para códigos de error específicos y comportamientos inesperados que puede encontrar al trabajar con el [!DNL Identity Service] API.

## [!DNL Identity Service] mensajes de error

A continuación se muestra una lista de los mensajes de error que puede encontrar al usar la variable [!DNL Identity Service] API.

### Falta el parámetro de consulta requerido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Este error se muestra cuando no se incluyó un parámetro de consulta requerido en la ruta de solicitud. La variable `detail` del mensaje de error proporciona el nombre del parámetro que falta. Las variaciones de este mensaje de error incluyen:

- Falta el parámetro de consulta requerido - nsId
- Falta el parámetro de consulta requerido - id
- Falta el parámetro de consulta requerido - xid o (nsid,id)
- Falta el parámetro de consulta requerido - targetNs
- Falta el parámetro de consulta requerido - xids o compositorXids

Compruebe que está incluyendo correctamente el parámetro indicado en la ruta de solicitud antes de intentarlo de nuevo.

### La marca de tiempo debe estar en los últimos 180 días

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] depura datos anteriores a 180 días. Este mensaje de error aparece cuando intenta acceder a datos anteriores a este.

### Hay un límite de 1000 XID en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad durante más del número máximo de [XID](#what-are-composite-identities-and-xids) permitido en una sola llamada de API. Reduzca el número de XID en la solicitud a menos del límite mostrado para resolver este problema.


### Hay un límite para 1000 compositorXids en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad durante más del número máximo de [identidades compuestas](#what-are-composite-identities-and-xids) permitido en una sola llamada de API. Reduzca el número de identidades compuestas en la solicitud a menos del límite mostrado para resolver este problema.

### El tipo de gráfico especificado no es válido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Este mensaje de error se muestra cuando `graph-type` se ha dado un valor no válido al parámetro de consulta en la ruta de solicitud. Consulte la sección sobre [gráficos de identidad](./home.md) en el [!DNL Identity Service] información general para conocer los tipos de gráficos admitidos.

### El token de servicio no tiene un ámbito válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Este mensaje de error se muestra cuando la organización de IMS no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### El token de servicio de puerta de enlace no es válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

En el caso de este error, el token de acceso no es válido. Los tokens de acceso caducan cada 24 horas y deben regenerarse para continuar utilizando [!DNL Platform] API. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre la generación de nuevos tokens de acceso.

### El token del servicio de autorización no es válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

En el caso de este error, el token de acceso no es válido. Los tokens de acceso caducan cada 24 horas y deben regenerarse para continuar utilizando [!DNL Platform] API. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre la generación de nuevos tokens de acceso.

### El token de usuario no tiene un contexto de producto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Este mensaje de error se muestra cuando el token de acceso no se ha generado a partir de un [!DNL Experience Platform] integración. Consulte la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para obtener instrucciones sobre la generación de nuevos tokens de acceso para un [!DNL Experience Platform] integración.

### Error interno al obtener el XID nativo de la identidad y el código de área de nombres

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

When [!DNL Identity Service] persiste en una identidad, el ID de la identidad y el ID de área de nombres asociado se asignan a un identificador único denominado XID. Este mensaje se muestra cuando se produce un error durante el proceso de búsqueda del XID para un valor de ID y un área de nombres determinados.

### La organización IMS no está aprovisionada para [!DNL Identity Service] usage

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Este mensaje de error se muestra cuando la organización de IMS no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### Error interno del servidor

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Este error se muestra cuando se produce una excepción inesperada en la ejecución de un [!DNL Platform] llamada de servicio. Una práctica recomendada es programar las llamadas automatizadas para volver a intentar sus solicitudes varias veces a un intervalo temporal al recibir este error. Si el problema persiste, póngase en contacto con el administrador del sistema.

## Códigos de error de ingesta de lotes

[!DNL Identity Service] Ingesta datos de identidad de datos de registros y series temporales que se cargan en [!DNL Platform] uso de ingesta por lotes. Como la ingesta por lotes es un proceso asincrónico, debe ver los detalles de un lote para ver los errores. Los errores se acumulan a medida que el lote avanza hasta que se completa.

A continuación se muestra una lista de mensajes de error relacionados con [!DNL Identity Service] puede encontrar información al usar la variable [API de ingesta de lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Esquema XDM desconocido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] solo consume identidades para datos de registros o series temporales que se ajustan a la variable [!DNL Profile] o [!DNL ExperienceEvent] , respectivamente. Intentando introducir datos para [!DNL Identity Service] que no se adhiere a ninguna de estas clases dará déclencheur a este error.

### Hubo 0 identidades válidas en las primeras 100 filas del lote procesado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Este error se muestra cuando las primeras 100 filas de un lote no presentaban identidades. Sin embargo, este error no indica de manera concluyente que no se hayan encontrado identidades en registros posteriores.

### Registros omitidos ya que solo tenían 1 identidad por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] solo vincula identidades cuando los registros individuales presentan dos o más valores de identidad. Este mensaje de error se produce una vez por cada lote ingestado y muestra el número de registros en los que solo se pudo encontrar una identidad y no se produjo ningún cambio en el gráfico de identidad.

### El código de área de nombres no está registrado para esta organización IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Este error se muestra cuando un registro ingerido presenta una identidad cuyo espacio de nombres asociado no existe o no es accesible para su organización IMS.

### Omitir la ingesta de lotes como organización de IMS no está aprovisionada para Private Identity Graph

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Al ingerir datos por lotes, este mensaje de error se muestra cuando la organización de IMS no se ha aprovisionado con los permisos adecuados para [!DNL Identity Service]. Póngase en contacto con el administrador del sistema para resolver este problema.

### Error interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Este error se muestra cuando se produce una excepción inesperada durante una ingesta por lotes. Una práctica recomendada es programar las llamadas automatizadas para volver a intentar sus solicitudes varias veces a un intervalo temporal al recibir este error. Si el problema persiste, póngase en contacto con el administrador del sistema.
