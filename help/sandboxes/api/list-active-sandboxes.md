---
keywords: Experience Platform;home;popular topics;list active sandboxes;list sandboxes
solution: Experience Platform
title: Lista de entornos limitados activos para el usuario actual
topic: developer guide
description: Puede realizar una lista de los entornos limitados activos para el usuario actual mediante una solicitud de GET al extremo raíz.
translation-type: tm+mt
source-git-commit: 6326b3072737acf30ba2aee7081ce28dc9627a9a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---


# Lista de entornos limitados activos para el usuario actual

>[!NOTE]
>
>A diferencia de otros extremos proporcionados en la API de Simulador para pruebas, este extremo está disponible para todos los usuarios, incluidos los que no tienen permisos de acceso a Administración de Simuladores para pruebas.

Puede realizar una lista de los entornos limitados que están activos para el usuario actual realizando una solicitud de GET en el extremo raíz (`/`).

**Formato API**

```http
GET /{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados. Consulte la sección sobre parámetros [de](#query) consulta para obtener más información. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
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
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del simulador para pruebas. Se utiliza con fines de búsqueda en llamadas de API. |
| `title` | Nombre para mostrar del simulador para pruebas. |
| `state` | Estado de procesamiento actual del simulador para pruebas. El estado de un simulador para pruebas puede ser cualquiera de los siguientes: <ul><li>**creación**: Se ha creado el simulador para pruebas, pero el sistema sigue aprovisionándolo.</li><li>**activo**: El simulador para pruebas se crea y se activa.</li><li>**error**: Debido a un error, el sistema no pudo aprovisionar el simulador para pruebas y está deshabilitado.</li><li>**eliminado**: El simulador para pruebas se ha deshabilitado manualmente.</li></ul> |
| `type` | El tipo de entorno limitado, ya sea &quot;desarrollo&quot; o &quot;producción&quot;. |
| `isDefault` | Una propiedad booleana que indica si este entorno limitado es el entorno limitado predeterminado para la organización. Generalmente este es el entorno limitado de producción. |
| `eTag` | Identificador de una versión específica del simulador para pruebas. Este valor se utiliza para el control de versiones y la eficacia del almacenamiento en caché y se actualiza cada vez que se realiza un cambio en el simulador para pruebas. |

## Uso de parámetros de consulta {#query}

La [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API admite el uso de parámetros de consulta para filtrar los resultados de la página al enumerar los entornos limitados.

>[!NOTE]
>
>Los parámetros `limit` y `offset` consulta deben especificarse juntos. Si solo especifica uno, la API devolverá un error. Si especifica ninguno, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --------- | ----------- |
| `limit` | El número máximo de registros que se devolverá en la respuesta. |
| `offset` | Número de entidades desde el primer registro hasta el inicio (desplazamiento) de la lista de respuesta. |
