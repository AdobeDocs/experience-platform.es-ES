---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Reemplazar un recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: 67826f838951b3202a6a04321c28daa8ee883d20

---


# Reemplazar un recurso

El Registro de Esquemas permite reemplazar un recurso completo mediante una operación PUT. Esta operación esencialmente vuelve a escribir el recurso, por lo tanto el cuerpo de la solicitud debe incluir todos los campos que serían necesarios al crear un nuevo recurso mediante una solicitud POST.

Este método es especialmente útil si desea actualizar mucha información en el recurso a la vez.

>[!NOTE] Si solo desea actualizar parte de un recurso en lugar de reemplazarlo por completo, consulte el documento sobre la [actualización de un recurso mediante una operación](update-resource.md)PATCH.

**Formato API**

Una solicitud PUT solo se puede realizar con los recursos definidos en el contenedor del inquilino.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parámetro | Descripción |
| --- | --- |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a actualizar desde la biblioteca de Esquemas. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{RESOURCE_ID}` | El `$id` URI con codificación URL o `meta:altId` del recurso. |

**Solicitud**

Esta solicitud de ejemplo sustituye al tipo de datos de Construcción de propiedades que se creó en un ejemplo anterior. El cuerpo de la solicitud tiene un aspecto similar al de la solicitud POST utilizada para crear el tipo de datos, con la diferencia de que ahora contiene un conjunto actualizado de campos con nuevos valores que sustituyen a los definidos anteriormente.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del tipo de datos, mostrando los campos y valores actualizados como se proporciona en la solicitud.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
