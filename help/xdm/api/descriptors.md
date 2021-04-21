---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;descriptor;descriptor;descriptores;descriptores;descriptores;identidad;identidad;nombre descriptivo;nombre reconocible;alternatedisplayinfo;referencia;relación;relación
solution: Experience Platform
title: Punto final de API de descriptores
description: El extremo /descriptors de la API del Registro de esquemas permite administrar mediante programación los descriptores XDM dentro de la aplicación de experiencia.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 1%

---

# Punto final del descriptor

Los esquemas definen una vista estática de las entidades de datos, pero no proporcionan detalles específicos sobre cómo los datos basados en estos esquemas (conjuntos de datos, por ejemplo) pueden relacionarse entre sí. Adobe Experience Platform permite describir estas relaciones y otros metadatos interpretativos sobre un esquema con descriptores.

Los descriptores de esquema son metadatos de nivel de inquilino, lo que significa que son únicos para su organización de IMS y todas las operaciones de descriptor se realizan en el contenedor de inquilino.

Cada esquema puede tener una o más entidades descriptor de esquema aplicadas a él. Cada entidad descriptor de esquema incluye un descriptor `@type` y el `sourceSchema` al que se aplica. Una vez aplicados, estos descriptores se aplican a todos los conjuntos de datos creados con el esquema .

