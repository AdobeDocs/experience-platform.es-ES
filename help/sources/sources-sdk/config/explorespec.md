---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Configuración de especificaciones de exploración para el SDK de fuentes
topic-legacy: overview
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar el SDK de fuentes.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Configuración de especificaciones de exploración para el SDK de fuentes

Las especificaciones de exploración definen los parámetros necesarios para explorar e inspeccionar los objetos contenidos en el origen. Explorar especificaciones también define el formato de respuesta devuelto cuando se exploran e inspeccionan los objetos.

>[!TIP]
>
>Las especificaciones del explorador están codificadas y puede copiar y pegar la carga útil siguiente en la especificación de conexión.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Explorar especificaciones | Descripción | Ejemplo |
| --- | --- | --- |
| `name` | Define el nombre o el identificador de la especificación de exploración. | `Resource` |
| `type` | Define el tipo de la especificación de exploración. | `Resource` |
| `requestSpec` | Contiene los parámetros necesarios para explorar objetos en la conexión. |
| `requestSpec.type` | Define el tipo de datos de la especificación de la solicitud. | `object` |
| `responseSpec` | Contiene los parámetros que definen el formato del mensaje de respuesta devuelto contra una llamada de exploración. |
| `responseSpec.type` | Define el tipo de datos de la especificación de respuesta. | `object` |
| `responseSpec.properties` | Contiene información relacionada con el formato del mensaje de respuesta. |
| `responseSpec.properties.format` | Define el formato del esquema de respuesta. | `object` |
| `responseSpec.properties.format.type` | Define el tipo de datos de las propiedades. | `string` |
| `responseSpec.schema` | Contiene información relacionada con el formato del esquema de respuesta. |
| `responseSpec.schema.type` | Define el tipo de datos del esquema. | `object` |
| `responseSpec.schema.properties` | Contiene información sobre las columnas, el tipo y los elementos contenidos en un esquema. |
| `responseSpec.schema.properties.columns.items.properties.name` | Muestra el nombre del archivo. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Define el tipo de datos del nombre del archivo. | `string` |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Con las especificaciones de exploración rellenadas, puede continuar creando una especificación de conexión completa utilizando la variable [!DNL Flow Service] API. Consulte la [[!DNL Sources SDK] Guía de API](../api/api-overview.md) para obtener más información.