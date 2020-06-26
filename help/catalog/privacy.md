---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 327be13cbaaa40e4d0409cbb49a051b7067759bf
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# Procesamiento de solicitudes de privacidad en Data Lake

Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales según lo establecido en las normas legales y de privacidad de la organización.

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para datos de clientes almacenados en Data Lake.

## Primeros pasos

Se recomienda que conozca bien los siguientes servicios de Experience Platform antes de leer esta guía:

* [Privacy Service](../privacy-service/home.md): Gestiona las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [Servicio](home.md)de catálogo: Sistema de registro para la ubicación y linaje de datos dentro del Experience Platform. Proporciona una API que se puede utilizar para actualizar los metadatos del conjunto de datos.
* [Sistema](../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Servicio](../identity-service/home.md)de identidad: Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.

## Explicación de las Áreas de nombres de identidad {#namespaces}

Adobe Experience Platform Identity Service une los datos de identidad del cliente entre sistemas y dispositivos. Identity Service utiliza Áreas de nombres **de** identidad para proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un ID de Advertising Cloud de Adobe (&quot;AdCloud&quot;) o un ID de Adobe Target (&quot;TNTID&quot;).

Identity Service mantiene un almacén de Áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las Áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;Correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear Áreas de nombres personalizadas para satisfacer sus necesidades específicas.

Para obtener más información sobre Áreas de nombres de identidad en Experience Platform, consulte la descripción general [de la Área de nombres de](../identity-service/namespaces.md)identidad.

## Añadir datos de identidad a conjuntos de datos

Al crear solicitudes de privacidad para el Data Lake, se deben proporcionar valores de identidad válidos (y sus Áreas de nombres asociadas) para cada cliente individual a fin de localizar sus datos y procesarlos en consecuencia. Por lo tanto, todos los conjuntos de datos que están sujetos a solicitudes de privacidad deben contener un descriptor **de** identidad en su esquema XDM asociado.

>[!NOTE] Los conjuntos de datos basados en esquemas que no admiten metadatos del descriptor de identidad (como conjuntos de datos ad-hoc) actualmente no se pueden procesar en solicitudes de privacidad.

