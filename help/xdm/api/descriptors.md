---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: Descriptores
description: El extremo /descriptors de la API del Registro de Esquema le permite administrar mediante programación descriptores XDM dentro de la aplicación de experiencia.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 1%

---


# Extremo de descriptores

Los esquemas definen una vista estática de las entidades de datos, pero no proporcionan detalles específicos sobre cómo los datos basados en estos esquemas (conjuntos de datos, por ejemplo) pueden relacionarse entre sí. Adobe Experience Platform le permite describir estas relaciones y otros metadatos interpretativos sobre un esquema mediante descriptores.

Los descriptores de esquema son metadatos de nivel de inquilino, lo que significa que son exclusivos de la organización de IMS y todas las operaciones de descriptor se realizan en el contenedor de inquilino.

Cada esquema puede tener una o varias entidades descriptoras de esquema aplicadas. Cada entidad descriptor de esquema incluye un descriptor `@type` y el `sourceSchema` al que se aplica. Una vez aplicados, estos descriptores se aplicarán a todos los conjuntos de datos creados mediante el esquema.

El extremo `/descriptors` de la API [!DNL Schema Registry] le permite administrar mediante programación descriptores dentro de la aplicación de experiencia.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

## Recuperar una lista de descriptores {#list}

Puede realizar una lista de todos los descriptores que haya definido su organización haciendo una solicitud de GET a `/tenant/descriptors`.

**Formato API**

