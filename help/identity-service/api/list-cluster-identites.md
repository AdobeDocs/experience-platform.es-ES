---
keywords: Experience Platform;inicio;temas populares;identidades de lista;clúster de lista
solution: Experience Platform
title: Mostrar todas las identidades en un clúster
description: Las identidades relacionadas en un gráfico de identidad, independientemente del área de nombres, se consideran parte del mismo "clúster" en ese gráfico de identidad. Las siguientes opciones proporcionan los medios para acceder a todos los miembros del clúster.
role: Developer
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# Mostrar todas las identidades de un clúster

Las identidades relacionadas en un gráfico de identidad, independientemente del área de nombres, se consideran parte del mismo &quot;clúster&quot; en ese gráfico de identidad. Las siguientes opciones proporcionan los medios para acceder a todos los miembros del clúster.

## Obtener identidades asociadas para una sola identidad

Recupere todos los miembros del clúster para una sola identidad.

Puede usar el parámetro `graph-type` opcional para indicar el gráfico de identidad desde el que obtener el clúster. Las opciones son:

- Ninguno: no realice ninguna vinculación de identidad.
- Gráfico privado: realice la vinculación de identidad en función de su gráfico de identidad privada. Si no se proporciona ningún `graph-type`, este es el valor predeterminado.

**Formato de API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Solicitud**

Opción 1: proporcione la identidad como área de nombres (`nsId`, por identificador) y valor de identificador (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 2: proporcione la identidad como área de nombres (`ns`, por nombre) y valor de identificador (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opción 3: proporcione la identidad como XID (`xid`). Para obtener más información sobre cómo obtener el XID de una identidad, consulte la sección de este documento que trata sobre [obtención del XID para una identidad](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Obtener identidades asociadas para varias identidades

Use `POST` como equivalente de lote del método `GET` descrito anteriormente para devolver las identidades en los clústeres de varias identidades.

>[!NOTE]
>
>La solicitud no debe indicar más de 1000 identidades. Las solicitudes que superen las 1000 identidades resultarán en 400 códigos de estado.

**Formato de API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Solicitud**

La siguiente solicitud muestra cómo se proporciona una lista de XID para los que se recuperan miembros de clúster.

**Solicitud de código auxiliar**

El uso del encabezado `x-uis-cst-ctx: stub` devolverá una respuesta con errores. Se trata de una solución temporal para facilitar el progreso temprano del desarrollo de la integración, mientras se completan los servicios. Esto quedará obsoleto cuando ya no sea necesario.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Llamar usando XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Llamar usando UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Respuesta**

**&#39;Stubbed&#39; response**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Respuesta completa**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>La respuesta siempre tendrá una entrada para cada XID proporcionado en la solicitud, independientemente de si los XID de una solicitud pertenecen al mismo clúster o si uno o más tienen algún clúster asociado.

## Pasos siguientes

Continúe con el siguiente tutorial para [enumerar el historial de clúster de una identidad](./list-cluster-history.md)