En esta sección se explican los pasos para agregar un descriptor de identidad al esquema XDM de un conjunto de datos existente. Si ya tiene un conjunto de datos con un descriptor de identidad, puede pasar a la [siguiente sección](#nested-maps).

>[!IMPORTANT]
>
>Cuando decida qué campos de esquema se definirán como identidades, tenga en cuenta las [limitaciones del uso de campos](#nested-maps)anidados de tipo de mapa.

Existen dos métodos para agregar un descriptor de identidad a un esquema de conjunto de datos:

* [Uso de la interfaz de usuario](#identity-ui)
* [Uso de la API](#identity-api)

### Uso de la interfaz de usuario {#identity-ui}

En la interfaz de usuario de Experience Platform, el espacio de trabajo _[!UICONTROL Esquemas]_permite editar los esquemas XDM existentes. Para agregar un descriptor de identidad a un esquema, seleccione el esquema en la lista y siga los pasos para[configurar un campo de esquema como campo](../xdm/tutorials/create-schema-ui.md#identity-field)de identidad en el tutorial Editor de Esquemas.

Una vez configurados los campos correspondientes dentro del esquema como campos de identidad, puede pasar a la siguiente sección sobre el [envío de solicitudes](#submit)de privacidad.

### Uso de la API {#identity-api}

>[!NOTE] En esta sección se asume que conoce el valor de ID de URI único del esquema XDM del conjunto de datos. Si no conoce este valor, puede recuperarlo mediante la API del servicio de catálogo. Después de leer la sección de [introducción](./api/getting-started.md) de la guía para desarrolladores, siga los pasos descritos en para [enumerar](./api/list-objects.md) o [buscar](./api/look-up-object.md) los objetos del catálogo para encontrar el conjunto de datos. El ID de esquema se encuentra en `schemaRef.id`
>
> Esta sección incluye llamadas a la API del Registro de Esquema. Para obtener información importante relacionada con el uso de la API, incluido el conocimiento del usuario `{TENANT_ID}` y el concepto de contenedores, consulte la sección de [introducción](../xdm/api/getting-started.md) de la guía para desarrolladores.

Puede agregar un descriptor de identidad al esquema XDM de un conjunto de datos haciendo una solicitud POST al extremo del `/descriptors` en la API del Registro de Esquema.

**Formato API**

```http
POST /descriptors
```

**Solicitud**

La siguiente solicitud define un descriptor de identidad en un campo &quot;dirección de correo electrónico&quot; de un esquema de ejemplo.

```shell
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

| Propiedad | Descripción |
| --- | --- |
| `@type` | Tipo de descriptor que se está creando. Para los descriptores de identidad, el valor debe ser &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | El identificador URI exclusivo del esquema XDM del conjunto de datos. |
| `xdm:sourceVersion` | Versión del esquema XDM especificado en `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Ruta al campo de esquema al que se está aplicando el descriptor. |
| `xdm:namespace` | Una de las Áreas de nombres [de identidad](../privacy-service/api/appendix.md#standard-namespaces) estándar reconocidas por el Privacy Service o una Área de nombres personalizada definida por la organización. |
| `xdm:property` | &quot;xdm:id&quot; o &quot;xdm:code&quot;, en función de la Área de nombres que se utilice en `xdm:namespace`. |
| `xdm:isPrimary` | Un valor booleano opcional. Cuando es true, indica que el campo es una identidad principal. Los Esquemas solo pueden contener una identidad primaria. El valor predeterminado es false si no se incluye. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y los detalles del descriptor recién creado.

```json
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

## Envío de solicitudes {#submit}

>[!NOTE] En esta sección se explica cómo dar formato a las solicitudes de privacidad del lago de datos. Se recomienda encarecidamente que revise la documentación de la interfaz de usuario [del](../privacy-service/ui/overview.md) Privacy Service o de la API [del](../privacy-service/api/getting-started.md) Privacy Service para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluida la forma correcta de dar formato a los datos de identidad del usuario enviados en las cargas de solicitud.

La siguiente sección describe cómo realizar solicitudes de privacidad para el lago de datos mediante la interfaz de usuario o API del Privacy Service.

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **AEP Data Lake** y/o **Perfil** en _Productos_ para procesar los trabajos de datos almacenados en Data Lake o en Real-time Customer Perfil, respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier `userIDs` que se proporcione debe utilizar un valor específico `namespace` y `type` dependiendo del almacén de datos al que se apliquen. Los ID del lago de datos deben utilizar &quot;no registrados&quot; para su `type` valor y un `namespace` valor que coincida con una de las etiquetas [de](#privacy-labels) privacidad que se han agregado a los conjuntos de datos aplicables.

Además, la `include` matriz de la carga útil de la solicitud debe incluir los valores del producto para los diferentes almacenes de datos a los que se realiza la solicitud. Al realizar solicitudes al lago de datos, la matriz debe incluir el valor &quot;aepDataLake&quot;.

La siguiente solicitud crea un nuevo trabajo de privacidad para Data Lake, mediante la Área de nombres &quot;email_label&quot; no registrada. También incluye el valor de producto para el lago de datos en la `include` matriz:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Eliminar procesamiento de solicitud

Cuando el Experience Platform recibe una solicitud de eliminación del Privacy Service, Platform envía una confirmación al Privacy Service de que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del lago de datos en un plazo de siete días. Durante ese período de siete días, los datos se eliminan de forma suave y, por lo tanto, ningún servicio de Platform puede acceder a ellos.

En futuras versiones, Platform enviará una confirmación al Privacy Service después de que se hayan eliminado físicamente los datos.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de las solicitudes de privacidad del Data Lake. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Consulte el documento sobre el procesamiento de solicitudes de [privacidad para el Perfil](../profile/privacy.md) de clientes en tiempo real para ver los pasos sobre el procesamiento de solicitudes de privacidad para el almacén de Perfiles.

## Apéndice

La siguiente sección contiene información adicional para procesar solicitudes de privacidad en el lago de datos.

### Etiquetado de campos anidados de tipo de mapa {#nested-maps}

Es importante tener en cuenta que hay dos tipos de campos anidados de tipo mapa que no admiten el etiquetado de privacidad:

* Campo de tipo mapa dentro de un campo de tipo matriz
* Campo de tipo mapa dentro de otro campo de tipo mapa

El procesamiento del trabajo de privacidad de cualquiera de los dos ejemplos anteriores fallará eventualmente. Por este motivo, se recomienda evitar el uso de campos anidados de tipo mapa para almacenar datos privados de clientes. Los ID de consumidor relevantes deben almacenarse como un tipo de datos que no sea de mapa dentro del `identityMap` campo (campo de tipo mapa en sí mismo) para conjuntos de datos basados en registros o el `endUserID` campo para conjuntos de datos basados en series temporales.