---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Crear una Área de nombres personalizada
topic: API guide
description: Mediante la API de Área de nombres de identidad, puede crear una Área de nombres de identidad personalizada que solo estará disponible para su organización.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 4%

---


# Creación de una Área de nombres personalizada

Mediante la [!DNL Identity Namespace] API, puede crear una Área de nombres de identidad personalizada que solo estará disponible para su organización.

Para obtener recomendaciones sobre la creación de Áreas de nombres personalizadas, consulte [la documentación](../troubleshooting-guide.md)de preguntas más frecuentes de Identity Service.

>[!NOTE]
>
>Las Áreas de nombres son un calificador para las identidades. Como tal, una vez creada una Área de nombres, no se puede eliminar.

**Formato API**

```http
POST /idnamespace/identities
```

**Solicitud**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Respuesta**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Pasos siguientes

Vaya al siguiente tutorial para [lista del ID nativo de una identidad](./list-native-id.md)