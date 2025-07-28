---
title: Exploración de una base de datos mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar el contenido y la estructura de archivos de una base de datos de terceros.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 46e1a62e558a209ffed4a693cfd71ad5e76d7d98
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 7%

---

# Explorar una base de datos mediante la API [!DNL Flow Service]

Este tutorial utiliza la API [!DNL Flow Service] para explorar el contenido y la estructura de archivos de una base de datos de terceros.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a una base de datos de terceros mediante la API [!DNL Flow Service].

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../landing/api-guide.md).

## Exploración de las tablas de datos

Con el ID de conexión de la base de datos, puede explorar las tablas de datos realizando solicitudes GET. Utilice la siguiente llamada para encontrar la ruta de la tabla que desea inspeccionar o introducir en Experience Platform.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión del origen de la base de datos. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de tablas de la base de datos. Busque la tabla que desea introducir en Experience Platform y tome nota de su propiedad `path`, ya que debe proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspeccionar la estructura de una tabla

Para inspeccionar la estructura de una tabla desde la base de datos, realice una petición GET y especifique la ruta de una tabla como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de una conexión de base de datos. |
| `{TABLE_PATH}` | La ruta de una tabla. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de la tabla especificada. Los detalles relativos a cada una de las columnas de la tabla se encuentran en elementos de la matriz `columns`.

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
            }
        ]
    },
    "data": [],
    "cdcMetadata": {
      "columnDetected": true
    }
}
```

## Próximos pasos

Al seguir este tutorial, ha explorado la base de datos, encontrado la ruta de la tabla que desea introducir en Experience Platform y obtenido información sobre su estructura. Puedes usar esta información en el siguiente tutorial para [recopilar datos de tu base de datos e introducirlos en Experience Platform](../collect/database-nosql.md).
