---
keywords: Experience Platform;inicio;temas populares;Sandbox;Sandbox
solution: Experience Platform
title: Creación de un Simulador para pruebas en la API
topic-legacy: developer guide
description: Puede crear un nuevo simulador de pruebas realizando una solicitud de POST al extremo "/sandboxes".
exl-id: 676c5de8-2c3a-4612-9dd8-93e01cafe90e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# Creación de un simulador para pruebas en la API

Puede crear un nuevo entorno limitado realizando una solicitud de POST al extremo `/sandboxes` .

**Formato de API**

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
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en futuras solicitudes. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. No puede contener espacios ni mayúsculas. |
| `title` | Un nombre legible que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de simulador de pruebas que se va a crear. Actualmente, una organización solo puede crear entornos limitados de tipo &quot;desarrollo&quot;. |

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que su `state` está &quot;creando&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Los entornos limitados tardan aproximadamente 15 minutos en ser aprovisionados por el sistema, después de lo cual su `state` se convertirá en &quot;activo&quot; o &quot;fallido&quot;.
