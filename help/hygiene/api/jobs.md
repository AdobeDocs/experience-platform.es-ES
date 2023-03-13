---
title: Eliminación de registros mediante la API de higiene de datos
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---

# Eliminación de registros mediante la API de higiene de datos

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.

Puede acceder a la API a través de la misma ruta raíz que el [API de Privacy Service](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Primeros pasos

Esta sección proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de higiene de datos.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a la API de higiene de datos, primero debe recopilar sus credenciales de autenticación. Son las mismas credenciales que se utilizan para acceder a la API de Privacy Service. Consulte la [Resumen de API](./overview.md#getting-started) para generar valores para cada uno de los encabezados requeridos para la API de higiene de datos, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

### Leer llamadas de API de muestra

Este documento proporciona una llamada de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Experience Platform.

## Creación de un trabajo de eliminación

Puede crear un trabajo de eliminación realizando una solicitud de POST.

**Formato de API**

```http
POST /jobs
```

**Solicitud**

La carga útil de la solicitud tiene una estructura similar a la de un [Eliminar solicitud en la API de Privacy Service](../../privacy-service/api/privacy-jobs.md#access-delete). Incluye un `users` matriz cuyos objetos representan a los usuarios cuyos datos se van a eliminar.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
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
| `companyContexts` | Matriz que contiene información de autenticación de su organización. Debe contener un solo objeto con las siguientes propiedades: <ul><li>`namespace`: Debe definirse en `imsOrgID`.</li><li>`value`: su ID de organización de IMS. Es el mismo valor que se proporciona en la variable `x-gw-ims-org-id` encabezado.</li></ul> |
| `users` | Matriz que contiene una colección de al menos un usuario cuya información desea eliminar. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`: Identificador de un usuario que se utiliza para clasificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a él o buscarlo más tarde.</li><li>`action`: una matriz que enumera las acciones deseadas que se deben realizar en los datos del usuario. Debe contener un solo valor de cadena: `delete`.</li><li>`userIDs`: una colección de identidades del usuario. El número de identidades que un solo usuario puede tener está limitado a nueve. Cada identidad contiene las siguientes propiedades: <ul><li>`namespace`: La [área de nombres de identidad](../../identity-service/namespaces.md) asociado con el ID. Puede ser un [espacio de nombres estándar](../../privacy-service/api/appendix.md#standard-namespaces) Platform o puede ser un área de nombres personalizada definida por su organización. El tipo de área de nombres utilizado debe reflejarse en la variable `type` propiedad.</li><li>`value`: El valor de identidad.</li><li>`type`: debe configurarse como `standard` si se utiliza un área de nombres reconocida globalmente, o `custom` si utiliza un área de nombres definida por su organización.</li></ul></li></ul> |

{style="table-layout:auto"}

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
