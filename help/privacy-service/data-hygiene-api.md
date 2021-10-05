---
title: API de higiene de datos (Alpha)
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: dfe9c1ef826bc769a82938223029cd41c066c221
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---

# API de higiene de datos (Alpha)

>[!IMPORTANT]
>
>La API de higiene de datos se encuentra actualmente en alfa y es posible que su organización no tenga acceso a ella todavía. La funcionalidad descrita en este documento está sujeta a cambios.

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform. A diferencia de la API de Privacy Service, estas operaciones no necesitan estar asociadas con regulaciones legales de privacidad y pueden utilizarse exclusivamente para mantener los datos limpios y precisos.

## Primeros pasos

Esta sección proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de higiene de datos.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a la API de higiene de datos, primero debe recopilar sus credenciales de autenticación. Estas son las mismas credenciales que se usan para acceder a la API de Privacy Service. Siga la [guía de introducción](./api/getting-started.md) de la API del Privacy Service para generar valores para cada uno de los encabezados necesarios para la API de higiene de datos, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

### Leer llamadas de API de ejemplo

Este documento proporciona una llamada API de ejemplo para demostrar cómo dar formato a las solicitudes. Para obtener información sobre las convenciones utilizadas en la documentación para ver ejemplos de llamadas de API, consulte la sección sobre [cómo leer ejemplos de llamadas de API](../landing/api-guide.md#sample-api) en la guía de introducción para las API de Experience Platform.

## Crear un trabajo de eliminación

Puede crear un trabajo de eliminación realizando una solicitud de POST.

**Formato de API**

```http
POST /jobs
```

**Solicitud**

La carga útil de la solicitud está estructurada de forma similar a la de una solicitud de [eliminación en la API del Privacy Service](./api/privacy-jobs.md#access-delete). Incluye una matriz `users` cuyos objetos representan a los usuarios cuyos datos se van a eliminar.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `companyContexts` | Matriz que contiene información de autenticación para su organización. Debe contener un solo objeto con las siguientes propiedades: <ul><li>`namespace`: Debe definirse en `imsOrgID`.</li><li>`value`: Su ID de organización de IMS. Este es el mismo valor que se proporciona en el encabezado `x-gw-ims-org-id`.</li></ul> |
| `users` | Matriz que contiene una colección de al menos un usuario cuya información desea eliminar. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`: Identificador de un usuario que se utiliza para clasificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella o buscarla más adelante.</li><li>`action`: Matriz que enumera las acciones deseadas que deben realizarse en los datos del usuario. Debe contener un solo valor de cadena: `delete`.</li><li>`userIDs`: Una colección de identidades para el usuario. El número de identidades que un solo usuario puede tener está limitado a nueve. Cada identidad contiene las siguientes propiedades: <ul><li>`namespace`: El espacio de  [nombres de ](../identity-service/namespaces.md) identidad asociado al ID. Puede ser un [espacio de nombres estándar](./api/appendix.md#standard-namespaces) reconocido por Platform o puede ser un espacio de nombres personalizado definido por su organización. El tipo de área de nombres utilizado debe reflejarse en la propiedad `type` .</li><li>`value`: El valor de identidad.</li><li>`type`: Debe establecerse en  `standard` si utiliza un espacio de nombres reconocido globalmente o  `custom` si utiliza un espacio de nombres definido por su organización.</li></ul></li></ul> |

**Respuesta**

Una respuesta correcta devuelve los detalles de los trabajos creados.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
