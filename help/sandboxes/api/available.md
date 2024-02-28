---
keywords: Experience Platform;inicio;temas populares;enumerar zonas protegidas disponibles;zonas protegidas de lista
solution: Experience Platform
title: Extremo de API de zonas protegidas disponibles
description: Puede enumerar las zonas protegidas disponibles para el usuario actual realizando una solicitud de GET al extremo de las zonas protegidas disponibles.
role: Developer
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 3%

---

# Extremo de zonas protegidas disponibles

>[!NOTE]
>
>A diferencia de otros extremos proporcionados en la API de espacio aislado, este extremo está disponible para todos los usuarios, incluidos los que no tienen permisos de acceso de administración de espacio aislado.

Puede enumerar las zonas protegidas disponibles para el usuario actual realizando una solicitud de GET al extremo de las zonas protegidas disponibles.

**Formato de API**

```http
GET /{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la [documento anexo](./appendix.md#query) para obtener una lista de los parámetros disponibles. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de zonas protegidas disponibles para el usuario actual, incluidos detalles como `name`, `title`, `state`, y `type`.

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
| `name` | Nombre de la zona protegida. Se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | El nombre para mostrar de la zona protegida. |
| `state` | El estado de procesamiento actual de la zona protegida. El estado de una zona protegida puede ser cualquiera de los siguientes: <ul><li>`creating`: se ha creado la zona protegida, pero el sistema aún la está aprovisionando.</li><li>`active`: la zona protegida se crea y se activa.</li><li>`failed`: Debido a un error, el sistema no pudo aprovisionar la zona protegida y está deshabilitada.</li><li>`deleted`: la zona protegida se ha deshabilitado manualmente.</li></ul> |
| `type` | El tipo de zona protegida, ya sea de &quot;desarrollo&quot; o de &quot;producción&quot;. |
| `isDefault` | Una propiedad booleana que indica si esta zona protegida es la zona protegida de producción predeterminada para la organización. |
| `eTag` | Identificador de una versión específica de la zona protegida. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en la zona protegida. |