```http
GET /tenant/descriptors
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Observe que el extremo `/descriptors` utiliza encabezados `Accept` diferentes a todos los demás extremos de la API [!DNL Schema Registry].

>[!IMPORTANT]
>
>Los descriptores requieren encabezados `Accept` únicos que reemplazan a `xed` por `xdm` y también oferta una opción `link` que es única para los descriptores. Los encabezados `Accept` adecuados se han incluido en las llamadas de ejemplos siguientes, pero tenga especial cuidado de asegurarse de que se utilizan los encabezados correctos al trabajar con descriptores.

| `Accept` header | Descripción |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Devuelve una matriz de ID de descriptor |
| `application/vnd.adobe.xdm-link+json` | Devuelve una matriz de rutas de API descriptivas |
| `application/vnd.adobe.xdm+json` | Devuelve una matriz de objetos descriptivos expandidos |
| `application/vnd.adobe.xdm-v2+json` | Este encabezado `Accept` debe utilizarse para utilizar las capacidades de paginación. |

**Respuesta**

La respuesta incluye una matriz para cada tipo de descriptor que tiene descriptores definidos. En otras palabras, si no hay descriptores de una `@type` determinada definida, el Registro no devolverá una matriz vacía para ese tipo de descriptor.

Al utilizar el encabezado `link` `Accept`, cada descriptor se muestra como un elemento de matriz en formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Buscar un descriptor {#lookup}

Si desea realizar una vista de los detalles de un descriptor específico, puede buscar (GET) un descriptor individual utilizando su `@id`.

**Formato API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea buscar. |

**Solicitud**

La siguiente solicitud recupera un descriptor por su valor `@id`. Los descriptores no tienen versiones, por lo tanto no se requiere el encabezado `Accept` en la solicitud de búsqueda.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor, incluidos sus `@type` y `sourceSchema`, así como información adicional que varía según el tipo de descriptor. El `@id` devuelto debe coincidir con el descriptor `@id` proporcionado en la solicitud.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Crear un descriptor {#create}

Puede crear un nuevo descriptor realizando una solicitud de POST al extremo `/tenant/descriptors`.

>[!IMPORTANT]
>
>El [!DNL Schema Registry] permite definir varios tipos de descriptores diferentes. Cada tipo de descriptor requiere que se envíen sus propios campos específicos en el cuerpo de la solicitud. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

**Formato API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud define un descriptor de identidad en un campo &quot;dirección de correo electrónico&quot; de un esquema de ejemplo. Esto indica a [!DNL Experience Platform] que utilice la dirección de correo electrónico como identificador para ayudar a unir información sobre el individuo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles del descriptor recién creado, incluido su `@id`. El `@id` es un campo de sólo lectura asignado por el [!DNL Schema Registry] y utilizado para hacer referencia al descriptor en la API.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Actualizar un descriptor {#put}

Puede actualizar un descriptor incluyendo su `@id` en la ruta de una solicitud de PUT.

**Formato API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea actualizar. |

**Solicitud**

Esta solicitud esencialmente vuelve a escribir el descriptor, de modo que el cuerpo de la solicitud debe incluir todos los campos necesarios para definir un descriptor de ese tipo. En otras palabras, la carga útil de solicitud para actualizar (PUT) un descriptor es la misma que la carga útil para [crear (POST) un descriptor](#create) del mismo tipo.

>[!IMPORTANT]
>
>Al igual que con la creación de descriptores mediante solicitudes de POST, cada tipo de descriptor requiere que se envíen sus propios campos específicos en las cargas de solicitud de PUT. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

El ejemplo siguiente actualiza un descriptor de identidad para hacer referencia a un `xdm:sourceProperty` (`mobile phone`) diferente y cambiar el `xdm:namespace` a `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y el `@id` del descriptor actualizado (que debe coincidir con el `@id` enviado en la solicitud).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Al realizar una solicitud [de búsqueda (GET)](#lookup) para la vista del descriptor, se mostrará que los campos se han actualizado para reflejar los cambios enviados en la solicitud de PUT.

## Eliminar un descriptor {#delete}

En ocasiones, es posible que deba eliminar un descriptor que haya definido de [!DNL Schema Registry]. Esto se realiza haciendo una solicitud de DELETE que hace referencia al `@id` descriptor que desea eliminar.

**Formato API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea eliminar. |

**Solicitud**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar que el descriptor se ha eliminado, puede realizar una [solicitud de búsqueda](#lookup) con el descriptor `@id`. La respuesta devuelve el estado HTTP 404 (no encontrado) porque el descriptor se ha eliminado de [!DNL Schema Registry].

## Apéndice

La siguiente sección proporciona información adicional sobre cómo trabajar con descriptores en la API [!DNL Schema Registry].

### Definición de descriptores {#defining-descriptors}

Las siguientes secciones proporcionan información general sobre los tipos de descriptor disponibles, incluidos los campos obligatorios para definir un descriptor de cada tipo.

#### Descriptor de identidad

Un descriptor de identidad indica que &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; es un campo [!DNL Identity] como lo describe [Adobe Experience Platform Identity Service](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. |
| `xdm:sourceSchema` | El URI `$id` del esquema donde se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica que será la identidad. La ruta debe comenzar con &quot;/&quot; y no terminar con una. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, utilice &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | El valor `id` o `code` de la Área de nombres de identidad. Se puede encontrar una lista de Áreas de nombres usando el [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | `xdm:id` o `xdm:code`, según el `xdm:namespace` utilizado. |
| `xdm:isPrimary` | Un valor booleano opcional. Si es true, indica el campo como identidad principal. Los esquemas solo pueden contener una identidad primaria. |

#### Descriptor de nombres descriptivos

Los descriptores de nombres prácticos permiten al usuario modificar los valores `title`, `description` y `meta:enum` de los campos de esquema de la biblioteca principal. Especialmente útil cuando se trabaja con &quot;eVars&quot; y otros campos &quot;genéricos&quot; que se desea etiquetar como que contienen información específica de su organización. La interfaz de usuario puede utilizarlos para mostrar un nombre más sencillo o solo para mostrar campos con un nombre descriptivo.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. |
| `xdm:sourceSchema` | El URI `$id` del esquema donde se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica que será la identidad. La ruta debe comenzar con &quot;/&quot; y no terminar con una. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, utilice &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | El nuevo título que desea mostrar para este campo, escrito en Caso de título. |
| `xdm:description` | Se puede añadir una descripción opcional junto con el título. |
| `meta:enum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena, `meta:enum` determina la lista de los valores sugeridos para el campo en la interfaz de usuario [!DNL Experience Platform]. Es importante tener en cuenta que `meta:enum` no declara una lista desglosada ni proporciona ninguna validación de datos para el campo XDM.<br><br>Esto solo debe utilizarse para los campos XDM principales definidos por Adobe. Si la propiedad source es un campo personalizado definido por su organización, debe editar la propiedad `meta:enum` del campo directamente a través de una solicitud de PATCH al recurso principal del campo. |

#### Descriptor de relación

Los descriptores de relación describen una relación entre dos esquemas diferentes, basados en las propiedades descritas en `sourceProperty` y `destinationProperty`. Consulte el tutorial sobre [definición de una relación entre dos esquemas](../tutorials/relationship-api.md) para obtener más información.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. |
| `xdm:sourceSchema` | El URI `$id` del esquema donde se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se está definiendo la relación. Debe comenzar con &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | El URI `$id` del esquema de destino con el que este descriptor está definiendo una relación. |
| `xdm:destinationVersion` | Versión principal del esquema de destino. |
| `xdm:destinationProperty` | Ruta opcional a un campo de destinatario dentro del esquema de destino. Si se omite esta propiedad, el campo de destinatario se deduce con cualquier campo que contenga un descriptor de identidad de referencia coincidente (véase más adelante). |


#### Descriptor de identidad de referencia

Los descriptores de identidad de referencia proporcionan un contexto de referencia a la identidad principal de un campo de esquema, lo que permite que los campos de otros esquemas hagan referencia a él. Los campos ya deben etiquetarse con un descriptor de identidad para poder aplicarles un descriptor de referencia.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está definiendo. |
| `xdm:sourceSchema` | El URI `$id` del esquema donde se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se está definiendo el descriptor. Debe comenzar con &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Código de Área de nombres de identidad de la propiedad source. |