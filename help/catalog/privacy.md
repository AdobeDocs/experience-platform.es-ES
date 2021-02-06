---
keywords: Experience Platform;hogar;temas populares;privacidad del lago de datos;Áreas de nombres de identidad;privacidad;lago de datos
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en el lago de datos
topic: overview
description: Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales según lo establecido en las normas legales y de privacidad de la organización. Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para datos de clientes almacenados en Data Lake.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# Procesamiento de solicitud de privacidad en [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] procesa las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales según lo establecido en las regulaciones legales y de privacidad de la organización.

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para datos de clientes almacenados en [!DNL Data Lake].

## Primeros pasos

Antes de leer esta guía, se recomienda que conozca los siguientes servicios [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../privacy-service/home.md):: Gestiona las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales en todas las aplicaciones de Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md):: Sistema de registro para la ubicación y linaje de datos dentro de  [!DNL Experience Platform]. Proporciona una API que se puede utilizar para actualizar los metadatos del conjunto de datos.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
* [[!DNL Identity Service]](../identity-service/home.md):: Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.

## Explicación de las Áreas de nombres de identidad {#namespaces}

Adobe Experience Platform [!DNL Identity Service] une datos de identidad del cliente entre sistemas y dispositivos. [!DNL Identity Service] utiliza Áreas de nombres de identidad para proporcionar contexto a los valores de identidad relacionándolos con su sistema de origen. Una Área de nombres puede representar un concepto genérico, como una dirección de correo electrónico (&quot;Correo electrónico&quot;) o asociar la identidad con una aplicación específica, como un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] mantiene un almacén de Áreas de nombres de identidad definidas globalmente (estándar) y definidas por el usuario (personalizadas). Las Áreas de nombres estándar están disponibles para todas las organizaciones (por ejemplo, &quot;Correo electrónico&quot; y &quot;ECID&quot;), mientras que la organización también puede crear Áreas de nombres personalizadas para satisfacer sus necesidades específicas.

Para obtener más información acerca de las Áreas de nombres de identidad en [!DNL Experience Platform], consulte la [información general de la Área de nombres de identidad](../identity-service/namespaces.md).

## Añadir datos de identidad a conjuntos de datos

Al crear solicitudes de privacidad para [!DNL Data Lake], se deben proporcionar valores de identidad válidos (y sus Áreas de nombres asociadas) para cada cliente individual a fin de ubicar sus datos y procesarlos en consecuencia. Por lo tanto, todos los conjuntos de datos que están sujetos a solicitudes de privacidad deben contener un descriptor de identidad en su esquema XDM asociado.

>[!NOTE]
>
>Los conjuntos de datos basados en esquemas que no admiten metadatos del descriptor de identidad (como conjuntos de datos ad-hoc) actualmente no se pueden procesar en solicitudes de privacidad.

