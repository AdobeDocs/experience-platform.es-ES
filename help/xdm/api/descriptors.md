---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;descriptor;Descriptor;descriptores;identity;nombre descriptivo;nombre descriptivo;alternatedisplayinfo;reference;Reference;relation;Relationship
solution: Experience Platform
title: Punto final de API de descriptores
description: El extremo /descriptors de la API de Registro de esquemas le permite administrar mediante programación descriptores XDM dentro de la aplicación de experiencia.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 44355aa2ddf03b20aca64c6675414b73682bc2b5
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 2%

---

# Extremo de descriptores

Los esquemas definen una vista estática de las entidades de datos, pero no proporcionan detalles específicos sobre cómo los datos basados en estos esquemas (conjuntos de datos, por ejemplo) pueden relacionarse entre sí. Adobe Experience Platform permite describir estas relaciones y otros metadatos interpretativos sobre un esquema mediante descriptores.

Los descriptores de esquema son metadatos de nivel de inquilino, lo que significa que son únicos para su organización y que todas las operaciones de descriptor se realizan en el contenedor de inquilino.

Cada esquema puede tener una o más entidades de descriptor de esquema aplicadas. Cada entidad descriptor de esquema incluye un descriptor `@type` y el `sourceSchema` al que se aplica. Una vez aplicados, estos descriptores se aplicarán a todos los conjuntos de datos creados con el esquema.

El extremo `/descriptors` de la API [!DNL Schema Registry] le permite administrar descriptores mediante programación dentro de la aplicación de experiencia.

