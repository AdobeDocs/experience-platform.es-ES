---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guía para desarrolladores de API de registro de esquema
description: El Registro de Esquemas se utiliza para acceder a la biblioteca de Esquemas de Adobe Experience Platform, proporcionando una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles. Con la API de Registro de Esquema, puede realizar operaciones CRUD básicas para realizar vistas y administrar todos los esquemas y recursos relacionados disponibles en Adobe Experience Platform.
topic: developer guide
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---


# [!DNL Schema Registry] Guía para desarrolladores de API

El [!DNL Schema Registry] se utiliza para acceder a la biblioteca de Esquemas en Adobe Experience Platform, proporcionando una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles.

Con la API de Registro de Esquema, puede realizar operaciones CRUD básicas para realizar vistas y administrar todos los esquemas y recursos relacionados disponibles en Adobe Experience Platform. Esto incluye los definidos por Adobes, socios [!DNL Experience Platform] y proveedores cuyas aplicaciones utiliza. También puede utilizar llamadas de API para crear nuevos esquemas y recursos para su organización, así como vistas y recursos de edición que ya haya definido.

En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio del uso de la [!DNL Schema Registry] API. A continuación, la guía proporciona llamadas de API de muestra para realizar operaciones clave mediante el [!DNL Schema Registry].

## Requisitos previos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM) [!DNL]](../home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM.
* [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!Sandboxes DNL]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a la [!DNL Schema Registry] API correctamente.

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

## Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Schema Registry], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes de búsqueda (GET) al [!DNL Schema Registry] requieren un encabezado Accept adicional, cuyo valor determina el formato de la información devuelta por la API. Consulte la sección [Aceptar encabezado](#accept) más abajo para obtener más detalles.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Conozca su TENANT_ID {#know-your-tenant_id}

A lo largo de esta guía verá referencias a un `TENANT_ID`. Este ID se utiliza para garantizar que los recursos que cree tengan el espacio de nombres correcto y estén contenidos en la organización de IMS. Si no conoce su ID, puede acceder a él realizando la siguiente solicitud de GET:

**Formato API**

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

