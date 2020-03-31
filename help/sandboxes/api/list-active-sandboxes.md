---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Lista de entornos limitados activos para el usuario actual
topic: developer guide
translation-type: tm+mt
source-git-commit: 982764ae7807e40cbca5ca60c70bf363a271e3c2

---


# Lista de entornos limitados activos para el usuario actual

>[!NOTE] A diferencia de otros extremos proporcionados en la API de Simulador para pruebas, este extremo está disponible para todos los usuarios, incluidos los que no tienen permisos de acceso a Administración de Simuladores para pruebas.

Puede realizar una lista de los entornos limitados activos para el usuario actual mediante una solicitud GET al extremo raíz (`/`).

**Formato API**

```http
GET /
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de entornos limitados que están activos para el usuario actual, incluidos detalles como `name`, `title`, `state`y `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ]
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
