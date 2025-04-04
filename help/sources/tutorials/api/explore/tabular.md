---
keywords: Experience Platform;inicio;temas populares;fuentes;API;explorar;servicio de flujo
title: Exploración de una Source tabular mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar el contenido y la estructura de un origen basado en tablas.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 6%

---

# Explorar tablas de datos mediante la API [!DNL Flow Service]

Este tutorial proporciona pasos sobre cómo explorar y previsualizar la estructura y el contenido de las tablas de datos mediante la API [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Para explorar las tablas de datos, ya debe tener un identificador de conexión base válido para un origen tabular. Si no tiene este ID, consulte los siguientes tutoriales para ver los pasos sobre cómo crear un ID de conexión base para un origen tabular: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Éxito del cliente](../../../home.md#customer-success)</li><li>[Database](../../../home.md#database)</li><li>[Comercio electrónico](../../../home.md#ecommerce)</li><li>[Automatización de marketing](../../../home.md#marketing-automation)</li><li>[Pagos](../../../home.md#payments)</li><li>[Protocolos](../../../home.md#protocols)</li></ul>

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../landing/api-guide.md).

## Exploración de las tablas de datos

Puede recuperar información sobre la estructura de sus tablas de datos realizando una petición GET a la API [!DNL Flow Service] y proporcionando al mismo tiempo el ID de conexión base de su origen.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de su origen. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de tablas de origen. Busque la tabla que desea introducir en Experience Platform y tome nota de su propiedad `path`, ya que debe proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspeccionar la estructura de una tabla

Para inspeccionar el contenido de las tablas de datos, realice una petición GET a la API [!DNL Flow Service] y especifique la ruta de una tabla como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de su origen. |
| `{TABLE_PATH}` | La propiedad path de la tabla que desea inspeccionar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve información sobre el contenido y la estructura de la tabla especificada. Los detalles relativos a cada una de las columnas de la tabla se encuentran en elementos de la matriz `columns`.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Pasos siguientes

Al seguir este tutorial, ha recopilado información sobre la estructura y el contenido de las tablas de datos. Además, ha recuperado la ruta a la tabla que desea introducir en Experience Platform. Puede utilizar esta información para crear una conexión de origen y un flujo de datos para llevar los datos a Experience Platform. Consulte los siguientes tutoriales para ver los pasos específicos sobre cómo crear una conexión de origen y un flujo de datos mediante la API [!DNL Flow Service]:

* [Fuentes de Advertising](../collect/advertising.md)
* [Fuentes CRM](../collect/crm.md)
* [Fuentes de éxito del cliente](../collect/customer-success.md)
* [Orígenes de base de datos](../collect/database-nosql.md)
* [Fuentes de comercio electrónico](../collect/ecommerce.md)
* [Fuentes de automatización de marketing](../collect/marketing-automation.md)
* [Fuentes de pagos](../collect/payments.md)
* [Fuentes de protocolos](../collect/protocols.md)
