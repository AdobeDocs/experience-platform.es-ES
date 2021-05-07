---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquemas; registro de esquemas;
solution: Experience Platform
title: Introducción a la API del Registro de esquemas
description: Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API del Registro de esquemas.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Introducción a la API [!DNL Schema Registry]

La API [!DNL Schema Registry] permite crear y administrar varios recursos del Modelo de datos de experiencia (XDM). Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API [!DNL Schema Registry].

## Requisitos previos

El uso de la guía para desarrolladores requiere comprender bien los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

XDM utiliza el formato de esquema JSON para describir y validar la estructura de los datos de experiencia del cliente incorporados. Por lo tanto, se recomienda encarecidamente que revise la [documentación oficial del esquema JSON](https://json-schema.org/) para comprender mejor esta tecnología subyacente.

## Leer llamadas de API de ejemplo

La documentación de la API [!DNL Schema Registry] proporciona ejemplos de llamadas de API para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Schema Registry], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes de búsqueda (GET) al [!DNL Schema Registry] requieren un encabezado `Accept` adicional, cuyo valor determina el formato de la información que devuelve la API. Consulte la sección [Accept header](#accept) a continuación para obtener más información.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Conozca su TENANT_ID {#know-your-tenant_id}

En todas las guías de API verá referencias a `TENANT_ID`. Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. Si no conoce su ID, puede acceder a él realizando la siguiente solicitud de GET:

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve información sobre el uso del [!DNL Schema Registry] por parte de su organización. Esto incluye un atributo `tenantId`, cuyo valor es su `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "fieldgroups": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
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
      "meta:resourceType": "fieldgroups",
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

## Comprender el `CONTAINER_ID` {#container}

Las llamadas a la API [!DNL Schema Registry] requieren el uso de `CONTAINER_ID`. Existen dos contenedores para realizar llamadas de API: el contenedor `global` y el contenedor `tenant`.

### Contenedor global

El contenedor `global` contiene todos los Adobes estándar y el socio [!DNL Experience Platform] proporciona clases, grupos de campos de esquema, tipos de datos y esquemas. Solo puede realizar solicitudes de lista y búsqueda (GET) contra el contenedor `global` .

Un ejemplo de una llamada que utiliza el contenedor `global` tendría el siguiente aspecto:

```http
GET /global/classes
```

### Contenedor del inquilino

No se debe confundir con su `TENANT_ID` único, el contenedor `tenant` contiene todas las clases, grupos de campos, tipos de datos, esquemas y descriptores definidos por una organización de IMS. Estas son únicas para cada organización, lo que significa que otras organizaciones IMS no las pueden ver ni administrar. Puede realizar todas las operaciones de CRUD (GET, POST, PUT, PATCH, DELETE) con los recursos que cree en el contenedor `tenant`.

Un ejemplo de una llamada que utiliza el contenedor `tenant` tendría el siguiente aspecto:

```http
POST /tenant/fieldgroups
```

Cuando se crea una clase, un grupo de campos, un esquema o un tipo de datos en el contenedor `tenant`, se guarda en el [!DNL Schema Registry] y se asigna un URI `$id` que incluye su `TENANT_ID`. Este `$id` se utiliza en toda la API para hacer referencia a recursos específicos. En la siguiente sección se proporcionan ejemplos de valores `$id`.

## Identificación de recursos {#resource-identification}

Los recursos XDM se identifican con un atributo `$id` en forma de URI, como los siguientes ejemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para que el URI sea más sencillo de usar con REST, los esquemas también tienen una codificación de notación de puntos del URI en una propiedad denominada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Las llamadas a la API [!DNL Schema Registry] admitirán el URI `$id` con codificación URL o el `meta:altId` (formato de notación de puntos). Una práctica recomendada es utilizar el URI `$id` con codificación de URL al realizar una llamada REST a la API, de esta manera:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceptar encabezado {#accept}

Al realizar operaciones de lista y búsqueda (GET) en la API [!DNL Schema Registry] , se requiere un encabezado `Accept` para determinar el formato de los datos devueltos por la API. Al buscar recursos específicos, también debe incluirse un número de versión en el encabezado `Accept`.

En la tabla siguiente se enumeran los valores de encabezado `Accept` compatibles, incluidos los que tienen números de versión, así como las descripciones de lo que la API devolverá cuando se utilicen.

| Accept | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Devuelve solo una lista de ID. Esto se utiliza generalmente para enumerar recursos. |
| `application/vnd.adobe.xed+json` | Devuelve una lista del esquema JSON completo con el `$ref` original y `allOf` incluido. Se utiliza para devolver una lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` y  `allOf` resuelto. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` y  `allOf` resuelto. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` y  `allOf` resuelto. Se incluyen los descriptores. |

>[!NOTE]
>
>Actualmente, Platform solo admite una versión principal para cada esquema (`1`). Por lo tanto, el valor de `version` siempre debe ser `1` al realizar solicitudes de búsqueda para devolver la última versión secundaria del esquema. Consulte la subsección siguiente para obtener más información sobre el control de versiones de esquemas.

### Versiones del esquema {#versioning}

Los encabezados `Accept` hacen referencia a las versiones de esquema en la API del Registro de esquemas y en las `schemaRef.contentType` propiedades en las cargas útiles de API del servicio de Platform descendente.

Actualmente, Platform solo admite una única versión principal (`1`) para cada esquema. Según las [reglas de evolución de esquema](../schema/composition.md#evolution), cada actualización de un esquema debe ser no destructiva, lo que significa que las nuevas versiones secundarias de un esquema (`1.2`, `1.3`, etc.) siempre son compatibles con versiones anteriores menores. Por lo tanto, al especificar `version=1`, el Registro de esquemas siempre devuelve la **última** versión principal `1` de un esquema, lo que significa que no se devuelven las versiones menores anteriores.

>[!NOTE]
>
>El requisito no destructivo para la evolución del esquema solo se aplica después de que un conjunto de datos haya hecho referencia al esquema y de que uno de los siguientes casos sea verdadero:
>
>* Se han introducido datos en el conjunto de datos.
>* El conjunto de datos se ha habilitado para su uso en el perfil del cliente en tiempo real (incluso si no se han introducido datos).

>
>
Si el esquema no se ha asociado con un conjunto de datos que cumpla uno de los criterios anteriores, se puede realizar cualquier cambio en él. Sin embargo, en todos los casos el componente `version` permanece en `1`.

## Restricciones del campo XDM y prácticas recomendadas

Los campos de un esquema se muestran dentro de su objeto `properties` . Cada campo es un objeto, que contiene atributos para describir y restringir los datos que el campo puede contener.

Puede encontrar más información sobre la definición de tipos de campo en la API en la [guía de restricciones de campo](../schema/field-constraints.md) para esta guía, que incluye ejemplos de código y restricciones opcionales para los tipos de datos más utilizados.

El siguiente campo de ejemplo ilustra un campo XDM con un formato correcto, con más detalles sobre restricciones de nombres y prácticas recomendadas que se proporcionan a continuación. Estas prácticas también se pueden aplicar al definir otros recursos que contengan atributos similares.

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

* El nombre de un objeto de campo puede contener caracteres alfanuméricos, guiones o guiones bajos, pero **no puede** comenzar con un guión bajo.
   * **Correcto:** `fieldName`,  `field_name2`,  `Field-Name`.  `field-name_3`
   * **Incorrecto:** `_fieldName`
* camelCase es preferible para el nombre del objeto de campo. Ejemplo: `fieldName`
* El campo debe incluir un `title`, escrito en el caso del título. Ejemplo: `Field Name`
* El campo requiere un `type`.
   * La definición de ciertos tipos puede requerir un `format` opcional.
   * Cuando se requiere un formato específico de los datos, se puede agregar `examples` como una matriz.
   * El tipo de campo también se puede definir utilizando cualquier tipo de datos en el registro. Consulte la sección sobre [creación de un tipo de datos](./data-types.md#create) en la guía de extremo de tipos de datos para obtener más información.
* El `description` explica el campo y la información pertinente con respecto a los datos de campo. Debe escribirse en frases completas con un lenguaje claro para que cualquier persona que acceda al esquema pueda comprender la intención del campo.

Consulte el documento sobre [restricciones de campo](../schema/field-constraints.md) para obtener más información sobre cómo definir diferentes tipos de campos en la API.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Schema Registry], seleccione una de las guías de punto final disponibles.
