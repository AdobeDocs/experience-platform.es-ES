---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de solución de problemas de Adobe Experience Platform Identity Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2225'
ht-degree: 1%

---


# Guía de solución de problemas del servicio de identidad

Este documento proporciona respuestas a las preguntas más frecuentes sobre el Adobe Experience Platform [!DNL Identity Service], así como una guía de solución de problemas para los errores más comunes. Para preguntas y solución de problemas con [!DNL Platform] las API en general, consulte la guía [de solución de problemas de la API de](../landing/troubleshooting.md)Adobe Experience Platform.

Los datos que identifican a un único cliente suelen estar fragmentados en los distintos dispositivos y sistemas que utilizan para interactuar con su marca. [!DNL Identity Service] recopila estas identidades fragmentadas, lo que facilita una comprensión completa del comportamiento del cliente para que pueda ofrecer experiencias digitales impactantes en tiempo real. Para obtener más información, consulte la descripción general [del servicio de](./home.md)identidad.

## Preguntas frecuentes

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre [!DNL Identity Service].

## ¿Qué son los datos de identidad?

Los datos de identidad son datos que pueden utilizarse para identificar a una persona. Según el contexto en el que se utilicen los datos en su organización, los datos de identidad pueden incluir nombres de usuario, direcciones de correo electrónico e ID de sistemas CRM. Los datos de identidad no se limitan a los usuarios registrados del sitio web o servicio, ya que los usuarios anónimos también pueden identificarse mediante su ID de dispositivo o cookie.

## ¿Cuál es el beneficio de etiquetar los campos de datos como identidades?

Etiquetar determinados campos de datos como identidades en los datos de registros y series temporales permite asignar relaciones de identidad dentro de la estructura natural de los datos y reconciliar los datos de duplicado entre canales. Consulte la información general [del servicio de](./home.md) identidad para obtener más información.

## ¿Qué son las identidades conocidas y anónimas?

Una identidad conocida se refiere a un valor de identidad que puede utilizarse por sí solo o con otra información para identificar, contactar o ubicar a una persona individual. Algunos ejemplos de identidades conocidas pueden incluir direcciones de correo electrónico, números de teléfono e ID de CRM.

Una identidad anónima hace referencia a un valor de identidad que no se puede utilizar por sí solo o con otra información para identificar, contactar o ubicar a una persona individual (como un ID de cookie).

## ¿Qué es un gráfico de identidad privado?

Un gráfico de identidad privada es un mapa privado de las relaciones entre identidades vinculadas y vinculadas, visible únicamente para su organización.

Cuando se incluye más de una identidad en cualquier dato ingerido desde un extremo de flujo o enviado a un conjunto de datos habilitado para [!DNL Identity Service], estas identidades se vinculan en el Gráfico de identidad privada. [!DNL Identity Service] aprovecha este gráfico para crear identidades brillantes para un consumidor o entidad determinado, lo que permite la vinculación de identidad y la combinación de perfiles.

## ¿Cómo se crean varios campos de identidad dentro de un esquema XDM?

[Los esquemas del Modelo de datos de experiencia (XDM)](../xdm/home.md) admiten varios campos de identidad. Cualquier campo de datos de tipo `string` dentro de un esquema que implemente la clase XDM Individual Perfil o XDM ExperienceEvent puede etiquetarse como campo de identidad. Una vez etiquetados, los datos contenidos en estos campos se agregan al mapa de identidad del perfil.

Para ver los pasos sobre cómo etiquetar un campo XDM como un campo de identidad mediante la interfaz de usuario, consulte la sección [](../xdm/tutorials/create-schema-ui.md) Identidad en el tutorial Editor de Esquemas. Si está utilizando la API, consulte la sección [Descriptor de](../xdm/tutorials/create-schema-api.md) identidad en el tutorial de la API del Registro de Esquema.

## ¿Existen contextos en los que algunos campos no deben etiquetarse como identidades?

Los campos de identidad deben reservarse para valores que sean únicos para cada individuo. Por ejemplo: considere un conjunto de datos para un programa de lealtad del cliente. El campo &quot;nivel de lealtad&quot; (oro, plata, bronce) no sería un campo de identidad útil, mientras que el ID de lealtad (un valor único) lo sería.

