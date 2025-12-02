---
title: _container
description: Ver todo el contenedor de etiquetas en un solo objeto.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

El objeto `_satellite._container` contiene la configuración completa y el contexto de tiempo de ejecución de la propiedad de etiqueta cargada en la página. Toda la información, como reglas, elementos de datos, extensiones y entornos, está disponible dentro de este objeto. Su uso principal es ayudar a depurar la implementación para que pueda ver exactamente qué lógica se expone o publica.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Este objeto solo se utiliza con fines de depuración. No vincule la lógica de producción a este objeto, haga referencia a este objeto en la implementación ni edite los valores dentro de este objeto. Adobe puede cambiar la disponibilidad de propiedades o nombres dentro de este objeto en cualquier momento.

## Campos disponibles

Los siguientes objetos están disponibles como referencia:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

El objeto `_satellite._container.buildInfo` contiene una copia de [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

El objeto `_satellite._container.company` contiene una copia de [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

El objeto `_satellite._container.dataElements` proporciona una referencia de todos los elementos de datos dentro de la propiedad de etiquetas.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Cada elemento de datos incluye las siguientes propiedades:

| Nombre | Tipo | Descripción |
|---|---|---|
| **`modulePath`** | `string` | Ruta del archivo JavaScript que determina la lógica de ese tipo de elemento de datos. |
| **`settings`** | `Settings` | La configuración del elemento de datos. Las propiedades de este objeto dependen del tipo de elemento de datos. |

## `environment`

El objeto `_satellite._container.environment` contiene una copia de [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

El objeto `_satellite._container.extensions` enumera todas las extensiones publicadas en la propiedad de etiqueta.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Cada extensión incluye las siguientes propiedades:

| Nombre | Tipo | Descripción |
|---|---|---|
| **`displayName`** | `string` | Nombre descriptivo de la extensión. |
| **`hostedLibFilesUrl`** | `string` | Ubicación de la CDN en la que reside la extensión. |
| **`modules`** | `Modules` | La lógica de JavaScript para todos los eventos, acciones, condiciones y elementos de datos que utiliza la extensión. El contenido de este objeto es diferente para cada extensión. |

## `property`

El objeto `_satellite._container.property` proporciona información sobre la propiedad de la etiqueta en sí.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Nombre | Tipo | Descripción |
|---|---|---|
| **`id`** | `string` | Identificador único de la propiedad de etiqueta. |
| **`name`** | `string` | Nombre descriptivo de la propiedad de etiquetas. |
| **`settings`** | `PropertySettings` | Configuración de esta propiedad. Consulte la siguiente tabla. |

| Nombre de configuración | Tipo | Descripción |
|---|---|---|
| **`domains`** | `string[]` | Los dominios configurados para la propiedad, tal como se estableció al [configurar una propiedad de etiqueta](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Determina si la casilla de verificación **[!UICONTROL Run rule components in sequence]** está habilitada al configurar la propiedad de etiqueta. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Determina si la casilla de verificación **[!UICONTROL Return an empty string for undefined data elements]** está habilitada al configurar la propiedad de etiqueta. |

## `_container.rules`

La matriz de objetos `rules` proporciona una referencia de todas las reglas de la propiedad de etiquetas.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Cada regla contiene los campos siguientes:

| Nombre | Tipo | Descripción |
|---|---|---|
| **`id`** | `string` | El identificador único de la regla. |
| **`name`** | `string` | Nombre descriptivo de la regla. |
| **`events`** | `Event[]` | Una matriz de eventos que ha configurado para almacenar en déclencheur la regla. |
| **`conditions`** | `Condition[]` | Una matriz de condiciones que ha configurado para almacenar en déclencheur la regla. |
| **`actions`** | `Action[]` | Una matriz de acciones que ha configurado para ejecutarse cuando se active la regla. |
