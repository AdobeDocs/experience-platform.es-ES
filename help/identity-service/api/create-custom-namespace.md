---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear una Área de nombres personalizada
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Creación de una Área de nombres personalizada

Mediante la API de Área de nombres de identidad, puede crear una Área de nombres de identidad personalizada que solo estará disponible para su organización.

Para obtener recomendaciones sobre la creación de Áreas de nombres personalizadas, consulte [la documentación](../troubleshooting-guide.md)de preguntas más frecuentes de Identity Service.

>[!NOTE] Las Áreas de nombres son un calificador para las identidades. Como tal, una vez creada una Área de nombres, no se puede eliminar.

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