El extremo `/descriptors` de la API [!DNL Schema Registry] le permite administrar mediante programación los descriptores dentro de la aplicación de experiencia.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recupere una lista de descriptores {#list}

Puede enumerar todos los descriptores definidos por su organización realizando una solicitud de GET a `/tenant/descriptors`.

**Formato de API**

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
>Los descriptores requieren encabezados `Accept` únicos que reemplacen `xed` por `xdm` y también ofrecen una opción `link` que es única para los descriptores. Los encabezados `Accept` adecuados se han incluido en las llamadas de ejemplos siguientes, pero tenga especial cuidado para asegurarse de que se utilizan los encabezados correctos al trabajar con descriptores.

| `Accept` header | Descripción |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Devuelve una matriz de ID de descriptor |
| `application/vnd.adobe.xdm-link+json` | Devuelve una matriz de rutas de API de descriptor |
| `application/vnd.adobe.xdm+json` | Devuelve una matriz de objetos descriptor expandidos |
| `application/vnd.adobe.xdm-v2+json` | Este encabezado `Accept` debe usarse para utilizar las capacidades de paginación. |

**Respuesta**

La respuesta incluye una matriz para cada tipo de descriptor que tiene descriptores definidos. En otras palabras, si no hay descriptores de un `@type` determinado definido, el registro no devolverá una matriz vacía para ese tipo de descriptor.

Al utilizar el encabezado `link` `Accept`, cada descriptor se muestra como un elemento de matriz con el formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Si desea ver los detalles de un descriptor específico, puede buscar (GET) un descriptor individual usando su `@id`.

**Formato de API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea buscar. |

**Solicitud**

La siguiente solicitud recupera un descriptor por su valor `@id`. Los descriptores no tienen versiones, por lo tanto no se requiere ningún encabezado `Accept` en la solicitud de consulta.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor, incluidos su `@type` y `sourceSchema`, así como información adicional que varía según el tipo de descriptor. El `@id` devuelto debe coincidir con el descriptor `@id` proporcionado en la solicitud.

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

Puede crear un nuevo descriptor realizando una solicitud de POST al extremo `/tenant/descriptors` .

>[!IMPORTANT]
>
>El [!DNL Schema Registry] permite definir varios tipos de descriptor diferentes. Cada tipo de descriptor requiere que se envíen sus propios campos específicos en el cuerpo de la solicitud. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

**Formato de API**

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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles del descriptor recién creado, incluido su `@id`. El `@id` es un campo de solo lectura asignado por el [!DNL Schema Registry] y utilizado para hacer referencia al descriptor en la API.

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

**Formato de API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea actualizar. |

**Solicitud**

Esta solicitud básicamente reescribe el descriptor, por lo que el cuerpo de la solicitud debe incluir todos los campos necesarios para definir un descriptor de ese tipo. En otras palabras, la carga útil de la solicitud para actualizar (PUT) un descriptor es la misma que la carga útil para [crear (POST) un descriptor](#create) del mismo tipo.

>[!IMPORTANT]
>
>Al igual que con la creación de descriptores mediante solicitudes de POST, cada tipo de descriptor requiere que sus propios campos específicos se envíen en cargas de solicitud de PUT. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

El siguiente ejemplo actualiza un descriptor de identidad para que haga referencia a un `xdm:sourceProperty` diferente (`mobile phone`) y cambie el `xdm:namespace` a `Phone`.

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

Al realizar una solicitud [lookup (GET)](#lookup) para ver el descriptor, se mostrará que los campos se han actualizado para reflejar los cambios enviados en la solicitud del PUT.

## Eliminar un descriptor {#delete}

En ocasiones, es posible que tenga que eliminar un descriptor que haya definido de [!DNL Schema Registry]. Esto se hace haciendo una solicitud de DELETE que hace referencia al `@id` del descriptor que desea eliminar.

**Formato de API**

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

Para confirmar que el descriptor se ha eliminado, puede realizar una [solicitud de consulta](#lookup) con el descriptor `@id`. La respuesta devuelve el estado HTTP 404 (no encontrado) porque el descriptor se ha eliminado de [!DNL Schema Registry].

## Apéndice

La siguiente sección proporciona información adicional sobre cómo trabajar con descriptores en la API [!DNL Schema Registry].

### Definición de descriptores {#defining-descriptors}

Las siguientes secciones proporcionan información general sobre los tipos de descriptor disponibles, incluidos los campos obligatorios para definir un descriptor de cada tipo.

#### Descriptor de identidad

Un descriptor de identidad indica que &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; es un campo [!DNL Identity] tal como se describe en [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

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
| `xdm:sourceSchema` | El URI `$id` del esquema en el que se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica que será la identidad. La ruta debe comenzar con &quot;/&quot; y no terminar con una. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, use &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | El valor `id` o `code` del área de nombres de identidad. Se puede encontrar una lista de áreas de nombres usando [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | `xdm:id` o `xdm:code`, según el `xdm:namespace` utilizado. |
| `xdm:isPrimary` | Un valor booleano opcional. Si es true, indica el campo como identidad principal. Los esquemas solo pueden contener una identidad principal. |

#### Descriptor de nombres descriptivos

Los descriptores de nombres descriptivos permiten al usuario modificar los valores `title`, `description` y `meta:enum` de los campos de esquema de la biblioteca principal. Resulta especialmente útil cuando se trabaja con &quot;eVars&quot; y otros campos &quot;genéricos&quot; que desea etiquetar como que contienen información específica de su organización. La IU puede utilizarlos para mostrar un nombre más descriptivo o solo para mostrar campos con un nombre descriptivo.

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
| `xdm:sourceSchema` | El URI `$id` del esquema en el que se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica que será la identidad. La ruta debe comenzar con &quot;/&quot; y no terminar con una. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, use &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | El nuevo título que desea mostrar para este campo, escrito en el caso Título. |
| `xdm:description` | Se puede añadir una descripción opcional junto con el título. |
| `meta:enum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena, `meta:enum` determina la lista de valores sugeridos para el campo en la interfaz de usuario [!DNL Experience Platform]. Es importante tener en cuenta que `meta:enum` no declara una enumeración ni proporciona ninguna validación de datos para el campo XDM.<br><br>Esto solo debe utilizarse para campos XDM principales definidos por el Adobe. Si la propiedad de origen es un campo personalizado definido por su organización, en su lugar debe editar la propiedad `meta:enum` del campo directamente a través de una solicitud de PATCH al recurso principal del campo. |

#### Descriptor de relaciones

Los descriptores de relación describen una relación entre dos esquemas diferentes, basados en las propiedades descritas en `sourceProperty` y `destinationProperty`. Consulte el tutorial sobre la [definición de una relación entre dos esquemas](../tutorials/relationship-api.md) para obtener más información.

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
| `xdm:sourceSchema` | El URI `$id` del esquema en el que se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se está definiendo la relación. Debe comenzar con &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | El URI `$id` del esquema de destino con el que este descriptor define una relación. |
| `xdm:destinationVersion` | La versión principal del esquema de destino. |
| `xdm:destinationProperty` | Ruta opcional a un campo de destino dentro del esquema de destino. Si se omite esta propiedad, el campo de destino se deduce por cualquier campo que contenga un descriptor de identidad de referencia coincidente (consulte a continuación). |


#### Descriptor de identidad de referencia

Los descriptores de identidad de referencia proporcionan un contexto de referencia a la identidad principal de un campo de esquema, lo que permite que los campos de otros esquemas hagan referencia a él. Los campos ya deben etiquetarse con un descriptor de identidad para poder aplicar un descriptor de referencia a ellos.

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
| `xdm:sourceSchema` | El URI `$id` del esquema en el que se está definiendo el descriptor. |
| `xdm:sourceVersion` | Versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se está definiendo el descriptor. Debe comenzar con &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | El código de área de nombres de identidad para la propiedad de origen. |
