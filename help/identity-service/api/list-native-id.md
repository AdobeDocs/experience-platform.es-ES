---
keywords: Experience Platform;inicio;temas populares;identity xid;XID
solution: Experience Platform
title: Obtención del ID nativo de una identidad
description: Los datos de identidad se proporcionan generalmente como un valor de cadena de ID y un área de nombres de identidad en los datos XDM introducidos y al proporcionar una identidad para su uso en una llamada de API. Cuando las identidades persisten en el servicio de identidad, se genera un ID y se asigna a esa identidad, denominado XID nativo. Las API de Platform que requieren compatibilidad con datos de identidad utilizan este formulario más compacto para el ID y el área de nombres agregados. XID es una cadena codificada en base64.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Obtención del ID nativo de una identidad

Los datos de identidad se proporcionan generalmente como un valor de cadena de ID y un área de nombres de identidad en los datos XDM introducidos y al proporcionar una identidad para su uso en una llamada de API. Cuando las identidades persisten en [!DNL Identity Service], se genera un ID y se asigna a esa identidad, denominado XID nativo. [!DNL Platform] API que requieren compatibilidad con datos de identidad al utilizar este formulario más compacto para el ID y el área de nombres agregados. XID es una cadena codificada en base64.

>[!NOTE]
>
>Este formato es principalmente para uso interno del Adobe. El XID nativo como valor singular ahorra espacio y es lo que se usa internamente en las soluciones [!DNL Platform] para almacenamiento y serialización. Sin embargo, no es legible en lenguaje natural, es opaco y requiere una llamada independiente para obtenerlo y utilizarlo.

Adquiera el XID para un valor de ID y un área de nombres determinados mediante el servicio descrito en esta sección.

**Formato de API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Solicitud**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
