---
title: Datos de identidad en el SDK web de Platform
description: Obtenga información sobre cómo recuperar y administrar Adobe Experience Cloud ID (ECID) mediante el SDK web de Adobe Experience Platform.
keywords: Identidad;Identidad de origen;Servicio de identidad;Identidad de terceros;Migración de ID;ID de visitante;identidad de terceros;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Sincronizando identidades;syncIdentity;sendEvent;identityMap;primary;ecid;Área de nombres de identidad;id de área de nombres;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 1%

---

# Datos de identidad en el SDK web de Platform

El SDK web de Adobe Experience Platform aprovecha [Adobe Experience Cloud ID (ECID)](../../identity-service/ecid.md) para realizar un seguimiento del comportamiento de los visitantes. Con los ECID, se puede garantizar que cada dispositivo tenga un identificador único que pueda persistir en varias sesiones y que vincule todas las visitas que se producen durante las sesiones web y entre ellas a un dispositivo específico.

Este documento proporciona información general sobre cómo administrar los ECID mediante el SDK web de Platform.

## Seguimiento de ECID con el SDK

El SDK web de Platform asigna y rastrea los ECID mediante el uso de cookies, con varios métodos disponibles para configurar cómo se generan estas cookies.

Cuando un usuario nuevo llega a su sitio web, el servicio de identidad de Adobe Experience Cloud intenta establecer una cookie de identificación de dispositivo para ese usuario. Para los visitantes que acceden al sitio por primera vez, se genera un ECID que se devuelve en la primera respuesta de Adobe Experience Platform Edge Network. Para visitantes repetidos, el ECID se recupera del `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` y se agrega a la carga útil mediante la red perimetral.

