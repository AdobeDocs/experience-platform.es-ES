---
title: Datos de identidad en el SDK web de Platform
description: Obtenga información sobre cómo recuperar y administrar Adobe Experience Cloud ID (ECID) mediante el SDK web de Adobe Experience Platform.
keywords: Identidad;Identidad de origen;Servicio de identidad;Identidad de terceros;Migración de ID;ID de visitante;identidad de terceros;Cookies de tercerosEnabled;idMigrationEnabled;getIdentity;Sincronización de identidades;syncIdentity;sendEvent;identityMap;principal;ecid;espacio de nombres;id de área de nombres;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: d6aed404828d06bf223f348dd97960652b05933a
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 1%

---

# Datos de identidad en el SDK web de Platform

El SDK web de Adobe Experience Platform aprovecha [Adobe Experience Cloud ID (ECID)](../../identity-service/ecid.md) para realizar un seguimiento del comportamiento de los visitantes. Con los ECID, se puede garantizar que cada dispositivo tenga un identificador único que pueda persistir en varias sesiones, vinculando todas las visitas que se producen durante y entre sesiones web a un dispositivo específico.

Este documento proporciona información general sobre cómo administrar los ECID mediante el SDK web de Platform.

## Seguimiento de ECID mediante el SDK

El SDK web de Platform asigna y rastrea los ECID mediante el uso de cookies, con varios métodos disponibles para configurar cómo se generan estas cookies.

Cuando un nuevo usuario llega a su sitio web, el servicio de identidad de Adobe Experience Cloud intenta establecer una cookie de identificación de dispositivo para ese usuario. Para los visitantes nuevos, se genera un ECID que se devuelve en la primera respuesta de Adobe Experience Platform Edge Network. Para los visitantes repetidos, el ECID se recupera del `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` y la red perimetral la agrega a la carga útil.

