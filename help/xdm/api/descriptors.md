---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;descriptor;Descriptor;descriptores;Identity;nombre descriptivo;nombre descriptivo;alternatedisplayinfo;reference;Reference;relation;Relationship
solution: Experience Platform
title: Punto final de API de descriptores
description: El extremo /descriptors de la API de Registro de esquemas le permite administrar mediante programación descriptores XDM dentro de la aplicación de experiencia.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 1%

---

# Extremo de descriptores

Los esquemas definen la estructura de las entidades de datos, pero no especifican cómo se relacionan entre sí los conjuntos de datos creados a partir de estos esquemas. En Adobe Experience Platform, puede utilizar descriptores para describir estas relaciones y agregar metadatos interpretativos a un esquema.

Los descriptores son objetos de metadatos de nivel de inquilino aplicados a esquemas en Adobe Experience Platform. Definen relaciones estructurales, claves y campos de comportamiento (como marcas de tiempo o versiones) que influyen en el modo en que se validan, unen o interpretan los datos en sentido descendente.

Un esquema puede tener uno o más descriptores. Cada descriptor define `@type` y `sourceSchema` a los que se aplica. El descriptor se aplica automáticamente a todos los conjuntos de datos creados a partir de ese esquema.

En Adobe Experience Platform, un descriptor es un metadato que agrega reglas de comportamiento o significado estructural a un esquema.
Existen varios tipos de descriptores, entre ellos:

