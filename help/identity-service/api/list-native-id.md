---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtener el ID nativo de una identidad
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Obtener el XID de una identidad

Los datos de identidad suelen proporcionarse como un valor de cadena de ID y una Área de nombres de identidad en los datos XDM ingestados y al proporcionar una identidad para utilizarla en una llamada de API. Cuando se mantienen identidades en el servicio de identidad, se genera un ID y se asigna a esa identidad, denominado XID nativo. Las API de plataforma que requieren compatibilidad con datos de identidad utilizan este formulario más compacto para la ID y Área de nombres agregadas. XID es una cadena con codificación base64.

>[!NOTE] Este formato es principalmente para uso interno de Adobe. El XID nativo como valor único es más eficiente en el espacio y es lo que se utiliza internamente dentro de las soluciones de plataforma para almacenamiento y serialización. Sin embargo, no es legible por el ser humano, es opaco y requiere una llamada separada para obtenerlo para su uso.

Adquirir el XID para un valor de ID y una Área de nombres determinados mediante el servicio descrito en esta sección.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Solicitud**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
