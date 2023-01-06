---
keywords: Experience Platform;inicio;temas populares;id de identidad xid;XID
solution: Experience Platform
title: Obtención del ID nativo de una identidad
description: Los datos de identidad generalmente se proporcionan como un valor de cadena de ID y un área de nombres de identidad en los datos XDM incorporados y al proporcionar una identidad para utilizarlos en una llamada de API. Cuando se mantienen identidades en el servicio de identidad, se genera un ID que se asigna a esa identidad, denominado XID nativo. Las API de plataforma que requieren compatibilidad con datos de identidad utilizan este formulario más compacto para el ID agregado y el área de nombres. XID es una cadena codificada base64.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Obtención del ID nativo de una identidad

Los datos de identidad generalmente se proporcionan como un valor de cadena de ID y un área de nombres de identidad en los datos XDM incorporados y al proporcionar una identidad para utilizarlos en una llamada de API. Cuando las identidades se mantienen en [!DNL Identity Service], se genera un ID que se asigna a esa identidad, denominado XID nativo. [!DNL Platform] Las API que requieren compatibilidad con datos de identidad utilizan este formulario más compacto para el ID agregado y el área de nombres. XID es una cadena codificada base64.

>[!NOTE]
>
>Este formato es principalmente para uso de Adobe interno. El XID nativo como valor único es más eficiente en el espacio y es lo que se utiliza internamente dentro de [!DNL Platform] soluciones para almacenamiento y serialización. Sin embargo, no es legible por el ser humano, es opaco y requiere una llamada separada para obtenerlo para su uso.

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