Una vez establecida la cookie que contiene el ECID, cada solicitud posterior generada por el SDK web incluirá un ECID codificado en la variable `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Al utilizar cookies para la identificación del dispositivo, tiene dos opciones para interactuar con la red perimetral:

1. Enviar datos directamente al dominio de red perimetral `adobedc.net`. Este método se denomina [recopilación de datos de terceros](#third-party).
1. Cree un CNAME en su propio dominio que apunte a `adobedc.net`. Este método se denomina [recopilación de datos de origen](#first-party).

Como se explica en las secciones siguientes, el método de recopilación de datos que decide utilizar tiene un impacto directo en la duración de las cookies en los exploradores.

### Recopilación de datos de terceros {#third-party}

La recopilación de datos de terceros implica el envío de datos directamente al dominio de red perimetral `adobedc.net`.

En los últimos años, los navegadores web se han vuelto cada vez más restrictivos en el manejo de cookies configuradas por terceros. Algunos exploradores bloquean las cookies de terceros de forma predeterminada. Si utiliza cookies de terceros para identificar a los visitantes del sitio, la duración de dichas cookies es casi siempre más corta que la que estaría disponible de otro modo utilizando cookies de origen en su lugar. En algunos casos, una cookie de terceros caducará en tan solo siete días.

Además, cuando se utiliza la recopilación de datos de terceros, algunos bloqueadores de anuncios restringen el tráfico a los extremos de recopilación de datos de Adobe por completo.

### Recopilación de datos de origen {#first-party}

La recopilación de datos de origen implica la configuración de cookies a través de un CNAME en su propio dominio que señala a `adobedc.net`.

Aunque los exploradores han tratado durante mucho tiempo las cookies configuradas por los extremos CNAME de manera similar a las establecidas por los extremos propiedad del sitio, los cambios recientes implementados por los exploradores han creado una distinción en la forma en que se administran las cookies CNAME. Aunque actualmente no hay exploradores que bloqueen las cookies CNAME de origen de forma predeterminada, algunos restringen la duración de las cookies configuradas con un CNAME a solo siete días.

### Efectos de la duración de las cookies en las aplicaciones de Adobe Experience Cloud {#lifespans}

Independientemente de si elige la recopilación de datos de origen o de terceros, el tiempo que una cookie puede persistir tiene un impacto directo en el recuento de visitantes en Adobe Analytics y Customer Journey Analytics. Además, es posible que los usuarios finales experimenten experiencias de personalización incoherentes cuando se utiliza Adobe Target o Offer Decisioning en el sitio.

Por ejemplo, considere una situación en la que ha creado una experiencia de personalización que promocionará cualquier elemento a la página principal si un usuario lo ha visto tres veces en los últimos siete días.

Si un usuario final visita tres veces en una semana y luego no regresa al sitio durante siete días, ese usuario podría considerarse un nuevo usuario cuando regresa al sitio porque sus cookies pueden haber sido eliminadas por una política del explorador (según el explorador que estuviera utilizando cuando visitó el sitio). Si esto sucede, la herramienta Analytics tratará al visitante como un nuevo usuario aunque haya visitado el sitio hace poco más de siete días. Además, cualquier esfuerzo por personalizar la experiencia del usuario volverá a comenzar.

### ID de dispositivos de origen

Para tener en cuenta los efectos de la duración de las cookies como se describe más arriba, puede optar por establecer y administrar sus propios identificadores de dispositivo en su lugar. Consulte la guía de [ID de dispositivos de origen](./first-party-device-ids.md) para obtener más información.

## Recuperación del ECID y la región para el usuario actual

Para recuperar el ECID único del visitante actual, utilice el `getIdentity` comando. Para los visitantes nuevos que aún no tienen un ECID, este comando genera un nuevo ECID. `getIdentity` también devuelve el ID de región del visitante.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el [!DNL Experience Cloud] ID o necesita una sugerencia de ubicación para Adobe Audience Manager. No se utiliza en una implementación estándar.

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

## Uso de `identityMap`

Uso de un XDM [`identityMap` campo](../../xdm/schema/composition.md#identityMap), puede identificar un dispositivo o usuario con varias identidades, establecer su estado de autenticación y decidir qué identificador se considera el principal. Si no se ha establecido ningún identificador como `primary`, el valor predeterminado principal es `ECID`.

`identityMap` Los campos de se actualizan mediante la variable `sentEvent` comando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe recomienda enviar áreas de nombres que representen a una persona, como `CRMID`, como identidad principal.


Cada propiedad dentro de `identityMap` representa identidades que pertenecen a un [área de nombres de identidad](../../identity-service/namespaces.md). El nombre de la propiedad debe ser el símbolo del área de nombres de identidad, que se puede encontrar en la interfaz de usuario de Adobe Experience Platform, en &quot;[!UICONTROL Identidades]&quot;. El valor de la propiedad debe ser una matriz de identidades pertenecientes a ese área de nombres de identidad.

>[!IMPORTANT]
>
>El ID de área de nombres pasado en `identityMap` distingue entre mayúsculas y minúsculas. Asegúrese de utilizar el ID de área de nombres correcto para evitar una recopilación de datos incompleta.

Cada objeto de identidad de la matriz de identidades contiene las siguientes propiedades:

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | **(Obligatorio)** El ID que desea establecer para el área de nombres determinada. |
| `authenticationState` | Cadena | **(Obligatorio)** El estado de autenticación del ID. Los valores posibles son `ambiguous`, `authenticated`, y `loggedOut`. |
| `primary` | Booleano | Determina si esta identidad debe utilizarse como fragmento principal en el perfil. De forma predeterminada, el ECID se establece como identificador principal del usuario. Si se omite, el valor predeterminado es `false`. |

Uso del `identityMap` para identificar dispositivos o usuarios lleva al mismo resultado que usar el campo [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=es) método desde el [!DNL ID Service API]. Consulte la [Documentación de API del servicio de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) para obtener más información.

## Migración de la API de visitante a ECID

Al migrar desde la API de visitante, también puede migrar las cookies AMCV existentes. Para habilitar la migración de ECID, establezca el `idMigrationEnabled` en la configuración de. La migración de ID habilita los siguientes casos de uso:

* Cuando algunas páginas de un dominio utilizan la API de visitante y otras páginas utilizan este SDK. Para admitir este caso, el SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. Además, el SDK escribe cookies AMCV de modo que, si el ECID se obtiene primero en una página instrumentada con el SDK, las páginas posteriores instrumentadas con la API de visitante tengan el mismo ECID.
* Cuando el SDK web de Adobe Experience Platform está configurado en una página que también tiene API de visitante. Para admitir este caso, si no se establece la cookie AMCV, el SDK busca la API de visitante en la página y la llama para obtener el ECID.
* Cuando todo el sitio utiliza el SDK web de Adobe Experience Platform y no tiene API de visitante, resulta útil migrar los ECID para que se conserve la información del visitante de retorno. Después de implementar el SDK con `idMigrationEnabled` durante un tiempo para que se migren la mayoría de las cookies del visitante, la configuración se puede desactivar.

### Actualización de características para la migración

Cuando se envían datos con formato XDM al Audience Manager, estos datos deberán convertirse en señales al migrar. Sus características deberán actualizarse para reflejar las nuevas claves que proporciona XDM. Este proceso es más fácil gracias al uso del [Herramienta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que el Audience Manager ha creado.

## Uso en el reenvío de eventos

Si actualmente tiene [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) habilitado y está utilizando `appmeasurement.js` y `visitor.js`No obstante, puede mantener activada la función de reenvío de eventos y esto no causará ningún problema. En el back-end, el Adobe AAM recupera cualquier segmento de y lo añade a la llamada a Analytics. Si la llamada a Analytics contiene esos segmentos, Analytics no llamará al Audience Manager para reenviar ningún dato, por lo que no hay ninguna recopilación de datos doble. Tampoco es necesario utilizar una sugerencia de ubicación al utilizar el SDK web, ya que se llaman los mismos extremos de segmentación en el backend.