En esta sección se explican los pasos para agregar un descriptor de identidad al esquema XDM de un conjunto de datos existente. Si ya tiene un conjunto de datos con un descriptor de identidad, puede pasar a la [siguiente sección](#nested-maps).

>[!IMPORTANT]
>
>Al decidir qué campos de esquema se configurarán como identidades, tenga en cuenta las [limitaciones de uso de campos anidados de tipo de mapa](#nested-maps).

Existen dos métodos para agregar un descriptor de identidad a un esquema de conjunto de datos:

* [Uso de la interfaz de usuario](#identity-ui)
* [Uso de la API](#identity-api)

### Uso de la IU {#identity-ui}

En la interfaz de usuario [!DNL Experience Platform ], el espacio de trabajo **[!UICONTROL Esquemas]** permite editar los esquemas XDM existentes. Para agregar un descriptor de identidad a un esquema, seleccione el esquema en la lista y siga los pasos para [configurar un campo de esquema como un campo de identidad](../xdm/tutorials/create-schema-ui.md#identity-field) en el tutorial [!DNL Schema Editor].

Una vez configurados los campos correspondientes dentro del esquema como campos de identidad, puede pasar a la siguiente sección sobre [envío de solicitudes de privacidad](#submit).

### Uso de la API {#identity-api}

>[!NOTE]
>
>En esta sección se asume que conoce el valor de ID de URI único del esquema XDM del conjunto de datos. Si no conoce este valor, puede recuperarlo mediante la API [!DNL Catalog Service]. Después de leer la sección [introducción](./api/getting-started.md) de la guía para desarrolladores, siga los pasos descritos en para [listar](./api/list-objects.md) o [buscar](./api/look-up-object.md) [!DNL Catalog] objetos para encontrar el conjunto de datos. El ID de esquema se encuentra en `schemaRef.id`
>
> Esta sección incluye llamadas a la API del Registro de Esquema. Para obtener información importante relacionada con el uso de la API, incluso conocer su `{TENANT_ID}` y el concepto de contenedores, consulte la sección [introducción](../xdm/api/getting-started.md) de la guía para desarrolladores.

Puede agregar un descriptor de identidad al esquema XDM de un conjunto de datos haciendo una solicitud de POST al extremo `/descriptors` en la API [!DNL Schema Registry].

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
| `xdm:namespace` | Una de las [Áreas de nombres de identidad estándar](../privacy-service/api/appendix.md#standard-namespaces) reconocidas por [!DNL Privacy Service] o una Área de nombres personalizada definida por su organización. |
| `xdm:property` | &quot;xdm:id&quot; o &quot;xdm:code&quot;, según la Área de nombres que se esté utilizando en `xdm:namespace`. |
| `xdm:isPrimary` | Un valor booleano opcional. Cuando es true, indica que el campo es una identidad principal. Los esquemas solo pueden contener una identidad primaria. El valor predeterminado es false si no se incluye. |

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

>[!NOTE]
>
>Esta sección trata cómo dar formato a las solicitudes de privacidad para [!DNL Data Lake]. Se recomienda encarecidamente que revise la documentación de [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) o [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) para conocer los pasos completos sobre cómo enviar un trabajo de privacidad, incluida la forma de dar un formato adecuado a los datos de identidad del usuario enviados en las cargas de la solicitud.

La siguiente sección describe cómo realizar solicitudes de privacidad para [!DNL Data Lake] mediante la interfaz de usuario o API [!DNL Privacy Service].

>[!IMPORTANT]
>
>No se puede garantizar la cantidad de tiempo que una solicitud de privacidad puede tardar en completarse. Si se producen cambios dentro del lago de datos mientras se sigue procesando una solicitud, no se puede garantizar si esos registros se procesan o no.

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **[!UICONTROL AEP Data Lake]** y/o **[!UICONTROL Perfil]** en **[!UICONTROL Products]** para procesar trabajos para datos almacenados en [!DNL Data Lake] o [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

### Uso de la API

Al crear solicitudes de trabajo en la API, cualquier `userIDs` que se proporcione debe utilizar un `namespace` y `type` específicos en función del almacén de datos al que se apliquen. Los ID de [!DNL Data Lake] deben utilizar &quot;no registrados&quot; para su valor `type` y un valor `namespace` que coincida con uno de los [rótulos de privacidad](#privacy-labels) que se han agregado a los conjuntos de datos aplicables.

Además, la matriz `include` de la carga útil de la solicitud debe incluir los valores del producto para los diferentes almacenes de datos en los que se realiza la solicitud. Al realizar solicitudes a [!DNL Data Lake], la matriz debe incluir el valor `aepDataLake`.

La siguiente solicitud crea un nuevo trabajo de privacidad para [!DNL Data Lake], mediante la Área de nombres &quot;email_label&quot; no registrada. También incluye el valor del producto para la [!DNL Data Lake] en la matriz `include`:

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

Cuando [!DNL Experience Platform] recibe una solicitud de eliminación de [!DNL Privacy Service], [!DNL Platform] envía una confirmación a [!DNL Privacy Service] de que la solicitud se ha recibido y los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del [!DNL Data Lake] en un plazo de siete días. Durante ese período de siete días, los datos se eliminan de forma suave y, por lo tanto, ningún servicio [!DNL Platform] puede acceder a ellos.

En futuras versiones, [!DNL Platform] enviará confirmación a [!DNL Privacy Service] después de que se hayan eliminado físicamente los datos.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de solicitudes de privacidad para [!DNL Data Lake]. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Consulte el documento sobre el [procesamiento de solicitudes de privacidad para el Perfil del cliente en tiempo real](../profile/privacy.md) para ver los pasos sobre el procesamiento de solicitudes de privacidad para el almacén [!DNL Profile].

## Apéndice

La siguiente sección contiene información adicional para procesar solicitudes de privacidad en [!DNL Data Lake].

### Etiquetado de campos anidados de tipo de mapa {#nested-maps}

Es importante tener en cuenta que hay dos tipos de campos anidados de tipo mapa que no admiten el etiquetado de privacidad:

* Campo de tipo mapa dentro de un campo de tipo matriz
* Campo de tipo mapa dentro de otro campo de tipo mapa

El procesamiento del trabajo de privacidad de cualquiera de los dos ejemplos anteriores fallará eventualmente. Por este motivo, se recomienda evitar el uso de campos anidados de tipo mapa para almacenar datos privados de clientes. Los ID de consumidor relevantes deben almacenarse como un tipo de datos que no sea de mapa dentro del campo `identityMap` (campo de tipo mapa en sí mismo) para conjuntos de datos basados en registros o el campo `endUserID` para conjuntos de datos basados en series temporales.