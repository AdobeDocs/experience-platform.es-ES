---
keywords: Experience Platform;inicio;temas populares;identidad;identidad
solution: Experience Platform
title: Asignaciones de identidad de lista
topic: API guide
description: Una asignación es una colección de todas las identidades de un clúster para una Área de nombres específica.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Asignaciones de identidad de lista

Una asignación es una colección de todas las identidades de un clúster para una Área de nombres específica.

## Obtener una asignación de identidad para una sola identidad

Dada la identidad, recupere todas las identidades relacionadas de la misma Área de nombres que la representada por la identidad en la solicitud.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Solicitud**

Opción 1: Proporcione la identidad como Área de nombres (`nsId`, por ID) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 2: Proporcione la identidad como Área de nombres (`ns`, por nombre) y valor de ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 3: Proporcione la identidad como XID (`xid`). Para obtener más información sobre cómo obtener el XID de una identidad, consulte la sección de este documento que trata de [obtener el XID de una identidad](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Obtener asignaciones de identidad para varias identidades

Utilice el método `POST` como equivalente por lotes del método `GET` descrito anteriormente para recuperar asignaciones para identidades múltiples.

>[!NOTE]
>
>La solicitud no debe indicar más de un máximo de 1000 identidades. Las solicitudes que superen las 1000 identidades resultarán en un código de estado de 400.

**Formato API**

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

Opción 2: Proporcione una lista de identidades como ID compuestos, donde cada uno asigna un nombre al valor de ID y a la Área de nombres por ID de Área de nombres. En este ejemplo se muestra el uso de este método mientras se sobrescribe el valor predeterminado `graph-type` de &quot;Private Graph&quot;.

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
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
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

Si no se encontraron identidades relacionadas con la entrada proporcionada, se devuelve un código de respuesta `HTTP 204` sin contenido.

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

- `lastAssociationTime`:: Marca de hora en la que se asoció por última vez la identidad de entrada a esta identidad.
- `regions`:: Proporciona el  `regionId` y  `lastAssociationTime` para dónde se vio la identidad.

## Pasos siguientes

Vaya al siguiente tutorial a [Áreas de nombres disponibles de lista](./list-namespaces.md).
