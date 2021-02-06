---
keywords: Experience Platform;inicio;temas populares;identidades;historial de clúster
solution: Experience Platform
title: Obtener historial de clúster de una identidad
topic: API guide
description: Las identidades pueden mover clústeres a lo largo de varias ejecuciones de gráficos de dispositivos. El servicio de identidad proporciona visibilidad en las asociaciones de clúster de una identidad determinada a lo largo del tiempo.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---


# Obtener el historial de clúster de una identidad

Las identidades pueden mover clústeres a lo largo de varias ejecuciones de gráficos de dispositivos. [!DNL Identity Service] proporciona visibilidad en las asociaciones de clúster de una identidad determinada a lo largo del tiempo.

Utilice el parámetro opcional `graph-type` para indicar el tipo de salida desde el que se obtiene el clúster. Las opciones son:

- `None` - No realice ninguna vinculación de identidad.
- `Private Graph` - Realizar la vinculación de identidad en función del gráfico de identidad privado. Si no se proporciona `graph-type`, este es el valor predeterminado.

## Obtener el historial de clúster de una sola identidad

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Solicitud**

Opción 1: Proporcione la identidad como Área de nombres (`nsId`, por ID) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 2: Proporcione la identidad como Área de nombres (`ns`, por nombre) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 3: Proporcione la identidad como XID (`xid`). Para obtener más información sobre cómo obtener el XID de una identidad, consulte la sección de este documento que trata de [obtener el XID de una identidad](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtener el historial de clúster de varias identidades

Utilice el método `POST` como equivalente por lotes del método `GET` descrito anteriormente para devolver los historiales de clúster de varias identidades.

>[!NOTE]
>
>La solicitud no debe indicar más de un máximo de 1000 identidades. Las solicitudes que superen las 1000 identidades resultarán en un código de estado de 400.

**Formato API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Cuerpo de solicitud**

Opción 1: Proporcione una lista de XID para los que recuperar miembros del clúster.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opción 2: Proporcione una lista de identidades como ID compuestos, donde cada uno asigna un nombre al valor de ID y a la Área de nombres por código de Área de nombres.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Solicitud**

**Solicitud Stub**

El uso del encabezado `x-uis-cst-ctx: stub` devolverá una respuesta stubbed. Se trata de una solución temporal para facilitar el progreso inicial en el desarrollo de la integración, mientras se completan los servicios. Esto quedará obsoleto cuando ya no se necesite.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Uso de XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Uso de UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "compositeXids": [{
                "nsid": 411,
                "id": "WRbM7AAAAJ_PBZHl"
            },
            {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            }
        ],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Respomse**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>La respuesta siempre tendrá una entrada para cada XID proporcionado en la solicitud, independientemente de si los XID de una solicitud pertenecen al mismo clúster o si uno o más tienen algún clúster asociado.

## Pasos siguientes

Vaya al siguiente tutorial para [asignaciones de identidad de lista](./list-identity-mappings.md)