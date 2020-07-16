---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elimine un recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# Elimine un recurso

En ocasiones puede ser necesario eliminar (DELETE) un recurso del [!DNL Schema Registry]. Solo se pueden eliminar los recursos que cree en el contenedor del inquilino. Esto se realiza realizando una solicitud de DELETE utilizando el `$id` del recurso que desea eliminar.

**Formato API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a eliminar del [!DNL Schema Library]. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{RESOURCE_ID}` | El `$id` URI con codificación URL o `meta:altId` del recurso. |

**Solicitud**

DELETE solicitudes no requieren encabezados Accept.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación mediante una solicitud de búsqueda (GET) al recurso. Deberá incluir un encabezado Accept en la solicitud, pero deberá recibir un estado HTTP 404 (no encontrado) porque el recurso se ha eliminado del [!DNL Schema Registry].