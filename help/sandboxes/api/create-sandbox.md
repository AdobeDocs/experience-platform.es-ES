---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un simulador para pruebas
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b

---


# Creación de un simulador para pruebas

Puede crear un nuevo simulador para pruebas realizando una solicitud POST al `/sandboxes` extremo.

**Formato API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea un nuevo entorno limitado de desarrollo denominado &quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en solicitudes futuras. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. No puede contener espacios ni mayúsculas. |
| `title` | Nombre legible en lenguaje natural que se utiliza para la visualización en la interfaz de usuario de la plataforma. |
| `type` | Tipo de entorno limitado que se va a crear. Actualmente, una organización solo puede crear entornos limitados de tipo &quot;desarrollo&quot;. |

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que `state` está &quot;creando&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE] El sistema tarda aproximadamente 15 minutos en aprovisionar los Simuladores para pruebas, después de lo cual `state` se activarán o &quot;fallarán&quot;.
