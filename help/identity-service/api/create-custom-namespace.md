---
keywords: Experience Platform;inicio;temas populares;área de nombres;área de nombres;áreas de nombres;área de nombres;área de nombres de identidad;área de nombres de identidad;identidad;identidad
solution: Experience Platform
title: Creación de un área de nombres personalizada en la API del servicio de identidad
description: Con la API de área de nombres de identidad, puede crear un área de nombres de identidad personalizada que solo estará disponible para su organización.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Creación de un área de nombres personalizada en la API del servicio de identidad

Al usar la variable [!DNL Identity Namespace] , puede crear un área de nombres de identidad personalizada que solo esté disponible para su organización.

Para obtener recomendaciones sobre la creación de áreas de nombres personalizadas, consulte [la documentación de preguntas frecuentes del servicio de ID](../troubleshooting-guide.md).

>[!NOTE]
>
>Los espacios de nombres son un calificador para identidades. Como tal, una vez que se ha creado un área de nombres, no se puede eliminar.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Continúe con el siguiente tutorial a [listar el ID nativo de una identidad](./list-native-id.md)