## Introducción

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de descriptores {#list}

Puede enumerar todos los descriptores que ha definido su organización realizando una solicitud de GET a `/tenant/descriptors`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

El formato de respuesta depende del encabezado `Accept` enviado en la solicitud. Observe que el extremo `/descriptors` utiliza encabezados `Accept` que son diferentes de todos los demás extremos de la API [!DNL Schema Registry].

>[!IMPORTANT]
>
>Los descriptores requieren encabezados `Accept` únicos que reemplazan a `xed` por `xdm`, y también ofrecen la opción `link` que es única para los descriptores. Los encabezados `Accept` adecuados se han incluido en las llamadas de ejemplo siguientes, pero tenga especial precaución para asegurarse de que se utilizan los encabezados correctos al trabajar con descriptores.

| `Accept` encabezado | Descripción |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Devuelve una matriz de ID de descriptor |
| `application/vnd.adobe.xdm-link+json` | Devuelve una matriz de rutas de API de descriptor |
| `application/vnd.adobe.xdm+json` | Devuelve una matriz de objetos descriptor expandidos |
| `application/vnd.adobe.xdm-v2+json` | Se debe usar este encabezado `Accept` para usar las capacidades de paginación. |

{style="table-layout:auto"}

**Respuesta**

La respuesta incluye una matriz para cada tipo de descriptor que tenga descriptores definidos. En otras palabras, si no hay descriptores de un determinado `@type` definido, el Registro no devolverá una matriz vacía para ese tipo de descriptor.

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

## Búsqueda de un descriptor {#lookup}

Si desea ver los detalles de un descriptor específico, puede buscar (GET) un descriptor individual usando su `@id`.

**Formato de API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera un descriptor por su valor `@id`. Los descriptores no tienen versiones, por lo tanto no se requiere ningún encabezado `Accept` en la solicitud de búsqueda.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del descriptor, incluidos `@type` y `sourceSchema`, así como información adicional que varía según el tipo de descriptor. El elemento devuelto `@id` debe coincidir con el descriptor `@id` proporcionado en la solicitud.

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
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Creación de un descriptor {#create}

Puede crear un nuevo descriptor realizando una solicitud de POST al extremo `/tenant/descriptors`.

>[!IMPORTANT]
>
>[!DNL Schema Registry] le permite definir varios tipos de descriptor diferentes. Cada tipo de descriptor requiere que se envíen sus propios campos específicos en el cuerpo de la solicitud. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

**Formato de API**

```http
POST /tenant/descriptors
```

**Solicitud**

La siguiente solicitud define un descriptor de identidad en un campo &quot;dirección de correo electrónico&quot; en un esquema de ejemplo. Esto indica a [!DNL Experience Platform] que use la dirección de correo electrónico como identificador para ayudar a unir información sobre el individuo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles del descriptor recién creado, incluido su `@id`. `@id` es un campo de solo lectura asignado por [!DNL Schema Registry] y utilizado para hacer referencia al descriptor en la API.

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

## Actualización de un descriptor {#put}

Puede actualizar un descriptor incluyendo su `@id` en la ruta de una solicitud de PUT.

**Formato de API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

Básicamente, esta solicitud reescribe el descriptor, por lo que el cuerpo de la solicitud debe incluir todos los campos necesarios para definir un descriptor de ese tipo. En otras palabras, la carga útil de solicitud para actualizar (PUT) un descriptor es la misma que la carga útil para [crear (POST) un descriptor](#create) del mismo tipo.

>[!IMPORTANT]
>
>Al igual que con la creación de descriptores mediante solicitudes de POST, cada tipo de descriptor requiere que se envíen sus propios campos específicos en las cargas útiles de solicitud de PUT. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

En el siguiente ejemplo se actualiza un descriptor de identidad para que haga referencia a un(a) `xdm:sourceProperty` (`mobile phone`) diferente y cambie el(la) `xdm:namespace` a `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Al realizar una [solicitud de búsqueda (GET)](#lookup) para ver el descriptor, se muestra que los campos se han actualizado para reflejar los cambios enviados en la solicitud del PUT.

## Eliminación de un descriptor {#delete}

En ocasiones, es posible que deba quitar un descriptor que haya definido del [!DNL Schema Registry]. Para ello, realice una solicitud de DELETE que haga referencia a `@id` del descriptor que desea eliminar.

**Formato de API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DESCRIPTOR_ID}` | El `@id` del descriptor que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar que el descriptor se ha eliminado, puede realizar una [solicitud de consulta](#lookup) con el descriptor `@id`. La respuesta devuelve el estado HTTP 404 (no encontrado) porque el descriptor se ha eliminado de [!DNL Schema Registry].

## Apéndice

La siguiente sección proporciona información adicional sobre cómo trabajar con descriptores en la API [!DNL Schema Registry].

### Definición de descriptores {#defining-descriptors}

>[!NOTE]
>
>El número máximo de descriptores que se pueden aplicar a un esquema es 4000.

En las secciones siguientes se ofrece una descripción general de los tipos de descriptor disponibles, incluidos los campos obligatorios para definir un descriptor de cada tipo.

>[!IMPORTANT]
>
>No puede etiquetar el objeto de área de nombres de inquilino, ya que el sistema aplicaría esa etiqueta a cada campo personalizado en esa zona protegida. En su lugar, debe especificar el nodo de hoja debajo de ese objeto que debe etiquetar.

#### Descriptor de identidad

Un descriptor de identidad indica que &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; es un campo [!DNL Identity] tal como lo describe [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | El tipo de descriptor que se define. Para un descriptor de identidad, este valor debe establecerse en `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica que será la identidad. La ruta debe comenzar por &quot;/&quot; y no terminar por uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, utilice &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | El valor `id` o `code` del área de nombres de identidad. Se puede encontrar una lista de áreas de nombres usando [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | `xdm:id` o `xdm:code`, según el `xdm:namespace` utilizado. |
| `xdm:isPrimary` | Un valor booleano opcional. Cuando es true, indica el campo como identidad principal. Los esquemas solo pueden contener una identidad principal. |

{style="table-layout:auto"}

#### Descriptor de nombre descriptivo {#friendly-name}

Los descriptores de nombres descriptivos permiten al usuario modificar los valores `title`, `description` y `meta:enum` de los campos de esquema de la biblioteca principal. Especialmente útil cuando se trabaja con eVars y otros campos &quot;genéricos&quot; que desea etiquetar como que contienen información específica de su organización. La interfaz de usuario puede usarlas para mostrar un nombre más descriptivo o solo para mostrar los campos que tienen un nombre descriptivo.

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
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | El tipo de descriptor que se define. Para un descriptor de nombre descriptivo, este valor debe establecerse en `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | La ruta a la propiedad específica cuyos detalles desea modificar. La ruta de acceso debe comenzar con una barra diagonal (`/`) y no terminar con una. No incluya `properties` en la ruta (por ejemplo, use `/personalEmail/address` en lugar de `/properties/personalEmail/properties/address`). |
| `xdm:title` | El nuevo título que desea mostrar para este campo, escrito en Mayúsculas y minúsculas. |
| `xdm:description` | Se puede añadir una descripción opcional junto con el título. |
| `meta:enum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena, `meta:enum` se puede usar para agregar valores sugeridos para el campo en la interfaz de usuario de la segmentación. Es importante tener en cuenta que `meta:enum` no declara una enumeración ni proporciona validación de datos para el campo XDM.<br><br>Esto solo debe usarse para campos XDM principales definidos por el Adobe. Si la propiedad de origen es un campo personalizado definido por su organización, debe editar la propiedad `meta:enum` del campo directamente mediante una solicitud del PATCH al recurso principal del campo. |
| `meta:excludeMetaEnum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena que tiene valores sugeridos existentes proporcionados bajo un campo `meta:enum`, puede incluir este objeto en un descriptor de nombre descriptivo para excluir algunos o todos estos valores de la segmentación. La clave y el valor de cada entrada deben coincidir con los incluidos en el `meta:enum` original del campo para que se excluya la entrada. |

{style="table-layout:auto"}

#### Descriptor de relación

Los descriptores de relación describen una relación entre dos esquemas diferentes, con claves en las propiedades descritas en `sourceProperty` y `destinationProperty`. Vea el tutorial sobre [definición de una relación entre dos esquemas](../tutorials/relationship-api.md) para obtener más información.

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
| `@type` | El tipo de descriptor que se define. Para un descriptor de relación, este valor debe establecerse en `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se define la relación. Debe comenzar por &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` del esquema de referencia con el que define una relación este descriptor. |
| `xdm:destinationVersion` | La versión principal del esquema de referencia. |
| `xdm:destinationProperty` | Ruta opcional a un campo de destino dentro del esquema de referencia. Si se omite esta propiedad, cualquier campo que contenga un descriptor de identidad de referencia coincidente deducirá el campo de destino (consulte a continuación). |

{style="table-layout:auto"}

#### Descriptor de identidad de referencia

Los descriptores de identidad de referencia proporcionan un contexto de referencia a la identidad principal de un campo de esquema, lo que permite que los campos de otros esquemas hagan referencia a él. El esquema de referencia ya debe tener un campo de identidad principal definido antes de que otros esquemas puedan hacer referencia a él a través de este descriptor.

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
| `@type` | El tipo de descriptor que se define. Para un descriptor de identidad de referencia, este valor debe establecerse en `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen que se utilizará para hacer referencia al esquema de referencia. Debe comenzar por &quot;/&quot; y no terminar con uno. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, `/personalEmail/address` en lugar de `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | El código del área de nombres de identidad de la propiedad de origen. |

{style="table-layout:auto"}

#### Descriptor de campo obsoleto

Puede [dejar de utilizar un campo dentro de un recurso XDM personalizado](../tutorials/field-deprecation-api.md#custom) al agregar un atributo `meta:status` establecido en `deprecated` al campo en cuestión. Sin embargo, si desea dejar obsoletos los campos proporcionados por los recursos XDM estándar en los esquemas, puede asignar un descriptor de campo obsoleto al esquema en cuestión para lograr el mismo efecto. Si usa el [encabezado `Accept` correcto](../tutorials/field-deprecation-api.md#verify-deprecation), podrá ver qué campos estándar están obsoletos para un esquema cuando lo busque en la API.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | El tipo de descriptor. Para un descriptor de desaprobación de campo, este valor debe establecerse en `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` del esquema al que está aplicando el descriptor. |
| `xdm:sourceVersion` | La versión del esquema al que está aplicando el descriptor. Debe establecerse en `1`. |
| `xdm:sourceProperty` | Ruta a la propiedad dentro del esquema al que está aplicando el descriptor. Si desea aplicar el descriptor a varias propiedades, puede proporcionar una lista de rutas en forma de matriz (por ejemplo, `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
