---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Procesamiento de solicitudes de privacidad en Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Procesamiento de solicitudes de privacidad en Data Lake

Adobe Experience Platform Privacy Service procesa las solicitudes de los clientes para acceder, exclusión de venta o eliminar sus datos personales, según lo establecido en las normas de privacidad, como la Regulación General de Protección de Datos (RGPD) y la Ley de Protección de los Consumidores de California (CCPA).

Este documento cubre conceptos esenciales relacionados con el procesamiento de solicitudes de privacidad para datos de clientes almacenados en Data Lake.

## Primeros pasos

Se recomienda que conozca bien los siguientes servicios de la plataforma de experiencias antes de leer esta guía:

* [Privacy Service](../privacy-service/home.md): Gestiona las solicitudes de los clientes para acceder, exclusión la venta o eliminar sus datos personales en las aplicaciones de Adobe Experience Cloud.
* [Servicio](home.md)de catálogo: Sistema de registro para la ubicación y el linaje de datos dentro de la plataforma de experiencias. Proporciona una API que se puede utilizar para actualizar los metadatos del conjunto de datos.
* [Sistema](../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.

## Añadir etiquetas de privacidad a conjuntos de datos {#privacy-labels}

Para que un conjunto de datos se procese en una solicitud de privacidad para el Data Lake, el conjunto de datos debe recibir etiquetas de privacidad. Las etiquetas de privacidad indican los campos dentro del esquema asociado de un conjunto de datos que se aplican a las Áreas de nombres que espera que se envíen en las solicitudes de privacidad.

Esta sección muestra cómo agregar etiquetas de privacidad a un conjunto de datos para utilizarlas en solicitudes de privacidad de Data Lake. Para empezar, considere el siguiente conjunto de datos:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

La `schemaMetadata` propiedad del conjunto de datos contiene una `gdpr` matriz, que actualmente está vacía. Para agregar etiquetas de privacidad al conjunto de datos, esta matriz debe actualizarse mediante una solicitud PATCH a la API [del servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catálogo.

>[!NOTE] Aunque se nombra la matriz `gdpr`, la adición de etiquetas permitirá solicitudes de trabajos de privacidad para las regulaciones GDPR y CCPA.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El `id` valor del conjunto de datos que se va a actualizar. |

**Solicitud**

En este ejemplo, un conjunto de datos incluye una dirección de correo electrónico en el `personalEmail.address` campo. Para que este campo funcione como identificador para las solicitudes de privacidad de Data Lake, se debe agregar a su `gdpr` matriz una etiqueta que utilice una Área de nombres no registrada.

La siguiente solicitud agrega una etiqueta de privacidad que asigna la Área de nombres &quot;email_label&quot; al `personalEmail.address` campo.

>[!IMPORTANT] Al ejecutar una operación PATCH en la propiedad `schemaMetadata` de un conjunto de datos, asegúrese de copiar las subpropiedades existentes dentro de la carga útil de la solicitud. Si se excluyen los valores existentes de la carga útil, se eliminarán del conjunto de datos.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `namespace` | Una matriz que enumera las Áreas de nombres que se asociarán al campo especificado en `path`. Las Áreas de nombres se utilizan para identificar los campos relacionados con la privacidad al [enviar solicitudes](#submit) de acceso o eliminación en la API de Privacy Service. |
| `path` | La ruta al campo dentro del esquema asociado del conjunto de datos que se aplica al `namespace`. Lo ideal sería que las etiquetas de privacidad solo se apliquen a los campos &quot;hoja&quot; (campos sin subcampos). |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Aceptar) con el ID del conjunto de datos proporcionado en la carga útil. El uso del ID para buscar de nuevo el conjunto de datos revela que se han agregado las etiquetas de privacidad.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Etiquetado de campos anidados de tipo de mapa

Es importante tener en cuenta que hay dos tipos de campos anidados de tipo mapa que no admiten el etiquetado de privacidad:

* Campo de tipo mapa dentro de un campo de tipo matriz
* Campo de tipo mapa dentro de otro campo de tipo mapa

El procesamiento del trabajo de privacidad de cualquiera de los dos ejemplos anteriores fallará eventualmente. Por este motivo, se recomienda evitar el uso de campos anidados de tipo mapa para almacenar datos privados de clientes. Los ID de consumidor relevantes deben almacenarse como un tipo de datos que no sea de mapa dentro del `identityMap` campo (campo de tipo mapa en sí mismo) para conjuntos de datos basados en registros o el `endUserID` campo para conjuntos de datos basados en series temporales.

## Envío de solicitudes {#submit}

>[!NOTE] En esta sección se explica cómo dar formato a las solicitudes de privacidad del lago de datos. Se recomienda encarecidamente que revise la documentación de la API [de](../privacy-service/api/getting-started.md) Privacy Service o de la interfaz de usuario [de](../privacy-service/ui/overview.md) Privacy Service para ver los pasos completos sobre cómo enviar un trabajo de privacidad, incluida la forma correcta de dar formato a los datos de identidad de usuario enviados en las cargas de solicitud.

La siguiente sección describe cómo realizar solicitudes de privacidad para el lago de datos mediante la API o la interfaz de usuario de Privacy Service.

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

### Uso de la interfaz de usuario

Al crear solicitudes de trabajo en la interfaz de usuario, asegúrese de seleccionar **AEP Data Lake** y/o **Perfil** en _Productos_ para procesar los trabajos de datos almacenados en Data Lake o en Real-time Customer Perfil, respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Eliminar procesamiento de solicitud

Cuando la plataforma de experiencia recibe una solicitud de eliminación de Privacy Service, la plataforma envía una confirmación a Privacy Service de que la solicitud se ha recibido y los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del lago de datos en un plazo de siete días. Durante ese período de siete días, los datos se eliminan de forma suave y, por lo tanto, ningún servicio de plataforma puede acceder a ellos.

En futuras versiones, Platform enviará una confirmación a Privacy Service después de que se hayan eliminado físicamente los datos.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos importantes relacionados con el procesamiento de las solicitudes de privacidad del Data Lake. Se recomienda seguir leyendo la documentación proporcionada en esta guía para comprender mejor cómo administrar los datos de identidad y crear trabajos de privacidad.

Consulte el documento sobre el procesamiento de solicitudes de [privacidad para el Perfil](../profile/privacy.md) de clientes en tiempo real para ver los pasos sobre el procesamiento de solicitudes de privacidad para el almacén de Perfiles.