---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;Registro de esquemas;
solution: Experience Platform
title: Introducción a la API de Registro de esquemas
description: Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de Registro de esquemas.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 5%

---

# Introducción a la API [!DNL Schema Registry]

La API [!DNL Schema Registry] le permite crear y administrar varios recursos del Modelo de datos de experiencia (XDM). Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API [!DNL Schema Registry].

## Requisitos previos

El uso de la guía para desarrolladores requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

XDM utiliza el formato de esquema JSON para describir y validar la estructura de los datos de experiencia del cliente introducidos. Por lo tanto, se recomienda revisar la [documentación oficial del esquema JSON](https://json-schema.org/) para comprender mejor esta tecnología subyacente.

## Lectura de llamadas de API de muestra

La documentación de la API [!DNL Schema Registry] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de Experience Platform.

## Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de la zona protegida](../../sandboxes/home.md).

Todas las solicitudes de búsqueda (GET) a [!DNL Schema Registry] requieren un encabezado `Accept` adicional, cuyo valor determina el formato de la información devuelta por la API. Consulte la sección [Aceptar encabezado](#accept) a continuación para obtener más detalles.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Conozca su TENANT_ID {#know-your-tenant_id}

A través de las guías de API verá referencias a un(a) `TENANT_ID`. Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización. Si no conoce su ID, puede acceder a él realizando la siguiente petición GET:

**Formato de API**

```http
GET /stats
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve información acerca del uso de [!DNL Schema Registry] por parte de su organización. Esto incluye un atributo `tenantId`, cuyo valor es su `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Comprender `CONTAINER_ID` {#container}

Las llamadas a la API [!DNL Schema Registry] requieren el uso de un `CONTAINER_ID`. Hay dos contenedores en los que se pueden realizar llamadas de API: el contenedor `global` y el contenedor `tenant`.

### Contenedor global

El contenedor `global` contiene todas las clases, los grupos de campos de esquema, los tipos de datos y los esquemas proporcionados por los socios estándar de Adobe y [!DNL Experience Platform]. Solo puede realizar solicitudes de lista y búsqueda (GET) en el contenedor `global`.

Un ejemplo de una llamada que utiliza el contenedor `global` tendría el siguiente aspecto:

```http
GET /global/classes
```

### Contenedor de inquilino

No debe confundirse con su `TENANT_ID` único, el contenedor `tenant` contiene todas las clases, grupos de campos, tipos de datos, esquemas y descriptores definidos por una organización. Son exclusivos de cada organización, lo que significa que no son visibles ni manejables por otras organizaciones. Puede realizar todas las operaciones de CRUD (GET, POST, PUT, PATCH, DELETE) con los recursos que cree en el contenedor `tenant`.

Un ejemplo de una llamada que utiliza el contenedor `tenant` tendría el siguiente aspecto:

```http
POST /tenant/fieldgroups
```

Cuando crea una clase, grupo de campos, esquema o tipo de datos en el contenedor `tenant`, se guarda en [!DNL Schema Registry] y se asigna un URI `$id` que incluye su `TENANT_ID`. Este(a) `$id` se usa en toda la API para hacer referencia a recursos específicos. En la siguiente sección se proporcionan ejemplos de `$id` valores.

## Identificación de recursos {#resource-identification}

Los recursos XDM se identifican con un atributo `$id` en forma de URI, como los siguientes ejemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para que el URI sea más compatible con REST, los esquemas también tienen una codificación de notación de puntos del URI en una propiedad denominada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Las llamadas a la API [!DNL Schema Registry] admitirán el URI `$id` con codificación URL o `meta:altId` (formato de notación de puntos). La práctica recomendada es utilizar el URI `$id` con codificación URL al realizar una llamada REST a la API, de esta manera:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Encabezado Aceptar {#accept}

Al realizar operaciones de lista y búsqueda (GET) en la API [!DNL Schema Registry], se requiere un encabezado `Accept` para determinar el formato de los datos devueltos por la API. Cuando busca recursos específicos, también debe incluir un número de versión en el encabezado `Accept`.

La siguiente tabla enumera los valores de encabezado `Accept` compatibles, incluidos los que tienen números de versión, junto con descripciones de lo que devolverá la API cuando se usen.

| Aceptar | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Devuelve solo una lista de ID. Normalmente se utiliza para enumerar recursos. |
| `application/vnd.adobe.xed+json` | Devuelve una lista de esquema JSON completo con `$ref` y `allOf` originales incluidos. Se utiliza para devolver una lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos y `allOf` resueltos. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` atributos y `allOf` resueltos. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` atributos y `allOf` resueltos. Se incluyen los descriptores. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` y `allOf` resueltos, tiene títulos y descripciones. Los campos obsoletos se indican con un atributo `meta:status` de `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Actualmente, Experience Platform solo admite una versión principal para cada esquema (`1`). Por lo tanto, el valor de `version` siempre debe ser `1` al realizar solicitudes de búsqueda para devolver la última versión secundaria del esquema. Consulte la subsección siguiente para obtener más información sobre el control de versiones de esquemas.

### Versiones de esquema {#versioning}

Los encabezados `Accept` hacen referencia a las versiones de esquema en la API del Registro de esquemas y en las propiedades `schemaRef.contentType` de las cargas útiles de la API del servicio Experience Platform descendente.

Actualmente, Experience Platform solo admite una única versión principal (`1`) para cada esquema. Según las [reglas de evolución de esquema](../schema/composition.md#evolution), cada actualización a un esquema debe ser no destructiva, lo que significa que las nuevas versiones menores de un esquema (`1.2`, `1.3`, etc.) siempre son compatibles con versiones menores anteriores. Por lo tanto, al especificar `version=1`, el Registro de esquemas siempre devuelve la **última** versión principal `1` de un esquema, lo que significa que no se devuelven versiones secundarias anteriores.

>[!NOTE]
>
>El requisito no destructivo para la evolución del esquema solo se aplica después de que un conjunto de datos haya hecho referencia al esquema y uno de los siguientes casos sea verdadero:
>
>* Se han introducido datos en el conjunto de datos.
>* El conjunto de datos se ha habilitado para su uso en el perfil del cliente en tiempo real (incluso si no se han introducido datos).
>
>Si el esquema no se ha asociado a un conjunto de datos que cumple uno de los criterios anteriores, se puede realizar cualquier cambio en él. Sin embargo, en todos los casos el componente `version` permanece en `1`.

## Restricciones de campo XDM y prácticas recomendadas

Los campos de un esquema se enumeran dentro de su objeto `properties`. Cada campo es en sí mismo un objeto, que contiene atributos para describir y restringir los datos que puede contener el campo. Consulte la guía [definición de campos personalizados en la API](../tutorials/custom-fields-api.md) para obtener muestras de código y restricciones opcionales para los tipos de datos más utilizados.

El siguiente campo de ejemplo ilustra un campo XDM con formato correcto, con más detalles sobre las restricciones de nomenclatura y las prácticas recomendadas a continuación. Estas prácticas también se pueden aplicar al definir otros recursos que contienen atributos similares.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* El nombre de un objeto de campo puede contener caracteres alfanuméricos, guiones o guiones bajos, pero **no** puede comenzar con un guion bajo.
   * **Correcto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrecto:** `_fieldName`
* Los nombres de campo no distinguen entre mayúsculas y minúsculas y deben tener nombres diferentes en el mismo nivel del esquema.
* Se prefiere camelCase para el nombre del objeto de campo. Ejemplo: `fieldName`
* El campo debe incluir un `title`, escrito en Mayúsculas y minúsculas. Ejemplo: `Field Name`
* El campo requiere un `type`.
   * La definición de ciertos tipos puede requerir un `format` opcional.
   * Cuando se requiere un formato específico de datos, `examples` se puede agregar como una matriz.
   * El tipo de campo también se puede definir utilizando cualquier tipo de datos del Registro. Consulte la sección sobre [creación de un tipo de datos](./data-types.md#create) en la guía de extremo de tipos de datos para obtener más información.
* `description` explica el campo y la información relevante con respecto a los datos de campo. Debe escribirse en frases completas con un lenguaje claro para que cualquier persona que acceda al esquema pueda comprender la intención del campo.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Schema Registry], seleccione una de las guías de extremos disponibles.