Una respuesta correcta devuelve información sobre el uso de la [!DNL Schema Registry]. Esto incluye un `tenantId` atributo cuyo valor es su `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

* `tenantId`:: El `TENANT_ID` valor de la organización de IMS.

## Comprender el `CONTAINER_ID` {#container}

Las llamadas a la [!DNL Schema Registry] API requieren el uso de un `CONTAINER_ID`. Existen dos contenedores para realizar llamadas de API: el contenedor global y el contenedor del inquilino.

### Contenedor global

El contenedor global contiene todas las clases, mezclas, tipos de datos y esquemas proporcionados por el Adobe y [!DNL Experience Platform] el socio estándar. Solo puede realizar solicitudes de lista y búsqueda (GET) en el contenedor global.

Un ejemplo de una llamada que utiliza el contenedor global sería el siguiente:

```http
GET /global/classes
```

### Contenedor del inquilino

No debe confundirse con su único `TENANT_ID`, el contenedor del inquilino contiene todas las clases, mezclas, tipos de datos, esquemas y descriptores definidos por una organización de IMS. Son exclusivas de cada organización, lo que significa que no son visibles ni manejables por otras organizaciones de IMS. Puede realizar todas las operaciones de CRUD (GET, POST, PUT, PATCH, DELETE) con los recursos que cree en el contenedor del inquilino.

Un ejemplo de una llamada que utiliza el contenedor del inquilino sería el siguiente:

```http
POST /tenant/mixins
```

Cuando se crea una clase, una mezcla, un esquema o un tipo de datos en el contenedor del inquilino, se guarda en el  [!DNL Schema Registry] y se asigna un `$id` URI que incluye su `TENANT_ID`. Esto `$id` se utiliza en toda la API para hacer referencia a recursos específicos. En la siguiente sección se proporcionan ejemplos de `$id` valores.

## Identificación del esquema {#schema-identification}

Los esquemas se identifican con un `$id` atributo en forma de URI, como:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para hacer que el URI sea más sencillo con REST, los esquemas también tienen una codificación de notación de puntos del URI en una propiedad denominada `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Las llamadas a la API del Registro de Esquema admitirán el `$id` URI con codificación URL o el `meta:altId` (formato de notación con puntos). Se recomienda utilizar el `$id` URI con codificación de URL al realizar una llamada REST a la API, del siguiente modo:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceptar encabezado {#accept}

Al realizar operaciones de lista y búsqueda (GET) en la [!DNL Schema Registry] API, se requiere un encabezado Accept para determinar el formato de los datos devueltos por la API. Al buscar recursos específicos, también se debe incluir un número de versión en el encabezado Aceptar.

Las siguientes listas de tabla son compatibles con los valores de encabezado Accept, incluidos los que tienen números de versión, junto con las descripciones de lo que la API devolverá cuando se utilicen.

| Aceptar | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Devuelve una lista de ID solamente. Esto se utiliza generalmente para enumerar los recursos. |
| `application/vnd.adobe.xed+json` | Devuelve una lista de esquema JSON completo con original `$ref` e `allOf` incluido. Se utiliza para devolver una lista de recursos completos. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | XDM sin procesar con `$ref` y `allOf`. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` atributos y `allOf` resueltos. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | XDM sin procesar con `$ref` y `allOf`. No hay títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` atributos y `allOf` resueltos. No hay títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` atributos y `allOf` resueltos. Se incluyen los descriptores. |

>[!NOTE]
>
>Si sólo se proporciona la versión `major` (por ejemplo, 1, 2, 3), el registro devolverá la última `minor` versión (por ejemplo: .1, .2, .3) automáticamente.

## Limitaciones y prácticas recomendadas del campo XDM

Los campos de un esquema se muestran dentro de su `properties` objeto. Cada campo es en sí mismo un objeto, que contiene atributos para describir y restringir los datos que el campo puede contener.

Puede encontrar más información sobre la definición de tipos de campo en la API en el [apéndice](appendix.md) de esta guía, incluyendo ejemplos de código y restricciones opcionales para los tipos de datos más utilizados.

El siguiente campo de ejemplo ilustra un campo XDM con un formato adecuado, con más detalles sobre las restricciones de nombres y las prácticas recomendadas que se proporcionan a continuación. Estas prácticas también se pueden aplicar al definir otros recursos que contengan atributos similares.

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

* El nombre de un objeto de campo puede contener caracteres alfanuméricos, guiones o guiones bajos, pero no **puede** tener un inicio con un guión bajo.
   * **Correcto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrecto:** `_fieldName`
* camelCase es preferible para el nombre del objeto de campo. Ejemplo: `fieldName`
* El campo debe incluir un `title`, escrito en Caso de título. Ejemplo: `Field Name`
* El campo requiere un `type`.
   * La definición de determinados tipos puede requerir un `format`valor opcional.
   * Cuando se requiere un formato específico de los datos, se `examples` puede agregar como una matriz.
   * El tipo de campo también se puede definir utilizando cualquier tipo de datos del Registro. Consulte la sección sobre la [creación de un tipo](create-data-type.md) de datos en esta guía para obtener más información.
* El `description` explica el campo y la información pertinente con respecto a los datos de campo. Debe escribirse en oraciones completas con un lenguaje claro para que cualquier persona que acceda al esquema pueda entender la intención del campo.

Consulte el [apéndice](appendix.md) para obtener más información sobre cómo definir los tipos de campo en la API.

## Pasos siguientes

Este documento cubría los conocimientos previos necesarios para realizar llamadas a la [!DNL Schema Registry] API, incluidas las credenciales de autenticación necesarias. Ahora puede continuar con las llamadas de muestra que se proporcionan en esta guía para desarrolladores y seguir sus instrucciones. Para obtener un tutorial paso a paso completo sobre cómo realizar un esquema en la API, consulte el siguiente [tutorial](../tutorials/create-schema-api.md).
