---
keywords: Experience Platform;inicio;temas populares;identidad;identidad
solution: Experience Platform
title: Enumerar asignaciones de identidad
description: Una asignación es una colección de todas las identidades de un clúster para un área de nombres especificada.
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---

# Enumerar asignaciones de identidad

Una asignación es una colección de todas las identidades de un clúster para un área de nombres especificada.

## Obtener una asignación de identidad para una sola identidad

Dada una identidad, recupere todas las identidades relacionadas del mismo área de nombres que la representada por la identidad en la solicitud.

**Formato de API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Solicitud**

Opción 1: Proporcione la identidad como área de nombres (`nsId`, por ID) y el valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 2: Proporcione la identidad como área de nombres (`ns`, por nombre) y el valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 3: proporcionar la identidad como XID (`xid`). Para obtener más información sobre cómo obtener el XID de una identidad, consulte la sección de este documento que trata [obtención del XID de una identidad](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Obtener asignaciones de identidad para varias identidades

Utilice el `POST` como equivalente de lote del método `GET` método descrito anteriormente para recuperar asignaciones para varias identidades.

>[!NOTE]
>
>La solicitud no debe indicar más de 1000 identidades. Las solicitudes que superen las 1000 identidades resultarán en 400 códigos de estado.

**Formato de API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Cuerpo de solicitud**

Opción 1: Proporcione una lista de XID para los que recuperar asignaciones.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opción 2: Proporcione una lista de identidades como ID compuestos, donde cada una de ellas nombra el valor de ID y el área de nombres por ID de área de nombres. En este ejemplo se muestra cómo utilizar este método al sobrescribir el predeterminado `graph-type` de &quot;Private Graph&quot;.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Solicitud**

**Uso de XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Uso de UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
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
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Si no se encontraron identidades relacionadas con la entrada proporcionada, una `HTTP 204` el código de respuesta se devuelve sin contenido.

**Respuesta**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: Marca de tiempo en la que la identidad de entrada se asoció por última vez a esta identidad.
- `regions`: proporciona el `regionId` y `lastAssociationTime` para ver dónde se vio la identidad.

## Pasos siguientes

Continúe con el siguiente tutorial para [enumerar áreas de nombres disponibles](./list-namespaces.md).