Los campos como códigos postales y direcciones IP no deben etiquetarse como identidades para individuos, ya que estos valores pueden aplicarse a más de una persona individual. Estos tipos de campos sólo deben etiquetarse como identidades para estrategias de mercadotecnia a nivel de los hogares.

## ¿Por qué mis campos de identidad no vinculan la manera esperada?

Mediante el uso del [`/cluster/members` extremo](./api/list-cluster-identites.md) en la API de servicio de identidad, puede realizar la vista de las identidades asociadas para uno o varios campos de identidad. Si la respuesta no devuelve las identidades vinculadas que espera, asegúrese de proporcionar la información de identidad adecuada en los datos XDM. Consulte la sección sobre [proporcionar datos XDM a Identity Service](./home.md) en la descripción general de Identity Service para obtener más información.

## ¿Qué es una Área de nombres de identidad?

Una Área de nombres de identidad proporciona contexto para la forma en que los campos de identidad se relacionan con la identidad del cliente. Por ejemplo, los campos de identidad bajo la Área de nombres &quot;Correo electrónico&quot; deben cumplir con un formato del correo electrónico estándar (nombre<span>@emailprovider.com), mientras que los campos que utilizan la Área de nombres &quot;Teléfono&quot; deben cumplir con un número de teléfono estándar (como 987-555-1234 en Norteamérica).

Las Áreas de nombres distinguen valores de identidad similares entre diferentes sistemas CRM. Por ejemplo, considere un perfil que contenga un ID de lealtad numérico asociado con el programa de recompensas de su compañía. Una Área de nombres de &quot;Lealtad&quot; separaría este valor de un ID numérico similar para el sistema de comercio electrónico que también aparece en el mismo perfil.

Consulte la descripción general [de la Área de nombres de](./home.md) identidad para obtener más información.

## ¿Cómo asocio una identidad con una Área de nombres de identidad?

Los campos de identidad deben asociarse con una Área de nombres de identidad existente cuando se crean. Las Áreas de nombres nuevas deben [crearse con la API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de asociarlas a campos de identidad.

Para obtener instrucciones paso a paso para definir una Área de nombres al crear un descriptor de identidad mediante la API, consulte la sección sobre la [creación de un descriptor](../xdm/tutorials/create-schema-ui.md) en la guía para desarrolladores de Esquema Registry. Para marcar un campo de esquema como una identidad en la interfaz de usuario, siga los pasos del tutorial [Editor de](../xdm/tutorials/create-schema-api.md)Esquemas.

## ¿Cuáles son las Áreas de nombres de identidad estándar proporcionadas por el Experience Platform?

Todas las organizaciones del Experience Platform proporcionan las siguientes Áreas de nombres estándar:

| Nombre para mostrar | ID | Código | Descripción |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | nombre heredado: &quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias: &quot;ID de Adobe Marketing Cloud&quot;, &quot;ID de Adobe Experience Cloud&quot;, &quot;ID de Adobe Experience Platform&quot; |
| Correo electrónico | 6 | Correo electrónico |  |
| Correo electrónico (SHA256, minúscula) | 11 | Correos electrónicos | Área de nombres estándar para correo electrónico predefinido. Los valores proporcionados en esta Área de nombres se convierten en minúsculas antes de utilizar el hash SHA-256. |
| Phone | 7 | Phone |  |
| AID de Windows | 8 | WAID |  |
| Adcloud | 411 | Adcloud | alias: Ad Cloud |
| Adobe Target | 9 | TNTID | ID de Destinatario |
| ID de publicidad de Google | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID para anunciantes |

## ¿Dónde puedo encontrar la lista de Áreas de nombres de identidad disponibles para mi organización?

Mediante la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)servicio de identidad, puede realizar una lista de todas las Áreas de nombres de identidad disponibles para su organización mediante una solicitud GET al `/idnamespace/identities` extremo. Consulte la sección sobre [listado de Áreas de nombres](./api/list-namespaces.md) disponibles en la descripción general de la API de servicio de identidad para obtener más información.

