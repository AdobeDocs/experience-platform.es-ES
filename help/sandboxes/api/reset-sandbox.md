---
keywords: Experience Platform;inicio;temas populares;restablecer entorno limitado
solution: Experience Platform
title: Restablecer un Simulador para pruebas en la API
topic: developer guide
description: Los entornos limitados de desarrollo tienen una función de "restablecimiento de fábrica" que elimina todos los recursos no predeterminados de un entorno limitado. Puede restablecer un simulador para pruebas realizando una solicitud de PUT que incluya el nombre del simulador para pruebas en la ruta de solicitud.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 3%

---


# Restablecer un entorno limitado en la API

Los entornos limitados de desarrollo tienen una función de &quot;restablecimiento de fábrica&quot; que elimina todos los recursos no predeterminados de un entorno limitado. Puede restablecer un simulador para pruebas realizando una solicitud de PUT que incluya el `name` del simulador para pruebas en la ruta de solicitud.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador para pruebas que desea restablecer. |

**Solicitud**

La siguiente solicitud restablece un entorno limitado denominado &quot;dev-2&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `action` | Este parámetro debe proporcionarse en la carga útil de la solicitud con el valor &quot;reset&quot; para restablecer el simulador para pruebas. |

**Respuesta**

Una respuesta correcta devuelve los detalles del simulador para pruebas actualizado, mostrando que su `state` está &quot;restableciendo&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Una vez restablecido el entorno limitado, el sistema tarda unos 15 minutos en aprovisionarlo. Una vez aprovisionado, el `state` del simulador para pruebas se convierte en &quot;activo&quot; o &quot;fallido&quot;.