---
title: Información general sobre eventos de flujo capilar
description: Aprenda a transmitir datos de Capillary a Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: b3b1542f7e297f4ca872a155ac3801266bc1e6a6
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>El origen [!DNL Capillary Streaming Events] está en la versión beta. Lea los [términos y condiciones](../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

[!DNL Capillary Technologies] es una plataforma líder de lealtad y participación, en la que confían más de 300 marcas en todo el mundo. Utilice el origen [!DNL Capillary Streaming Events] para permitir que su empresa transmita sin problemas perfiles de clientes, datos de fidelidad y eventos transaccionales de [!DNL Capillary] a Adobe Experience Platform. Conecte el origen de [!DNL Capillary] para habilitar la personalización en tiempo real, la segmentación de audiencia avanzada y la orquestación de campaña omnicanal.

Al integrar [!DNL Capillary] con Experience Platform, puede:

* Sincroniza **puntos de fidelidad, niveles y recompensas** en tiempo real.
* Enviar **datos transaccionales** a Experience Platform para su análisis y activación.
* Aproveche Real-Time CDP, Experience Platform y Adobe Journey Optimizer para la segmentación, orquestación de recorrido y personalización.

## Requisitos previos

Antes de conectar [!DNL Capillary] a Adobe Experience Platform, asegúrese de que dispone de lo siguiente:

* Una **ID de organización de Adobe** válida y acceso a una zona protegida de Experience Platform habilitada.
* **[!DNL Capillary]credenciales de origen** (ID de cliente y Secreto de cliente).
* Los permisos necesarios en Adobe Admin Console para crear fuentes y flujos de datos.

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Capillary] a Experience Platform:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de cliente | Identificador de cliente para el origen [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Secreto del cliente | El secreto de cliente emitido con el ID de cliente | `xxxxxxxxxxxxxxxxxx` |
| ID de la organización | Su ID de organización de Adobe | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Para obtener más información sobre cómo generar tokens de acceso, lea la [guía de autenticación de Adobe](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Generación de un token de acceso

A continuación, utilice su ID de cliente y Secreto de cliente para generar un token de acceso desde Adobe.

**Solicitud**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Respuesta**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Próximos pasos

Una vez que haya completado la configuración de requisitos previos para [!DNL Capillary], lea la siguiente documentación para saber cómo puede conectar su cuenta e iniciar la transmisión de datos de [!DNL Capillary] a Experience Platform.

* [Conectar  [!DNL Capillary Streaming Events] a Experience Platform mediante la API](../../tutorials/api/create/loyalty/capillary.md)
* [Conectar  [!DNL Capillary Streaming Events] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/loyalty/capillary.md)
