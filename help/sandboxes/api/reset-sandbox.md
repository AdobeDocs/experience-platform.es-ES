---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Restablecer un entorno limitado
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Restablecer un entorno limitado

Los entornos limitados de desarrollo tienen una función de &quot;restablecimiento de fábrica&quot; que elimina todos los recursos no predeterminados de un entorno limitado. Puede restablecer un simulador para pruebas realizando una solicitud PUT que incluya el simulador para pruebas `name` en la ruta de solicitud.

**Formato API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` propiedad del simulador para pruebas que desea restablecer. |

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

Una respuesta correcta devuelve los detalles del simulador para pruebas actualizado, mostrando que `state` se está &quot;restableciendo&quot;.

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

>[!NOTE] Una vez restablecido el entorno limitado, el sistema tarda unos 15 minutos en aprovisionarlo. Una vez aprovisionado, el simulador de pruebas `state` se convierte en &quot;activo&quot; o &quot;fallido&quot;.