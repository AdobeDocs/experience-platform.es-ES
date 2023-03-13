---
title: Relaciones en la API de Reactor
description: Descubra cómo se establecen las relaciones de recursos en la API de Reactor, incluidos los requisitos de relación para cada recurso.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 99%

---

# Relaciones en la API de Reactor

Los recursos de la API de Reactor suelen estar relacionados entre sí. Este documento proporciona una descripción general de cómo se establecen las relaciones de recursos en la API y los requisitos de relación de cada tipo de recurso.

Según el tipo de recurso en cuestión, se requieren algunas relaciones. Una relación necesaria implica que el recurso principal no puede existir sin la relación. Todas las demás relaciones son opcionales.

Independientemente de si son necesarias u opcionales, el sistema establece automáticamente las relaciones cuando se crean los recursos relevantes, o deben crearse manualmente. En el caso de la creación manual de relaciones, hay dos métodos posibles en función del recurso en cuestión:

* [Crear por carga útil](#payload)
* [Crear por dirección URL](#url) (solo para bibliotecas)

Consulte la sección sobre [requisitos de relación](#requirements) para obtener una lista de las relaciones compatibles con cada tipo de recurso y los métodos necesarios para establecerlas cuando corresponda.

## Creación de una relación por carga útil {#payload}

Algunas relaciones deben establecerse manualmente al crear inicialmente un recurso. Para ello, debe proporcionar un objeto `relationship` en la carga útil de la solicitud cuando cree el recurso principal por primera vez. Algunos ejemplos de estas relaciones son:

* [Creación de un elemento de datos](../endpoints/data-elements.md#create) con las extensiones requeridas
* [Creación de un entorno](../endpoints/environments.md#create) con la relación de host necesaria

**Formato de API**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El ID de la propiedad a la que pertenece el recurso. |
| `{RESOURCE_TYPE}` | El tipo de recurso que se va a crear. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud crea un nuevo `rule_component`, y establece relaciones con `rules` y una `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `relationships` | Un objeto que debe proporcionarse al crear relaciones mediante carga útil. Cada clave de este objeto representa un tipo de relación específico. En el ejemplo anterior, se establecen las relaciones `extension` y `rules`, que son específicas de `rule_components`. Para obtener más información sobre los tipos de relación compatibles con distintos recursos, consulte la sección sobre [requisitos de relación por recurso](#relationship-requirements-by-resource). |
| `data` | Cada tipo de relación proporcionado en el objeto `relationship` debe contener una propiedad `data`, que hace referencia a `id` y `type` del recurso con el que se establece una relación. Puede crear una relación con varios recursos del mismo tipo dando formato a la propiedad `data` como una matriz de objetos, cada uno de los cuales contiene `id` y `type` de un recurso aplicable. |
| `id` | El ID único de un recurso. Cada `id` debe acompañarse de una propiedad `type` del mismo nivel, que indique el tipo de recurso en cuestión. |
| `type` | El tipo de recurso al que hace referencia un campo `id` del mismo nivel. Los valores aceptados incluyen `data_elements`, `rules`, `extensions` y `environments`. |

{style="table-layout:auto"}

## Creación de una relación por dirección URL {#url}

A diferencia de otros recursos, las bibliotecas establecen relaciones a través de sus propios extremos de `/relationship` dedicados. Algunos ejemplos son:

* [Adición de extensiones, elementos de datos y reglas a una biblioteca](../endpoints/libraries.md#add-resources)
* [Asignación de una biblioteca a un entorno](../endpoints/libraries.md#environment)

**Formato de API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El ID de la propiedad a la que pertenece la biblioteca. |
| `{LIBRARY_ID}` | El ID de la biblioteca para la que desea crear una relación. |
| `{RESOURCE_TYPE}` | El tipo de recurso al que se dirige la relación. Los valores de ejemplo incluyen `environment`, `data_elements`, `extensions` y `rules`. |

**Solicitud**

La siguiente solicitud utiliza el extremo `/relationships/environment` de una biblioteca para crear una relación con un entorno.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `data` | Un objeto que hace referencia a `id` y `type` del recurso de destino para la relación. Si está creando una relación con varios recursos del mismo tipo (como `extensions` y `rules`), la propiedad `data` debe tener el formato de una matriz de objetos, cada uno de los cuales contenga las propiedades `id` y `type` de un recurso aplicable. |
| `id` | El ID único de un recurso. Cada `id` debe acompañarse de una propiedad `type` del mismo nivel, que indique el tipo de recurso en cuestión. |
| `type` | El tipo de recurso al que hace referencia un campo `id` del mismo nivel. Los valores aceptados incluyen `data_elements`, `rules`, `extensions` y `environments`. |

{style="table-layout:auto"}

## Requisitos de relación por recurso {#requirements}

En las tablas siguientes se describen las relaciones disponibles para cada tipo de recurso, independientemente de si se requieren o no esas relaciones, y el método aceptado para crear manualmente la relación cuando corresponda.

>[!NOTE]
>
>Si una relación no aparece como creada por carga útil o URL, el sistema la asigna automáticamente.

### Eventos de auditoría

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### Versiones

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Llamadas

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Compañías

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### Elementos de datos

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Entornos

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Extensiones

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Hosts

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Bibliotecas

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style="table-layout:auto"}

### Notas

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### Propiedades

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### Regla componentes

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### Reglas

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### Secretos

| Relación | Requerido | Crear por carga útil | Crear por dirección URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