Una vez configurada la cookie que contiene el ECID, cada solicitud posterior generada por el SDK web incluirá un ECID codificado en la variable `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Al utilizar cookies para la identificación de dispositivos, tiene dos opciones para interactuar con la red perimetral:

1. Enviar datos directamente al dominio de red perimetral `adobedc.net`. Este método se denomina [recopilación de datos de terceros](#third-party).
1. Cree un CNAME en su propio dominio que apunte a `adobedc.net`. Este método se denomina [recopilación de datos de origen](#first-party).

Como se explica en las secciones siguientes, el método de recopilación de datos que elija usar tiene un impacto directo en la duración de las cookies en los distintos navegadores.

### Recopilación de datos de terceros {#third-party}

La recopilación de datos de terceros implica enviar datos directamente al dominio de red perimetral `adobedc.net`.

En los últimos años, los navegadores web se han vuelto cada vez más restrictivos en su gestión de cookies establecidas por terceros. Algunos exploradores bloquean las cookies de terceros de forma predeterminada. Si usa cookies de terceros para identificar visitantes del sitio, la duración de esas cookies es casi siempre menor que la que estaría disponible de otro modo mediante cookies de origen. En algunos casos, una cookie de terceros caducará en tan solo siete días.

Además, cuando se utiliza la recopilación de datos de terceros, algunos bloqueadores de anuncios restringen el tráfico a los extremos de recopilación de datos de Adobe.

### Recopilación de datos de origen {#first-party}

La recopilación de datos de origen implica la configuración de cookies a través de un CNAME en su propio dominio que señala a `adobedc.net`.

Aunque los exploradores han tratado las cookies establecidas por los endpoints CNAME de forma similar a las establecidas por los endpoints de propiedad del sitio, los cambios recientes implementados por los exploradores han creado una distinción en el modo en que se gestionan las cookies CNAME. Aunque no hay exploradores que actualmente bloqueen las cookies CNAME de origen de forma predeterminada, algunos exploradores restringen la duración de las cookies configuradas con un CNAME a solo siete días.

### Efectos de las cookies en las aplicaciones de Adobe Experience Cloud {#lifespans}

Independientemente de si elige la recopilación de datos de origen o de terceros, el tiempo que una cookie puede persistir tiene un impacto directo en el recuento de visitantes en Adobe Analytics y en el Customer Journey Analytics. Además, los usuarios finales pueden experimentar experiencias de personalización incoherentes cuando se utiliza Adobe Target o Offer decisioning en el sitio.

Por ejemplo, imaginemos una situación en la que ha creado una experiencia de personalización que promoverá cualquier artículo a la página principal si un usuario lo ha visto tres veces en los últimos siete días.

Si un usuario final visita el sitio tres veces en una semana y luego no vuelve al sitio durante siete días, ese uso podría considerarse como un usuario nuevo cuando vuelva al sitio, ya que las cookies pueden haber sido eliminadas por una directiva de explorador (en función del explorador que estaba usando cuando visitó el sitio). Si esto sucede, la herramienta Analytics tratará al visitante como un nuevo usuario aunque haya visitado el sitio hace poco más de siete días. Además, cualquier esfuerzo para personalizar la experiencia para el usuario empezará de nuevo.

### ID de dispositivos de origen

Para tener en cuenta los efectos de los planes de vida de las cookies como se describe más arriba, puede optar por establecer y administrar sus propios identificadores de dispositivo. Consulte la guía de [ID de dispositivos de origen](./first-party-device-ids.md) para obtener más información.

## Recuperación del ECID y la región para el usuario actual

Para recuperar el ECID único para el visitante actual, utilice la variable `getIdentity` comando. Para los visitantes nuevos que aún no tienen un ECID, este comando genera un nuevo ECID. `getIdentity` también devuelve el ID de región del visitante.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer la variable [!DNL Experience Cloud] ID o necesita una sugerencia de ubicación para Adobe Audience Manager. No se utiliza en una implementación estándar.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Utilización `identityMap`

Uso de un XDM [`identityMap` field](../../xdm/schema/composition.md#identityMap), puede identificar un dispositivo o usuario que utilice varias identidades, establecer su estado de autenticación y decidir qué identificador se considera el principal. Si no se ha establecido ningún identificador como `primary`, el valor predeterminado principal es `ECID`.

`identityMap` los campos se actualizan utilizando la variable `sentEvent` comando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

Cada propiedad de `identityMap` representa identidades pertenecientes a una [área de nombres de identidad](../../identity-service/namespaces.md). El nombre de la propiedad debe ser el símbolo del área de nombres de identidad, que puede encontrar en la interfaz de usuario de Adobe Experience Platform en &quot;[!UICONTROL Identidades]&quot;. El valor de la propiedad debe ser una matriz de identidades pertenecientes a ese área de nombres de identidad.

>[!IMPORTANT]
>
>El ID de área de nombres pasado en la variable `identityMap` distingue entre mayúsculas y minúsculas. Asegúrese de utilizar el ID de área de nombres correcto para evitar una recopilación de datos incompleta.

Cada objeto de identidad de la matriz de identidades contiene las siguientes propiedades:

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | **(Obligatorio)** El ID que desea establecer para el área de nombres dada. |
| `authenticationState` | Cadena | **(Obligatorio)** El estado de autenticación del ID. Los valores posibles son `ambiguous`, `authenticated`y `loggedOut`. |
| `primary` | Booleano | Determina si esta identidad debe utilizarse como fragmento principal en el perfil. De forma predeterminada, el ECID se establece como identificador principal para el usuario. Si se omite, el valor predeterminado es `false`. |

## Migración de la API de visitante a ECID

Al migrar desde la API de visitante, también puede migrar las cookies AMCV existentes. Para habilitar la migración de ECID, establezca la variable `idMigrationEnabled` en la configuración. La migración de ID habilita los siguientes casos de uso:

* Cuando algunas páginas de un dominio utilizan la API de visitante y otras páginas utilizan este SDK. Para admitir este caso, el SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. Además, el SDK escribe cookies AMCV de modo que si el ECID se obtiene primero en una página instrumentada con el SDK, las páginas posteriores instrumentadas con la API de visitante tendrán el mismo ECID.
* Cuando el SDK web de Adobe Experience Platform se configura en una página que también tiene la API de visitante. Para admitir este caso, si no se establece la cookie AMCV, el SDK busca la API de visitante en la página y la llama para obtener el ECID.
* Cuando todo el sitio utiliza el SDK web de Adobe Experience Platform y no tiene la API de visitante, resulta útil migrar los ECID para conservar la información de visitante de retorno. Una vez implementado el SDK con `idMigrationEnabled` durante un periodo de tiempo para migrar la mayoría de las cookies del visitante, la configuración se puede desactivar.

### Actualización de características para la migración

Cuando se envían datos con formato XDM al Audience Manager, estos datos deben convertirse en señales al migrar. Los rasgos deberán actualizarse para reflejar las nuevas claves que proporciona XDM. Este proceso se facilita mediante el uso de la variable [Herramienta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) ese Audience Manager ha creado.

## Uso en el reenvío de eventos

Si tiene [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) habilitada y está utilizando `appmeasurement.js` y `visitor.js`, puede mantener habilitada la función de reenvío de eventos, lo que no provocará ningún problema. En el back-end, Adobe busca cualquier segmento AAM y lo agrega a la llamada a Analytics. Si la llamada a Analytics contiene estos segmentos, Analytics no llamará al Audience Manager para reenviar datos, por lo que no hay ninguna recopilación de datos doble. Tampoco hay necesidad de indicio de ubicación al utilizar el SDK web, ya que se llaman los mismos puntos finales de segmentación en el servidor.