- [Descriptor de identidad](#identity-descriptor): marca un campo como identidad
- [Descriptor de clave principal](#primary-key-descriptor): exige exclusividad
- [Descriptor de relación](#relationship-descriptor): define una combinación de clave externa
- [Descriptor de información de visualización alternativa](#friendly-name): le permite cambiar el nombre de un campo en la interfaz de usuario
- Descriptores de [Versión](#version-descriptor) y [marca de tiempo](#timestamp-descriptor): rastree el orden de eventos y la detección de cambios

El extremo `/descriptors` de la API [!DNL Schema Registry] le permite administrar descriptores mediante programación dentro de la aplicación de experiencia.

## Introducción

El extremo utilizado en esta guía forma parte de la [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

Además de los descriptores estándar, [!DNL Schema Registry] admite tipos de descriptor para esquemas relacionales, como **clave principal**, **versión** y **marca de tiempo**. Estas aplican exclusividad, controlan las versiones y definen los campos de serie temporal en el nivel de esquema. Si no está familiarizado con los esquemas relacionales, revise la [descripción general de Data Mirror](../data-mirror/overview.md) y la [referencia técnica de esquemas relacionales](../schema/relational.md) antes de continuar.

>[!IMPORTANT]
>
>Consulte el [Apéndice](#defining-descriptors) para obtener detalles sobre todos los tipos de descriptor.

## Recuperación de una lista de descriptores {#list}

Puede enumerar todos los descriptores que ha definido su organización realizando una petición GET a `/tenant/descriptors`.

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

Para ver los detalles de un descriptor específico, envíe una solicitud de GET con su `@id`.

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

Puede crear un nuevo descriptor realizando una petición POST al extremo `/tenant/descriptors`.

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

Puede actualizar un descriptor incluyendo su `@id` en la ruta de una petición PUT.

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
>Al igual que con la creación de descriptores mediante solicitudes POST, cada tipo de descriptor requiere que se envíen sus propios campos específicos en las cargas útiles de solicitud de PUT. Consulte el [apéndice](#defining-descriptors) para obtener una lista completa de los descriptores y los campos necesarios para definirlos.

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

Al realizar una [solicitud de búsqueda (GET)](#lookup) para ver el descriptor, se muestra que los campos se han actualizado para reflejar los cambios enviados en la solicitud de PUT.

## Eliminación de un descriptor {#delete}

En ocasiones, es posible que deba quitar un descriptor que haya definido del [!DNL Schema Registry]. Para ello, realice una petición DELETE que haga referencia a `@id` del descriptor que desea eliminar.

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

## Apéndice {#appendix}

La siguiente sección proporciona información adicional sobre cómo trabajar con descriptores en la API [!DNL Schema Registry].

### Definición de descriptores {#defining-descriptors}

>[!NOTE]
>
>El número máximo de descriptores que se pueden aplicar a la zona protegida de una organización es 4000.

En las secciones siguientes se ofrece una descripción general de los tipos de descriptor disponibles, incluidos los campos obligatorios para definir un descriptor de cada tipo.

>[!IMPORTANT]
>
>No puede etiquetar el objeto de área de nombres de inquilino, ya que el sistema aplicaría esa etiqueta a cada campo personalizado en esa zona protegida. En su lugar, debe especificar el nodo de hoja debajo de ese objeto que debe etiquetar.

#### Descriptor de identidad {#identity-descriptor}

Un descriptor de identidad indica que el &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; es un campo [!DNL Identity] tal como lo describe [Experience Platform Identity Service](../../identity-service/home.md).

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
| `meta:enum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena, `meta:enum` se puede usar para agregar valores sugeridos para el campo en la interfaz de usuario de la segmentación. Es importante tener en cuenta que `meta:enum` no declara una enumeración ni proporciona validación de datos para el campo XDM.<br><br>Esto solo debe usarse para los campos XDM principales definidos por Adobe. Si la propiedad de origen es un campo personalizado definido por su organización, debe editar la propiedad `meta:enum` del campo directamente a través de una petición PATCH al recurso principal del campo. |
| `meta:excludeMetaEnum` | Si el campo indicado por `xdm:sourceProperty` es un campo de cadena que tiene valores sugeridos existentes proporcionados bajo un campo `meta:enum`, puede incluir este objeto en un descriptor de nombre descriptivo para excluir algunos o todos estos valores de la segmentación. La clave y el valor de cada entrada deben coincidir con los incluidos en el `meta:enum` original del campo para que se excluya la entrada. |

{style="table-layout:auto"}

#### Descriptor de relación {#relationship-descriptor}

Los descriptores de relación describen una relación entre dos esquemas diferentes, con claves en las propiedades descritas en `xdm:sourceProperty` y `xdm:destinationProperty`. Vea el tutorial sobre [definición de una relación entre dos esquemas](../tutorials/relationship-api.md) para obtener más información.

Utilice estas propiedades para declarar cómo se relaciona un campo de origen (clave externa) con un campo de destino ([clave principal](#primary-key-descriptor) o clave candidata).

>[!TIP]
>
>Una **clave externa** es un campo en el esquema de origen (definido por `xdm:sourceProperty`) que hace referencia a un campo de clave en otro esquema. Una **clave candidata** es cualquier campo (o conjunto de campos) del esquema de destino que identifica de forma exclusiva un registro y se puede utilizar en lugar de la clave principal.

La API admite dos patrones:

- `xdm:descriptorOneToOne`: relación estándar 1:1.
- `xdm:descriptorRelationship`: patrón general para nuevos esquemas relacionales y de trabajo (admite destinos de clave no principal, nomenclatura y cardinalidad).

##### Relación uno a uno (esquemas estándar)

Utilice esto cuando mantenga integraciones de esquema estándar existentes que ya dependen de `xdm:descriptorOneToOne`.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

En la tabla siguiente se describen los campos necesarios para definir un descriptor de relación uno a uno.

| Propiedad | Descripción |
| --- | --- |
| `@type` | El tipo de descriptor que se define. Para un descriptor de relación, este valor debe establecerse en `xdm:descriptorOneToOne`, a menos que tenga acceso a Real-Time CDP B2B edition. Con B2B edition tiene la opción de usar `xdm:descriptorOneToOne` o [`xdm:descriptorRelationship`](#b2b-relationship-descriptor). |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se define la relación. Debe comenzar por &quot;/&quot; y no terminar por &quot;/&quot;. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` del esquema de referencia con el que define una relación este descriptor. |
| `xdm:destinationVersion` | La versión principal del esquema de referencia. |
| `xdm:destinationProperty` | (Opcional) Ruta a un campo de destino dentro del esquema de referencia. Si se omite esta propiedad, cualquier campo que contenga un descriptor de identidad de referencia coincidente deducirá el campo de destino (consulte a continuación). |

##### Relación general (esquemas relacionales y recomendados para nuevos proyectos)

Utilice este descriptor para todas las implementaciones nuevas y para los esquemas relacionales. Permite definir la cardinalidad de la relación (por ejemplo, uno a uno o varios a uno), especificar nombres de relación y vincular a un campo de destino que no sea la clave principal (clave no principal).

Los siguientes ejemplos muestran cómo definir un descriptor de relación general.

**Ejemplo mínimo:**

Este ejemplo mínimo incluye solo los campos requeridos para definir una relación de varios a uno entre dos esquemas.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**Ejemplo con todos los campos opcionales:**

Este ejemplo incluye todos los campos opcionales, como nombres de relación, títulos para mostrar y un campo de destino de clave no principal explícito.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### Selección de un descriptor de relación

Siga estas directrices para decidir qué descriptor de relación aplicar:

| Situación | Descriptor que utilizar |
| --------------------------------------------------------------------- | ----------------------------------------- |
| Nuevos esquemas de trabajo o relacionales | `xdm:descriptorRelationship` |
| Asignación de 1:1 existente en esquemas estándar | Continúe usando `xdm:descriptorOneToOne` a menos que necesite características compatibles únicamente con `xdm:descriptorRelationship`. |
| Necesita cardinalidad de varios a uno u opcional (`1:1`, `1:0`, `M:1`, `M:0`) | `xdm:descriptorRelationship` |
| Se necesitan nombres o títulos de relación para la legibilidad de la interfaz de usuario/flujo descendente | `xdm:descriptorRelationship` |
| Se necesita un destino que no sea una identidad | `xdm:descriptorRelationship` |

>[!NOTE]
>
>Para los descriptores de `xdm:descriptorOneToOne` existentes en los esquemas estándar, continúe usándolos a menos que necesite características como destinos de identidad no principales, nombres personalizados u opciones de cardinalidad expandida.

##### Comparación de capacidades

La siguiente tabla compara las capacidades de los dos tipos de descriptor:

| Capacidad | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| Cardinalidad | 1:1 | 1:1, 1:0, M:1, M:0 (informativo) |
| Destino objetivo | Campo de identidad/explícito | Clave principal de forma predeterminada o clave no principal mediante `xdm:destinationProperty` |
| Campos de nomenclatura | No compatible | `xdm:sourceToDestinationName`, `xdm:destinationToSourceName` y títulos |
| Ajuste relacional | Limitado | Patrón principal para esquemas relacionales |

##### Restricciones y validación

Siga estos requisitos y recomendaciones al definir un descriptor de relación general:

- Para los esquemas relacionales, coloque el campo de origen (clave externa) en el nivel raíz. Se trata de una limitación técnica actual para la ingesta, no solo una recomendación de prácticas recomendadas.
- Asegúrese de que los tipos de datos de los campos de origen y destino sean compatibles (numérico, de fecha, booleano, de cadena).
- Recuerde que la cardinalidad es informativa; el almacenamiento no la aplica. Especifique la cardinalidad en formato `<source>:<destination>`. Los valores aceptados son: `1:1`, `1:0`, `M:1` o `M:0`.

#### Descriptor de clave principal {#primary-key-descriptor}

El descriptor de clave principal (`xdm:descriptorPrimaryKey`) aplica restricciones de unicidad y no nulas en uno o varios campos de un esquema.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| Propiedad | Descripción |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | Debe ser `xdm:descriptorPrimaryKey`. |
| `xdm:sourceSchema` | URI `$id` del esquema. |
| `xdm:sourceProperty` | Punteros JSON a los campos de clave principal. Utilice una matriz para claves compuestas. Para los esquemas de series temporales, la clave compuesta debe incluir el campo de marca de tiempo para garantizar la exclusividad en los registros de eventos. |

#### Descriptor de versión {#version-descriptor}

>[!NOTE]
>
>En el Editor de esquemas de interfaz de usuario, el descriptor de versión aparece como &quot;[!UICONTROL Version identifier]&quot;.

El descriptor de versión (`xdm:descriptorVersion`) designa un campo para detectar y evitar conflictos por eventos de cambio desordenados.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| Propiedad | Descripción |
| -------------------- | ------------------------------------------------------------- |
| `@type` | Debe ser `xdm:descriptorVersion`. |
| `xdm:sourceSchema` | URI `$id` del esquema. |
| `xdm:sourceProperty` | Puntero JSON al campo de versión. Debe estar marcado `required`. |

#### Descriptor de marca de tiempo {#timestamp-descriptor}

>[!NOTE]
>
>En el Editor de esquemas de interfaz de usuario, el descriptor de marca de tiempo aparece como &quot;[!UICONTROL Timestamp identifier]&quot;.

El descriptor de marca de tiempo (`xdm:descriptorTimestamp`) designa un campo de fecha y hora como marca de tiempo para esquemas con `"meta:behaviorType": "time-series"`.

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| Propiedad | Descripción |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | Debe ser `xdm:descriptorTimestamp`. |
| `xdm:sourceSchema` | URI `$id` del esquema. |
| `xdm:sourceProperty` | Puntero JSON al campo de marca de tiempo. Debe estar marcado `required` y ser del tipo `date-time`. |

##### Descriptor de relación B2B {#B2B-relationship-descriptor}

Real-Time CDP B2B edition presenta una forma alternativa de definir relaciones entre esquemas, lo que permite relaciones varios a uno. Esta nueva relación debe tener el tipo `@type: xdm:descriptorRelationship` y la carga debe incluir más campos que la relación `@type: xdm:descriptorOneToOne`. Vea el tutorial sobre [definición de una relación de esquema para B2B edition](../tutorials/relationship-b2b.md) para obtener más información.

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Propiedad | Descripción |
| --- | --- |
| `@type` | El tipo de descriptor que se define. Para usar los campos siguientes, el valor debe establecerse en `xdm:descriptorRelationship`. Para obtener información sobre tipos adicionales, consulte la sección [descriptores de relación](#relationship-descriptor). |
| `xdm:sourceSchema` | URI `$id` del esquema donde se define el descriptor. |
| `xdm:sourceVersion` | La versión principal del esquema de origen. |
| `xdm:sourceProperty` | Ruta al campo en el esquema de origen donde se define la relación. Debe comenzar por &quot;/&quot; y no terminar por &quot;/&quot;. No incluya &quot;propiedades&quot; en la ruta (por ejemplo, &quot;/personalEmail/address&quot; en lugar de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` del esquema de referencia con el que define una relación este descriptor. |
| `xdm:destinationVersion` | La versión principal del esquema de referencia. |
| `xdm:destinationProperty` | (Opcional) Ruta a un campo de destino dentro del esquema de referencia. Esto debe resolverse en el ID principal del esquema o en otro campo con un tipo de datos compatible de `xdm:sourceProperty`. Si se omite, es posible que la relación no funcione según lo esperado. |
| `xdm:destinationNamespace` | El área de nombres del ID principal del esquema de referencia. |
| `xdm:destinationToSourceTitle` | El nombre para mostrar de la relación del esquema de referencia al esquema de origen. |
| `xdm:sourceToDestinationTitle` | El nombre para mostrar de la relación del esquema de origen al esquema de referencia. |
| `xdm:cardinality` | La relación de unión entre los esquemas. Este valor debe establecerse en `M:1`, en referencia a una relación de varios a uno. |

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
