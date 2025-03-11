---
title: getIdentity
description: Obtenga la identidad de un visitante sin enviar datos de evento.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 5f8a9938eaccfd2eeabc75c56608f11819a81ffa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---

# `getIdentity`

Cuando se ejecuta el comando [`sendEvent`](sendevent/overview.md), Web SDK obtiene automáticamente la identidad del visitante si no hay ninguna presente.

El comando `getIdentity` le permite obtener un ID de visitante sin enviar datos de evento.

Si necesita llamadas independientes para generar un ID de visitante y enviar datos, puede utilizar este comando.

El comando `getIdentity` pasa por el siguiente flujo para recuperar `ECID`.

1. Utiliza Web SDK para llamar a `getIdentity` o a [`appendIdentityToUrl`](appendidentitytourl.md).
1. Web SDK espera a que se proporcione la información de consentimiento.
1. Web SDK comprueba si el espacio de nombres `ECID` se solicitó en la llamada. De manera predeterminada, el espacio de nombres `ECID` siempre se incluye.
1. Web SDK lee la cookie `kndctr` y devuelve su valor como `ECID`, si existe. Esto solo devuelve el valor `ECID`, pero no el valor `regionId`.
1. Si no se ha establecido la cookie de identidad `kndctr` o se ha solicitado el espacio de nombres `"CORE"`, Web SDK realiza una solicitud a Edge Network.
1. Edge Network devuelve `ECID` y `regionId` (y `CORE ID`, si se solicita).

## Obtener identidad mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK no ofrece este comando a través de la interfaz de usuario de la extensión de etiquetas. Utilice el editor de código personalizado con sintaxis de biblioteca de JavaScript.

## Obtener identidad mediante la biblioteca JavaScript de Web SDK

Ejecute el comando `getIdentity` al llamar a la instancia configurada de Web SDK. Las siguientes opciones están disponibles al configurar este comando:

* **`namespaces`**: una matriz de áreas de nombres. El valor predeterminado es `["ECID"]`. Otros valores admitidos son:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  Puede solicitar [!DNL ECID] y [!DNL CORE ID] al mismo tiempo. Ejemplo: `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`**: un objeto [de anulación de configuración de secuencia de datos](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`identity.ECID`**: una cadena que contiene el ECID del visitante.
* **`identity.CORE`**: una cadena que contiene el CORE ID del visitante.
* **`edge.regionID`**: un entero que representa la región de Edge Network que el explorador visitó al adquirir una identidad. Es igual que la sugerencia de ubicación de Audience Manager heredada.
