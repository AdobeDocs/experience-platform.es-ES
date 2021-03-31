---
keywords: Experience Platform;inicio;temas populares;Sandbox;Sandbox
solution: Experience Platform
title: Creación de un Simulador para pruebas en la API
topic: guía para desarrolladores
description: Puede crear un nuevo simulador de pruebas realizando una solicitud de POST al extremo "/sandboxes".
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# Creación de un simulador para pruebas en la API

Puede crear un entorno limitado de desarrollo o producción realizando una solicitud de POST al extremo `/sandboxes` .

## Creación de un entorno limitado de desarrollo

Para crear un entorno limitado de desarrollo, realice una solicitud de POST al extremo `/sandboxes` y proporcione el valor `development` para la propiedad `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en futuras solicitudes. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de simulador de pruebas que se va a crear. El valor de la propiedad `type` puede ser de desarrollo o producción. |

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

## Creación de un simulador para pruebas de producción

>[!NOTE]
>
>La función Entornos aislados de producción múltiple está en fase beta.

Para crear un entorno limitado de producción, realice una solicitud de POST al extremo `/sandboxes` y proporcione el valor `production` para la propiedad `type`.

**Formato de API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea un nuevo entorno limitado de producción denominado &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en futuras solicitudes. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de simulador de pruebas que se va a crear. El valor de la propiedad `type` puede ser de desarrollo o producción. |

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que su `state` está &quot;creando&quot;.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
