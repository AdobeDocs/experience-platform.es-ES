---
description: El Destination SDK del Experience Platform utiliza plantillas de plataforma, lo que permite transformar los datos exportados desde el Experience Platform en el formato requerido por el destino.
title: Funciones de transformación admitidas en el Destination SDK
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# Funciones de transformación admitidas en el Destination SDK

Experience Platform Destination SDK utiliza [[!DNL Pebble] plantillas](https://pebbletemplates.io/), lo que permite transformar los datos exportados desde el Experience Platform en el formato requerido por el destino.

El Experience Platform [!DNL Pebble] La implementación de tiene algunos cambios, en comparación con la versión predeterminada proporcionada por [!DNL Pebble]. Además de las funciones integradas que proporciona [!DNL Pebble], Adobe ha creado algunas funciones adicionales que puede utilizar con Destination SDK.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Dónde se utiliza {#where-to-use}

Utilice las funciones compatibles que se enumeran más adelante en esta página cuando [creación de una plantilla de transformación de mensaje](../../testing-api/streaming-destinations/create-template.md) para los datos exportados fuera del Experience Platform al destino.

La plantilla de transformación de mensaje se utiliza en la variable [configuración del servidor de destino](templating-specs.md) para destinos de flujo continuo.

## Requisitos previos {#prerequisites}

Para comprender los conceptos y las funciones de esta página de referencia, lea la [formato del mensaje](message-format.md) documento primero. Debe comprender el [estructura de un perfil](message-format.md#profile-structure) en Experience Platform antes de poder usar [!DNL Pebble] plantillas para transformar y exportar datos.

Antes de avanzar a las funciones documentadas a continuación, revise los ejemplos de creación de plantillas en la sección [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos](message-format.md#using-templating). Los ejemplos de ahí empiezan de forma muy simple y aumentan la complejidad.

## Admitido [!DNL Pebble] funciones {#supported-functions}

En el [!DNL Pebble] etiquetas , el Destination SDK solo admite:

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [configurado](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Uso `for` es diferente al iterar *matriz* o *map* elementos de una plantilla. Al iterar a través de una matriz, puede obtener el elemento directamente. Cuando se repite a través de un mapa, se obtiene cada entrada de mapa, que tiene un par clave-valor.
>
> * Para ver un ejemplo de un elemento de matriz, piense en las identidades de un [identityMap](message-format.md#identities) área de nombres, donde puede iterar entre elementos como `identityMap.gaid`, `identityMap.email`, o similar.
> * Para ver un ejemplo de un elemento de mapa, piense en [segmentMembership](message-format.md#segment-membership).


En el [!DNL Pebble] filtro , Destination SDK admite todas las funciones. Un ejemplo más abajo muestra cómo `date` puede utilizarse en Destination SDK.

En el [!DNL Pebble] sección funciones, el Adobe sí *not* soporte técnico [range](https://pebbletemplates.io/wiki/function/range/) función.

## Ejemplo de cómo `date` se utiliza {#date-function}

Para ejemplificar cómo [!DNL Pebble] en Destination SDK, consulte a continuación cómo funciona date ([vínculo en la documentación de Pebble](https://pebbletemplates.io/wiki/filter/date/)) se utiliza para transformar el formato de una marca de tiempo.

### Caso de uso

Desea cambiar la variable `lastQualificationTime` marca de tiempo de la predeterminada [ISO 8601](https://es.wikipedia.org/wiki/ISO_8601) que el Experience Platform exporta a otro valor preferido por el destino.

### Ejemplo

#### Entrada

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Formato

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Output

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funciones agregadas por Adobe {#functions-added-by-adobe}

Además de las funciones integradas que proporciona [!DNL Pebble], consulte a continuación las funciones adicionales creadas por Adobe que puede utilizar para sus exportaciones de datos.

### `addedSegments` y `removedSegments` funciones {#addedsegments-removedsegments-functions}

#### Caso de uso

Estas funciones se pueden utilizar para obtener una lista de segmentos que se han agregado o eliminado de un perfil.

#### Ejemplo

##### Entrada

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Formato

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Output

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Pasos siguientes {#next-steps}

Ahora sabe cuál [!DNL Pebble] son compatibles con Destination SDK, así como con cómo utilizarlas para ajustar el formato de los datos exportados según sus necesidades. A continuación, debe revisar las páginas siguientes:

* [Creación y prueba de una plantilla de transformación de mensaje](../../testing-api/streaming-destinations/create-template.md)
* [Operaciones de API de plantilla de procesamiento](../../testing-api/streaming-destinations/render-template-api.md)