## ¿Cómo creo una Área de nombres personalizada para mi organización?

Mediante la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)servicio de identidad, puede crear una Área de nombres de identidad personalizada para su organización realizando una solicitud POST al `/idnamespace/identities` extremo. Consulte la sección sobre la [creación de una Área de nombres](./api/create-custom-namespace.md) personalizada en la descripción general de la API de servicio de identidad para obtener más información.

## ¿Qué son las identidades compuestas y los XID?

En las llamadas de API se hace referencia a las identidades mediante su identidad compuesta o XID. Una identidad **** compuesta es una representación de una identidad que contiene un valor de ID y una Área de nombres. Un **XID** es un identificador de un solo valor que representa la misma construcción que una identidad compuesta (un ID y una Área de nombres) y se asigna automáticamente a nuevas identidades cuando lo mantiene Identity Service. Consulte la descripción general [de la API de servicio de](./home.md) identidad para obtener más información.

## ¿Cómo gestiona Identity Service la información de identificación personal (PII)?

Identity Service crea un hash criptográfico unidireccional sólido de PII antes de los valores persistentes. Los datos de identidad de las Áreas de nombres &quot;Teléfono&quot; y &quot;Correo electrónico&quot; se etiquetan automáticamente mediante SHA-256, con valores de &quot;Correo electrónico&quot; convertidos automáticamente a minúsculas antes de los hash.

## ¿Debería cifrar toda la PII antes de enviarla a Platform?

No es necesario cifrar manualmente los datos PII antes de ingerirlos en Platform. Al aplicar la etiqueta de uso de datos a todos los campos de datos aplicables, Platform convierte automáticamente estos campos en valores de ID con hash tras la ingestión. `I1`

Para ver los pasos sobre cómo aplicar y administrar etiquetas de uso de datos, consulte el tutorial [de etiquetas de uso de](../data-governance/labels/user-guide.md)datos.

## ¿Hay alguna consideración al ocultar identidades basadas en PII?

Si va a enviar valores PII con hash a Identity Service, debe utilizar el mismo método de codificación en todos los conjuntos de datos. Esto garantiza que el mismo valor de identidad en todos los conjuntos de datos genere los mismos valores hash y que se pueda hacer coincidir y vincular correctamente en el gráfico de identidad.

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

## Resolución de problemas

En la sección siguiente se proporcionan sugerencias para la resolución de problemas de códigos de error específicos y comportamientos inesperados que puede encontrar al trabajar con la [!DNL Identity Service] API.

## [!DNL Identity Service] mensajes de error

La siguiente es una lista de mensajes de error que puede encontrar al usar la [!DNL Identity Service] API.

### Falta el parámetro de consulta requerido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Este error se muestra cuando no se incluyó un parámetro de consulta requerido en la ruta de la solicitud. El nombre `detail` del mensaje de error proporciona el nombre del parámetro que falta. Las variaciones de este mensaje de error incluyen:

- Falta el parámetro de consulta requerido - nsId
- Falta el parámetro de consulta requerido - id
- Falta el parámetro de consulta requerido - xid o (nsid,id)
- Falta el parámetro de consulta requerido - targetNs
- Falta el parámetro de consulta requerido: xids o compositorXids

Compruebe que está incluyendo correctamente el parámetro indicado en la ruta de la solicitud antes de intentarlo de nuevo.

### La marca de tiempo debe estar dentro de los últimos 180 días

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] purga datos de más de 180 días. Este mensaje de error se muestra cuando intenta acceder a datos anteriores a este.

### Hay un límite de 1000 XID en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad para más del número máximo de [XID](#what-are-composite-identities-and-xids) permitidos en una sola llamada de API. Reduzca el número de XID en la solicitud a menos del límite mostrado para resolver este problema.


### Hay un límite para 1000 compositoresXids en una sola llamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Este mensaje de error se muestra cuando intenta recuperar información de identidad para más del número máximo de identidades [](#what-are-composite-identities-and-xids) compuestas permitido en una sola llamada de API. Reduzca el número de identidades compuestas en la solicitud a menos del límite mostrado para resolver este problema.

