---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquemas; registro de esquemas;
solution: Experience Platform
title: Introducción a la API del Registro de esquemas
description: Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API del Registro de esquemas.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# Introducción a [!DNL Schema Registry] API

La variable [!DNL Schema Registry] La API le permite crear y administrar varios recursos del Modelo de datos de experiencia (XDM). Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas al [!DNL Schema Registry] API.

## Requisitos previos

El uso de la guía para desarrolladores requiere comprender bien los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

XDM utiliza el formato de esquema JSON para describir y validar la estructura de los datos de experiencia del cliente incorporados. Por lo tanto, es muy recomendable que revise la [documentación oficial del esquema JSON](https://json-schema.org/) para comprender mejor esta tecnología subyacente.

## Leer llamadas de API de ejemplo

La variable [!DNL Schema Registry] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes al [!DNL Schema Registry], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes de búsqueda (GET) a la variable [!DNL Schema Registry] requerir un `Accept` cuyo valor determina el formato de la información que devuelve la API. Consulte la [Aceptar encabezado](#accept) para obtener más información.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Conozca su TENANT_ID {#know-your-tenant_id}

En todas las guías de API verá referencias a un `TENANT_ID`. Este ID se utiliza para garantizar que los recursos que crea tengan un espacio de nombres adecuado y que estén contenidos dentro de su organización. Si no conoce su ID, puede acceder a él realizando la siguiente solicitud de GET:

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

Una respuesta correcta devuelve información sobre el uso de la variable [!DNL Schema Registry]. Esto incluye un `tenantId` , cuyo valor es su `TENANT_ID`.

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

## Comprender el `CONTAINER_ID` {#container}

Llamadas a la función [!DNL Schema Registry] La API requiere el uso de un `CONTAINER_ID`. Existen dos contenedores para realizar llamadas de API: el `global` y `tenant` contenedor.

### Contenedor global

La variable `global` el contenedor contiene todo el Adobe estándar y [!DNL Experience Platform] clases proporcionadas por el socio, grupos de campos de esquema, tipos de datos y esquemas. Solo puede realizar solicitudes de lista y búsqueda (GET) en el `global` contenedor.

Ejemplo de una llamada que utiliza la variable `global` El contenedor tendría el siguiente aspecto:

```http
GET /global/classes
```

### Contenedor del inquilino

No debe confundirse con su `TENANT_ID`, el `tenant` contiene todas las clases, grupos de campos, tipos de datos, esquemas y descriptores definidos por una organización. Estas son únicas para cada organización, lo que significa que otras organizaciones no las pueden ver ni administrar. Puede realizar todas las operaciones de CRUD (GET, POST, PUT, PATCH, DELETE) con los recursos que cree en la variable `tenant` contenedor.

Ejemplo de una llamada que utiliza la variable `tenant` El contenedor tendría el siguiente aspecto:

```http
POST /tenant/fieldgroups
```

Cuando se crea una clase, un grupo de campos, un esquema o un tipo de datos en la variable `tenant` contenedor, se guarda en el [!DNL Schema Registry] y se ha asignado un `$id` URI que incluye su `TENANT_ID`. Esta `$id` se utiliza en toda la API para hacer referencia a recursos específicos. Ejemplos de `$id` se proporcionan en la siguiente sección.

## Identificación de recursos {#resource-identification}

Los recursos XDM se identifican con un `$id` en forma de URI, como los siguientes ejemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para hacer que el URI sea más sencillo de REST, los esquemas también tienen una codificación de notación de puntos del URI en una propiedad denominada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Llamadas a la función [!DNL Schema Registry] La API admitirá la codificación URL `$id` URI o `meta:altId` (formato de notación de puntos). Una práctica recomendada es usar la codificación URL `$id` URI al realizar una llamada REST a la API, como así:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceptar encabezado {#accept}

Al realizar operaciones de lista y búsqueda (GET) en la variable [!DNL Schema Registry] API, una `Accept` para determinar el formato de los datos devueltos por la API. Al buscar recursos específicos, también debe incluirse un número de versión en la variable `Accept` encabezado.

La siguiente tabla enumera las listas compatibles `Accept` valores de encabezado, incluidos los que tienen números de versión, junto con descripciones de lo que la API devolverá cuando se utilicen.

| Accept | Descripción |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Devuelve solo una lista de ID. Esto se utiliza generalmente para enumerar recursos. |
| `application/vnd.adobe.xed+json` | Devuelve una lista del esquema JSON completo con el original `$ref` y `allOf` incluido. Se utiliza para devolver una lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos y `allOf` resuelto. Tiene títulos y descripciones. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM sin procesar con `$ref` y `allOf`. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` atributos y `allOf` resuelto. Sin títulos ni descripciones. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` atributos y `allOf` resuelto. Se incluyen los descriptores. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` y `allOf` resuelto, tiene títulos y descripciones. Los campos obsoletos se indican con un `meta:status` atributo de `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Actualmente, Platform solo admite una versión principal para cada esquema (`1`). Por lo tanto, el valor de `version` debe ser siempre `1` al realizar solicitudes de búsqueda para devolver la última versión menor del esquema. Consulte la subsección siguiente para obtener más información sobre el control de versiones de esquemas.

### Versiones de esquemas {#versioning}

Las versiones de esquema a las que se hace referencia en `Accept` encabezados en la API del Registro de esquemas y en `schemaRef.contentType` propiedades en cargas útiles de API del servicio de Platform descendente.

Actualmente, Platform solo admite una única versión principal (`1`) para cada esquema. Según el [reglas de evolución de esquema](../schema/composition.md#evolution), cada actualización a un esquema debe ser no destructiva, lo que significa que las nuevas versiones secundarias de un esquema (`1.2`, `1.3`, etc.) siempre son compatibles con versiones anteriores menores. Por lo tanto, al especificar `version=1`, el Registro de esquemas siempre devuelve la variable **última versión** versión principal `1` de un esquema , lo que significa que no se devuelven las versiones secundarias anteriores.

>[!NOTE]
>
>El requisito no destructivo para la evolución del esquema solo se aplica después de que un conjunto de datos haya hecho referencia al esquema y de que uno de los siguientes casos sea verdadero:
>
>* Se han introducido datos en el conjunto de datos.
>* El conjunto de datos se ha habilitado para su uso en el perfil del cliente en tiempo real (incluso si no se han introducido datos).
>
>Si el esquema no se ha asociado con un conjunto de datos que cumpla uno de los criterios anteriores, se puede realizar cualquier cambio en él. Sin embargo, en todos los casos la variable `version` el componente sigue en estado `1`.

## Restricciones del campo XDM y prácticas recomendadas

Los campos de un esquema se enumeran dentro de su `properties` objeto. Cada campo es un objeto, que contiene atributos para describir y restringir los datos que el campo puede contener. Consulte la guía de [definición de campos personalizados en la API](../tutorials/custom-fields-api.md) para muestras de código y restricciones opcionales para los tipos de datos más utilizados.

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

* El nombre de un objeto de campo puede contener caracteres alfanuméricos, guiones o guiones bajos, pero **no podrá** empiece con un guion bajo.
   * **Correcto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrecto:** `_fieldName`
* camelCase es preferible para el nombre del objeto de campo. Ejemplo: `fieldName`
* El campo debe incluir un `title`, escrito en el caso del título. Ejemplo: `Field Name`
* El campo requiere un `type`.
   * La definición de ciertos tipos puede requerir una `format`.
   * Cuando sea necesario un formato específico de los datos, `examples` se puede agregar como una matriz.
   * El tipo de campo también se puede definir utilizando cualquier tipo de datos en el registro. Consulte la sección sobre [creación de un tipo de datos](./data-types.md#create) en la guía de extremo de tipos de datos para obtener más información.
* La variable `description` explica el campo y la información pertinente sobre los datos de campo. Debe escribirse en frases completas con un lenguaje claro para que cualquier persona que acceda al esquema pueda comprender la intención del campo.

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Schema Registry] , seleccione una de las guías de punto final disponibles.
