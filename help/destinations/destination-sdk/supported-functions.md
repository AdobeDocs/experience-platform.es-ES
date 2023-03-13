---
description: Experience Platform Destination SDK utiliza plantillas Pebble, lo que permite transformar los datos exportados desde Experience Platform al formato requerido por el destino.
title: Funciones de transformación compatibles en Destination SDK
exl-id: 79bed9e4-5897-4c69-a4e9-a325a408302d
source-git-commit: d18b662ba8a8415dd71ed89a806e770f3cfbe72a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 4%

---

# Funciones de transformación compatibles en Destination SDK

## Información general {#overview}

El Destination SDK Experience Platform utiliza [[!DNL Pebble] templates](https://pebbletemplates.io/), lo que permite transformar los datos exportados desde Experience Platform al formato requerido por el destino.

El Experience Platform [!DNL Pebble] La implementación de tiene algunos cambios, en comparación con la versión predeterminada proporcionada por [!DNL Pebble]. Además de las funciones integradas que ofrece el producto, [!DNL Pebble], Adobe ha creado algunas funciones adicionales que puede utilizar con Destination SDK.

## Dónde se usa {#where-to-use}

Utilice las funciones admitidas que se enumeran a continuación en esta página cuando [creación de una plantilla de transformación de mensaje](./create-template.md) para los datos exportados fuera de Experience Platform a su destino. La plantilla de transformación de mensajes se utiliza en la [configuración del servidor de destino](./server-and-template-configuration.md) para destinos de streaming.

## Requisitos previos {#prerequisites}

Para comprender los conceptos y las funciones de esta página de referencia, lea la [formato del mensaje](/help/destinations/destination-sdk/message-format.md) documento primero. Debe comprender el [estructura de un perfil](/help/destinations/destination-sdk/message-format.md#profile-structure) en Experience Platform antes de poder usar [!DNL Pebble] plantillas para transformar y los datos exportados.

Antes de avanzar a las funciones documentadas a continuación, revise los ejemplos de creación de plantillas en la sección [Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos](/help/destinations/destination-sdk/message-format.md#using-templating). Los ejemplos comienzan muy simples y aumentan en complejidad.

## Admitido [!DNL Pebble] Funciones {#supported-functions}

Desde el [!DNL Pebble] sección de etiquetas, el Destination SDK solo admite:
* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [configurado](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Uso de `for` es diferente al iterar *matriz* o *asignar* elementos de una plantilla. Al iterar a través de una matriz, puede obtener el elemento directamente. Al iterar a través de un mapa, se obtiene cada entrada del mapa, que tiene un par clave-valor.
>
> * Para ver un ejemplo de un elemento de matriz, piense en las identidades de una matriz [identityMap](./message-format.md#identities) área de nombres, donde puede iterar a través de elementos como `identityMap.gaid`, `identityMap.email`, o similar.
> * Para ver un ejemplo de un elemento de mapa, piense en [segmentMembership](./message-format.md#segment-membership).


Desde el [!DNL Pebble] filtro, el Destination SDK admite todas las funciones. Un ejemplo más abajo muestra cómo se puede usar la función `date` se puede utilizar dentro de Destination SDK.

Desde el [!DNL Pebble] sección de funciones, el Adobe sí *no* admiten el [intervalo](https://pebbletemplates.io/wiki/function/range/) función.

## Ejemplo de cómo el `date` se utiliza la función {#date-function}

Para ejemplificar cómo [!DNL Pebble] funciones se utilizan en Destination SDK; consulte a continuación cómo funciona la fecha ([Vínculo en la documentación de Pebble](https://pebbletemplates.io/wiki/filter/date/)) se utiliza para transformar el formato de una marca de tiempo.

### Caso de uso

Desea cambiar el `lastQualificationTime` marca de tiempo predeterminada [ISO 8601](https://es.wikipedia.org/wiki/ISO_8601) valor que el Experience Platform exporta a otro valor preferido por el destino.

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

Además de las funciones integradas que proporciona el [!DNL Pebble], consulte a continuación las funciones adicionales creadas por Adobe que puede utilizar para sus exportaciones de datos.

### `addedSegments` y `removedSegments` Funciones {#addedsegments-removedsegments-functions}

#### Caso de uso

Estas funciones se pueden utilizar para obtener una lista de segmentos que se añadieron o eliminaron de un perfil.

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

Ahora sabe cuál [!DNL Pebble] Las funciones de se admiten en Destination SDK, así como la forma de utilizarlas para ajustar el formato de los datos exportados según sus necesidades. A continuación, debe revisar las siguientes páginas:

* [Creación y prueba de una plantilla de transformación de mensajes](/help/destinations/destination-sdk/create-template.md)
* [Procesar operaciones de API de plantilla](/help/destinations/destination-sdk/render-template-api.md)
