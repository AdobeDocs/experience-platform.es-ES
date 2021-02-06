---
keywords: Experience Platform;inicio;temas populares;Simulador para pruebas;Simulador para pruebas
solution: Experience Platform
title: Creación de un Simulador para pruebas en la API
topic: developer guide
description: Puede crear un nuevo simulador para pruebas realizando una solicitud de POST al extremo "/sandboxes".
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---


# Creación de un entorno limitado en la API

Puede crear un nuevo simulador para pruebas realizando una solicitud de POST al extremo `/sandboxes`.

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

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que su `state` es &quot;crear&quot;.

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
>El sistema tarda aproximadamente 15 minutos en aprovisionar los Simuladores para pruebas, después de lo cual su `state` será &quot;activo&quot; o &quot;fallido&quot;.
