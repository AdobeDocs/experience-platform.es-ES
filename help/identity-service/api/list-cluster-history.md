---
keywords: Experience Platform;inicio;temas populares;identidades;historial de clústeres
solution: Experience Platform
title: Obtención del historial de clústeres de una identidad
description: Las identidades pueden mover clústeres a lo largo de varias ejecuciones de gráficos de dispositivos. El servicio de identidad proporciona visibilidad sobre las asociaciones de clúster de una identidad determinada a lo largo del tiempo.
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---

# Obtener el historial de clúster de una identidad

Las identidades pueden mover clústeres a lo largo de varias ejecuciones de gráficos de dispositivos. [!DNL Identity Service] proporciona visibilidad de las asociaciones de clúster de una identidad determinada a lo largo del tiempo.

Use opcional `graph-type` para indicar el tipo de salida desde el que se obtiene el clúster. Las opciones son:

- `None` - No realice ninguna vinculación de identidad.
- `Private Graph` - Realice la vinculación de identidad en función de su gráfico de identidad privada. Si no `graph-type` es el valor predeterminado.

## Obtener el historial de clúster de una sola identidad

**Formato de API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Solicitud**

Opción 1: Proporcione la identidad como área de nombres (`nsId`, por ID) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 2: Proporcione la identidad como área de nombres (`ns`, por nombre) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 3: Proporcione la identidad como XID (`xid`). Para obtener más información sobre cómo obtener el XID de una identidad, consulte la sección de este documento que cubre [obtención del XID para una identidad](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtener el historial de clústeres de varias identidades

Utilice la variable `POST` como equivalente de lote de `GET` método descrito anteriormente para devolver los historiales de clúster de varias identidades.

>[!NOTE]
>
>La solicitud no debe indicar más de un máximo de 1000 identidades. Las solicitudes que superen las 1000 identidades resultarán en un código de estado de 400.

**Formato de API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Cuerpo de la solicitud**

Opción 1: Proporcione una lista de XID para los que recuperar miembros del clúster.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opción 2: Proporcione una lista de identidades como ID compuestos, donde cada una asigna un nombre al valor de ID y al área de nombres por código de área de nombres.

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

Uso de `x-uis-cst-ctx: stub` devolverá una respuesta de combinación. Se trata de una solución temporal para facilitar el progreso temprano en el desarrollo de la integración, mientras que los servicios se están completando. Esto quedará obsoleto cuando ya no se necesite.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Continúe con el siguiente tutorial a [asignación de identidad de lista](./list-identity-mappings.md)
