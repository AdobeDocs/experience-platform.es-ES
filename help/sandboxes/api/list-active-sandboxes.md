---
keywords: Experience Platform;inicio;temas populares;listar entornos limitados activos;listar entornos limitados
solution: Experience Platform
title: Lista de entornos limitados activos para el usuario actual en la API
topic: guía para desarrolladores
description: Puede enumerar los entornos limitados activos para el usuario actual realizando una solicitud de GET al extremo raíz.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Lista de entornos limitados activos para el usuario actual en la API

>[!NOTE]
>
>A diferencia de otros extremos proporcionados en la API de espacio aislado, este extremo está disponible para todos los usuarios, incluidos los que no tienen permisos de acceso de Administración de espacio aislado.

Puede enumerar los entornos limitados activos para el usuario actual realizando una solicitud de GET al extremo raíz (`/`).

**Formato de API**

```http
GET /{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados por. Consulte la sección sobre [parámetros de consulta](#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de entornos limitados que están activos para el usuario actual, incluidos detalles como `name`, `title`, `state` y `type`.

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
| `name` | Nombre del simulador de pruebas. Se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | Nombre para mostrar del simulador para pruebas. |
| `state` | Estado de procesamiento actual del simulador de pruebas. El estado de un simulador para pruebas puede ser cualquiera de los siguientes: <ul><li>**crear**: Se ha creado el simulador para pruebas, pero el sistema sigue aprovisionándolo.</li><li>**activo**: El simulador para pruebas se crea y se activa.</li><li>**error**: Debido a un error, el simulador de pruebas no pudo ser aprovisionado por el sistema y está deshabilitado.</li><li>**eliminado**: El simulador para pruebas se ha desactivado manualmente.</li></ul> |
| `type` | El tipo de entorno limitado, ya sea &quot;desarrollo&quot; o &quot;producción&quot;. |
| `isDefault` | Una propiedad booleana que indica si este entorno limitado es el entorno limitado predeterminado para la organización. Normalmente, este es el simulador para pruebas de producción. |
| `eTag` | Identificador de una versión específica del simulador de pruebas. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en el simulador para pruebas. |

## Uso de parámetros de consulta {#query}

La API [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) admite el uso de parámetros de consulta en la página y filtrar los resultados al enumerar entornos limitados.

>[!NOTE]
>
>Los parámetros de consulta `limit` y `offset` deben especificarse juntos. Si solo especifica uno, la API devolverá un error. Si no especifica ninguno, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --------- | ----------- |
| `limit` | Número máximo de registros que se van a devolver en la respuesta. |
| `offset` | Número de entidades del primer registro desde el que se inicia (desplaza) la lista de respuestas. |
