---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Buscar un simulador para pruebas
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b

---


# Buscar un simulador para pruebas

Puede buscar un simulador para pruebas individual realizando una solicitud GET que incluya la propiedad del `name` simulador para pruebas en la ruta de solicitud.

**Formato API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` propiedad del simulador para pruebas que desea buscar. |

**Solicitud**

La siguiente solicitud recupera un entorno limitado denominado &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del simulador para pruebas, incluidos su `name`, `title`, `state`y `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del simulador para pruebas. Se utiliza con fines de búsqueda en llamadas de API. |
| `title` | Nombre para mostrar del simulador para pruebas. |
| `state` | Estado de procesamiento actual del simulador para pruebas. El estado de un simulador para pruebas puede ser cualquiera de los siguientes: <ul><li>**creación**: Se ha creado el simulador para pruebas, pero el sistema sigue aprovisionándolo.</li><li>**activo**: El simulador para pruebas se crea y se activa.</li><li>**error**: Debido a un error, el sistema no pudo aprovisionar el simulador para pruebas y está deshabilitado.</li><li>**eliminado**: El simulador para pruebas se ha desactivado manualmente.</li></ul> |
| `type` | El tipo de entorno limitado, ya sea &quot;desarrollo&quot; o &quot;producción&quot;. |
| `isDefault` | Una propiedad booleana que indica si este entorno limitado es el entorno limitado predeterminado para la organización. Generalmente este es el entorno limitado de producción. |
| `eTag` | Identificador de una versión específica del simulador para pruebas. Este valor se utiliza para el control de versiones y la eficacia del almacenamiento en caché y se actualiza cada vez que se realiza un cambio en el simulador para pruebas. |