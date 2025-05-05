---
description: Experience Platform Destination SDK utiliza plantillas Pebble, lo que permite transformar los datos exportados desde Experience Platform al formato requerido por el destino.
title: Funciones de transformación compatibles en Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Funciones de transformación compatibles en Destination SDK

El Destination SDK de Experience Platform usa [[!DNL Pebble] templates](https://pebbletemplates.io/), lo que le permite transformar los datos exportados desde el Experience Platform al formato requerido por el destino.

La implementación del Experience Platform [!DNL Pebble] tiene algunos cambios, en comparación con la versión predeterminada proporcionada por [!DNL Pebble]. Además de las funciones predeterminadas proporcionadas por [!DNL Pebble], Adobe ha creado algunas funciones adicionales que puede usar con Destination SDK.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1&rbrace;.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Dónde se usa {#where-to-use}

Use las funciones admitidas que se enumeran a continuación en esta página al [crear una plantilla de transformación de mensajes](../../testing-api/streaming-destinations/create-template.md) para los datos exportados fuera de Experience Platform a su destino.

La plantilla de transformación de mensajes se usa en la [configuración del servidor de destino](templating-specs.md) para los destinos de flujo continuo.

## Requisitos previos {#prerequisites}

Para comprender los conceptos y las funciones de esta página de referencia, lea primero el documento [formato del mensaje](message-format.md). Necesita comprender la [estructura de un perfil](message-format.md#profile-structure) en Experience Platform para poder usar las plantillas [!DNL Pebble] para transformar y exportar los datos.

Antes de avanzar a las funciones documentadas a continuación, revise los ejemplos de creación de plantillas en la sección [Uso de un idioma de creación de plantillas para las transformaciones de identidad, atributos y pertenencia a audiencias](message-format.md#using-templating). Los ejemplos comienzan muy simples y aumentan en complejidad.

## Funciones [!DNL Pebble] compatibles {#supported-functions}

Desde la sección de etiquetas [!DNL Pebble], el Destination SDK solo admite:

* [filtro](https://pebbletemplates.io/wiki/tag/filter/)
* [para](https://pebbletemplates.io/wiki/tag/for/)
* [si](https://pebbletemplates.io/wiki/tag/if/)
* [conjunto](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>El uso de `for` es diferente al iterar a través de *matriz* o *mapa* elementos en una plantilla. Al iterar a través de una matriz, puede obtener el elemento directamente. Al iterar a través de un mapa, se obtiene cada entrada del mapa, que tiene un par clave-valor.
>
> * Para ver un ejemplo de un elemento de matriz, piense en las identidades de un área de nombres [identityMap](message-format.md#identities), donde podría iterar a través de elementos como `identityMap.gaid`, `identityMap.email` o similares.
> * Para ver un ejemplo de un elemento de asignación, vea [segmentMembership](message-format.md#segment-membership).

Desde la sección de filtros [!DNL Pebble], el Destination SDK admite todas las funciones. Un ejemplo más abajo muestra cómo se puede usar la función `date` en el Destination SDK.

Desde la sección de funciones [!DNL Pebble], el Adobe *no* admite la función [range](https://pebbletemplates.io/wiki/function/range/).

## Ejemplo de cómo se utiliza la función `date` {#date-function}

Para ejemplificar cómo se usan las funciones [!DNL Pebble] en Destination SDK, vea a continuación cómo se usa la función de fecha ([link en la documentación de Pebble](https://pebbletemplates.io/wiki/filter/date/)) para transformar el formato de una marca de tiempo.

### Ejemplo de uso

Desea cambiar la marca de tiempo `lastQualificationTime` del valor predeterminado [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) que el Experience Platform exporta a otro valor preferido por el destino.

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

#### Salida

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funciones agregadas por Adobe {#functions-added-by-adobe}

Además de las funciones predeterminadas proporcionadas por [!DNL Pebble], vea a continuación las funciones adicionales creadas por Adobe que puede utilizar para sus exportaciones de datos.

### Funciones `addedSegments` y `removedSegments` {#addedsegments-removedsegments-functions}

#### Ejemplo de uso

Estas funciones se pueden utilizar para obtener una lista de audiencias que se añadieron o eliminaron de un perfil.

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

##### Salida

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

Ahora sabe qué funciones de [!DNL Pebble] se admiten en Destination SDK, así como cómo utilizarlas para ajustar el formato de los datos exportados según sus necesidades. A continuación, debe revisar las siguientes páginas:

* [Creación y prueba de una plantilla de transformación de mensajes](../../testing-api/streaming-destinations/create-template.md)
* [Procesar operaciones de API de plantilla](../../testing-api/streaming-destinations/render-template-api.md)
