---
keywords: Experience Platform;inicio;temas populares;Área de nombres;Área de nombres;Áreas de nombres;Áreas de nombres;Área de nombres de identidad;Área de nombres de identidad;identidad;identidad;identidad
solution: Experience Platform
title: Creación de una Área de nombres personalizada en la API de servicio de identidad
topic: API guide
description: Mediante la API de Área de nombres de identidad, puede crear una Área de nombres de identidad personalizada que solo estará disponible para su organización.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---


# Creación de una Área de nombres personalizada en la API de servicio de identidad

Mediante la API [!DNL Identity Namespace], puede crear una Área de nombres de identidad personalizada que estará disponible solamente para su organización.

Para obtener recomendaciones sobre la creación de Áreas de nombres personalizadas, consulte [la documentación de preguntas más frecuentes de Identity Service](../troubleshooting-guide.md).

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