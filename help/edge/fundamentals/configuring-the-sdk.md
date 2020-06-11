---
title: Configuración del SDK
seo-title: Configuración del SDK web de la plataforma Adobe Experience
description: Descubra cómo configurar el SDK web de la plataforma de experiencia
seo-description: Descubra cómo configurar el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 11%

---


# Configuración del SDK

La configuración del SDK se realiza con el `configure` comando .

>[!IImportante]
>`configure` debe ser _siempre_ el primer comando llamado.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hay muchas opciones que se pueden configurar durante la configuración. Todas las opciones se encuentran a continuación, agrupadas por categoría.

## Opciones generales

### `edgeConfigId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

El ID de configuración asignado, que vincula el SDK con las cuentas y la configuración correspondientes.  Al configurar varias instancias dentro de una sola página, debe configurar una diferente `edgeConfigId` para cada instancia.

### `context`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matriz de cadenas | No | `["web", "device", "environment", "placeContext"]` |

Indica qué categorías de contexto se recopilarán automáticamente, tal como se describe en Información [](../reference/automatic-information.md)automática.  Si no se especifica esta configuración, se utilizan todas las categorías de forma predeterminada.

### `debugEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica si se debe habilitar la depuración. Al configurar esta configuración para que `true` habilite las siguientes funciones:

| **Función** |  |  |
| ---------------------- | ------------------ |
| Validación sincrónica | Valida los datos que se recopilan con el esquema y devuelve un error en la respuesta bajo la siguiente etiqueta: `collect:error OR success` |
| Registro de la consola | Permite que los mensajes de depuración se muestren en la consola JavaScript del explorador |

### `edgeDomain`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ------------------ |
| Cadena | No | `beta.adobedc.net` |

Dominio utilizado para interactuar con los servicios de Adobe. Solo se utiliza si tiene un dominio de origen (CNAME) que proxies solicitudes a la infraestructura Edge de Adobe.

### `orgId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

Su ID de organización de Experience Cloud asignado.  Al configurar varias instancias dentro de una página, debe configurar una diferente `orgId` para cada instancia.

## Recopilación de datos

### `clickCollectionEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica si los datos asociados con los clics en vínculos se deben recopilar automáticamente. Para los clics que se califican como clics en vínculos, se recopilan los siguientes datos de interacción [](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Web:

| **Propiedad** |  |
| ------------ | ----------------------------------- |
| Nombre del vínculo | Nombre determinado por el contexto del vínculo |
| URL del vínculo | URL normalizada |
| Tipo de vínculo | Configurar para descargar, salir u otro |

### `onBeforeEventSend`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Función | No | () => undefined |

Configure esta opción para configurar una llamada de retorno que se llame para cada evento justo antes de que se envíe.  Se `xdm` envía un objeto con el campo a la llamada de retorno.  Modifique el objeto xdm para cambiar lo que se envía.  Dentro de la llamada de retorno, el `xdm` objeto ya tendrá los datos pasados en el comando evento y la información recopilada automáticamente.  Para obtener más información sobre la temporización de esta llamada de retorno y un ejemplo, consulte [Modificación global de Eventos](tracking-events.md#modifying-events-globally).

## Opciones de privacidad

### `defaultConsent`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Objeto | No | `{"general": "in"}` |

Establece el consentimiento predeterminado del usuario. Se utiliza cuando no hay ninguna preferencia de consentimiento ya guardada para el usuario. El otro valor válido es `{"general": "pending"}`. Cuando se establece, el trabajo se pone en cola hasta que el usuario proporciona las preferencias de consentimiento. Una vez proporcionadas las preferencias del usuario, el trabajo continúa o se anula según sus preferencias. Consulte [Compatibilidad con el consentimiento](supporting-consent.md) para obtener más información.

## Opciones de personalización

### `prehidingStyle`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | No | none |

Se utiliza para crear una definición de estilo CSS que oculta las áreas de contenido de la página web mientras se carga contenido personalizado desde el servidor. Si no se proporciona esta opción, el SDK no intenta ocultar ninguna área de contenido mientras se carga el contenido personalizado, lo que podría dar como resultado un &quot;parpadeo&quot;.

Por ejemplo, si tuviera un elemento en la página web con un ID del `container` contenido predeterminado que desee ocultar mientras se carga contenido personalizado desde el servidor, un ejemplo de estilo de ocultación previa sería el siguiente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opciones de Audiencias

### `cookieDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita los destinos de cookies, lo que permite configurar las cookies en función de la calificación del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita los destinos de URL, lo que permite activar las direcciones URL en función de la calificación del segmento.

## Opciones de identidad

### `idSyncContainerId`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Número | No | none |

El ID de contenedor que especifica qué sincronizaciones de ID se activan. Se trata de un entero no negativo que se puede obtener de su consultor.

### `idSyncEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Habilita la función de sincronización de ID, que permite activar direcciones URL para sincronizar el ID de usuario único de Adobe con el ID de usuario único de un origen de datos de terceros.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se utilice el mismo ID de visitante en todo el sitio. Esto resulta útil si tiene varios sitios o desea compartir datos con socios; sin embargo, a veces esto no es deseable por razones de privacidad.