### El tipo de gráfico especificado no es válido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Este mensaje de error se muestra cuando se asigna un valor no válido a un parámetro de `graph-type` consulta en la ruta de la solicitud. Consulte la sección sobre gráficos [de](./home.md) identidad en la [!DNL Identity Service] información general para saber qué tipos de gráficos son compatibles.

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

En el caso de este error, el token de acceso no es válido. Los Tokenes de acceso caducan cada 24 horas y deben regenerarse para continuar usando [!DNL Platform] API. Consulte el tutorial [de](../tutorials/authentication.md) autenticación para obtener instrucciones sobre cómo generar nuevos tokenes de acceso.

### El token del servicio de autorización no es válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

En el caso de este error, el token de acceso no es válido. Los Tokenes de acceso caducan cada 24 horas y deben regenerarse para continuar usando [!DNL Platform] API. Consulte el tutorial [de](../tutorials/authentication.md) autenticación para obtener instrucciones sobre cómo generar nuevos tokenes de acceso.

### El token de usuario no tiene un contexto de producto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Este mensaje de error se muestra cuando el token de acceso no se ha generado a partir de una [!DNL Experience Platform] integración. Consulte el tutorial [de](../tutorials/authentication.md) autenticación para obtener instrucciones sobre cómo generar nuevos tokenes de acceso para una [!DNL Experience Platform] integración.

### Error interno al obtener XID nativo de la identidad y el código de Área de nombres

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Cuando [!DNL Identity Service] persiste una identidad, se asigna al ID de identidad y al ID de Área de nombres asociado un identificador único denominado XID. Este mensaje se muestra cuando se produce un error durante el proceso de búsqueda del XID para un valor de ID y una Área de nombres determinados.

### La organización IMS no está aprovisionada para [!DNL Identity Service] uso

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

Este error se muestra cuando se produce una excepción inesperada en la ejecución de una llamada de [!DNL Platform] servicio. Se recomienda realizar el programa de las llamadas automatizadas para volver a intentar sus solicitudes varias veces en un intervalo de tiempo al recibir este error. Si el problema persiste, póngase en contacto con el administrador del sistema.

## Códigos de error de ingestión de lotes

[!DNL Identity Service] ingiere datos de identidad de datos de registros y series temporales que se cargan en [!DNL Platform] mediante la ingesta por lotes. Dado que la ingestión por lotes es un proceso asincrónico, debe realizar la vista de los detalles de un lote a los errores de vista. Los errores se acumulan a medida que el lote avanza hasta que se completa.

A continuación se muestra una lista de mensajes de error relacionados con [!DNL Identity Service] el uso de la API [de inserción de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)datos.

### esquema XDM desconocido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] solo consume identidades para datos de registros o series temporales que se ajustan a las [!DNL Profile] clases o [!DNL ExperienceEvent] , respectivamente. Al intentar ingestar datos para los [!DNL Identity Service] que no se adhieren a ninguna de las clases, se activará este error.

### Hubo 0 identidades válidas en las primeras 100 filas del lote procesado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Este error se muestra cuando las primeras 100 filas de un lote no presentaron identidades. Sin embargo, este error no indica de manera concluyente que no se hayan encontrado identidades en registros posteriores.

### Se omitieron los registros porque sólo tenían una identidad por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] solo vincula identidades cuando los registros únicos presentan dos o más valores de identidad. Este mensaje de error se produce una vez por cada lote ingestado y muestra el número de registros en los que sólo se encontró una identidad y no se produjo ningún cambio en el gráfico de identidad.

### El código de Área de nombres no está registrado para esta organización IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Este error se muestra cuando un registro ingestado presenta una identidad cuya Área de nombres asociada no existe o no es accesible para la organización de IMS.

### Omitiendo la ingestión por lotes, ya que la organización IMS no está aprovisionada para Private Identity Graph

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

Este error se muestra cuando se produce una excepción inesperada durante una ingesta por lotes. Se recomienda realizar el programa de las llamadas automatizadas para volver a intentar sus solicitudes varias veces en un intervalo de tiempo al recibir este error. Si el problema persiste, póngase en contacto con el administrador del sistema.
