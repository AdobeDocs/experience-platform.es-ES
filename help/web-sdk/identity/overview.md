---
title: Datos de identidad en Web SDK
description: Obtenga información sobre cómo recuperar y administrar Adobe Experience Cloud ID (ECID) mediante Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 3724c43090e37d21384e9dfe45e60ee2eec68a81
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# Datos de identidad en Web SDK

Adobe Experience Platform Web SDK usa [Adobe Experience Cloud ID (ECID)](../../identity-service/features/ecid.md) para hacer un seguimiento del comportamiento de los visitantes. Con [!DNL ECIDs], puede asegurarse de que cada dispositivo tenga un identificador único que pueda persistir en varias sesiones y que vincule todas las visitas que se producen durante las sesiones web y entre ellas a un dispositivo específico.

Este documento proporciona información general sobre cómo administrar [!DNL ECIDs] y [!DNL CORE IDs] mediante Web SDK.

## Seguimiento de ECID con Web SDK {#tracking-ecids-web-sdk}

Web SDK asigna y rastrea [!DNL ECIDs] mediante cookies, con varios métodos disponibles para configurar cómo se generan estas cookies.

Cuando un usuario nuevo llega a su sitio web, el [servicio de identidad de Adobe Experience Cloud](../../identity-service/home.md) intenta establecer una cookie de identificación de dispositivo para ese usuario.

* Para los visitantes nuevos, se genera un [!DNL ECID] que se devuelve en la primera respuesta del Edge Network Experience Platform.
* Para los visitantes habituales, el Edge Network recupera [!DNL ECID] de la cookie `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` y lo agrega a la carga de la solicitud.

Una vez establecida la cookie que contiene [!DNL ECID], cada solicitud posterior generada por Web SDK incluye [!DNL ECID] codificado en la cookie `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`.

Al utilizar cookies para identificar el dispositivo, tiene dos formas de interactuar con el Edge Network:

1. Cree un CNAME en su propio dominio que apunte a `adobedc.net`. Este método se conoce como [recopilación de datos de origen](#first-party).
1. Enviar datos directamente al dominio Edge Network `adobedc.net`. Este método se conoce como [recopilación de datos de terceros](#third-party).

Como se explica en las secciones siguientes, el método de recopilación de datos que decide utilizar tiene un impacto directo en la duración de las cookies en los exploradores.

## Seguimiento de ID de CORE mediante Web SDK {#tracking-coreid-web-sdk}

Cuando se usa Google Chrome con cookies de terceros habilitadas y no se ha establecido ninguna cookie `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`, la primera solicitud de Edge Network pasa por un dominio `demdex.net`, que establece una cookie demdex. Esta cookie contiene un [!DNL CORE ID]. Se trata de un identificador de usuario único, distinto del [!DNL ECID].

Según su implementación, es posible que desee [acceder a [!DNL CORE ID]](#retrieve-coreid).

### Recopilación de datos de origen {#first-party}

La recopilación de datos de origen implica la configuración de cookies a través de un `CNAME` en su propio dominio que señala a `adobedc.net`.

Aunque los exploradores han tratado durante mucho tiempo las cookies configuradas por `CNAME` extremos de manera similar a las establecidas por los extremos propiedad del sitio, los cambios recientes implementados por los exploradores han creado una distinción en la forma en que se administran las cookies de `CNAME`. Aunque no hay exploradores que bloqueen las cookies de origen `CNAME` de forma predeterminada, algunos restringen la duración de las cookies configuradas con un `CNAME` a solo siete días.

### Recopilación de datos de terceros {#third-party}

La recopilación de datos de terceros implica el envío de datos directamente al dominio Edge Network `adobedc.net`.

En los últimos años, los navegadores web se han vuelto cada vez más restrictivos en el manejo de cookies configuradas por terceros. Algunos exploradores bloquean las cookies de terceros de forma predeterminada. Si utiliza cookies de terceros para identificar a los visitantes del sitio, la duración de dichas cookies es casi siempre más corta que la que estaría disponible de otro modo utilizando cookies de origen en su lugar. A veces, una cookie de terceros caduca en tan solo siete días.

Además, al utilizar la recopilación de datos de terceros, algunos bloqueadores de anuncios restringen el tráfico a los extremos de recopilación de datos de Adobe por completo.

### Efectos de la duración de las cookies en las aplicaciones de Adobe Experience Cloud {#lifespans}

Independientemente de si elige la recopilación de datos de origen o de terceros, el tiempo que una cookie puede persistir tiene un impacto directo en los recuentos de visitantes en [Adobe Analytics](https://experienceleague.adobe.com/es/docs/analytics) y [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/customer-journey-analytics). Además, los usuarios finales pueden experimentar experiencias de personalización incoherentes cuando se usan [Adobe Target](https://experienceleague.adobe.com/es/docs/target) o [Offer decisioning](https://experienceleague.adobe.com/es/docs/target/using/integrate/ajo/offer-decision) en el sitio.

Por ejemplo, considere una situación en la que ha creado una experiencia de personalización que promociona cualquier elemento a la página principal si un usuario lo ha visto tres veces en los últimos siete días.

Si un usuario final visita el sitio tres veces en una semana y luego no regresa al sitio durante siete días, ese usuario podría considerarse un nuevo usuario cuando vuelva al sitio porque una política de explorador puede haber eliminado sus cookies (según el explorador que estuviera utilizando cuando visitó el sitio). Si esto sucede, la herramienta Analytics trata al visitante como un nuevo usuario aunque haya visitado el sitio hace poco más de siete días. Además, cualquier esfuerzo por personalizar la experiencia para el usuario comienza de nuevo.

### ID de dispositivos de origen (FPID) {#fpid}

Para tener en cuenta los efectos de la duración de las cookies como se describe más arriba, puede elegir establecer y administrar sus propios identificadores de dispositivo en su lugar. Consulte la guía de [ID de dispositivos de origen](./first-party-device-ids.md) para obtener más información.

## Recupere el ECID y la región del usuario actual {#retrieve-ecid}

Según su caso de uso, puede acceder a [!DNL ECID] de dos formas:

* [Recupere [!DNL ECID] mediante la preparación de datos para la recopilación de datos](#retrieve-ecid-data-prep): este es el método recomendado que debe utilizar.
* [Recupere  [!DNL ECID] a través del comando `getIdentity()`](#retrieve-ecid-getidentity): Utilice este método únicamente cuando necesite la información de [!DNL ECID] en el lado del cliente.

### Recuperar [!DNL ECID] mediante la preparación de datos para la recopilación de datos {#retrieve-ecid-data-prep}

Use la [preparación de datos para la recopilación de datos](../../datastreams/data-prep.md) para asignar [!DNL ECID] a un campo de [!DNL XDM]. Esta es la forma recomendada de obtener acceso a [!DNL ECID].

Para ello, establezca el campo de origen en la siguiente ruta:

```js
xdm.identityMap.ECID[0].id
```

A continuación, establezca el campo de destino en una ruta XDM donde el campo sea del tipo `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Recuperar [!DNL ECID] mediante el comando `getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Solamente debe recuperar el ECID a través del comando `getIdentity()` si necesita el [!DNL ECID] en el lado del cliente. Si solo desea asignar el ECID a un campo XDM, utilice [Preparación de datos para la recopilación de datos](#retrieve-ecid-data-prep) en su lugar.

Para recuperar el ECID único del visitante actual, use el comando `getIdentity`. Para los visitantes nuevos que aún no tienen un [!DNL ECID], este comando genera un nuevo [!DNL ECID]. `getIdentity` también devuelve el ID de región del visitante.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el ID de [!DNL Experience Cloud] o necesitan una sugerencia de ubicación para Adobe Audience Manager. No se utiliza en una implementación estándar.

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

## Recuperar el CORE ID del usuario actual {#retrieve-coreid}

Para recuperar el CORE ID de un usuario, puede utilizar el comando [`getIdentity()`](../commands/getidentity.md), como se muestra a continuación.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## Usando `identityMap` {#using-identitymap}

Con un campo XDM [`identityMap`](../../xdm/schema/composition.md#identityMap), puede identificar un dispositivo o usuario con varias identidades, establecer su estado de autenticación y decidir qué identificador se considera el principal. Si no se ha establecido ningún identificador como `primary`, el valor predeterminado principal es `ECID`.

`identityMap` campos se han actualizado mediante el comando `sentEvent`.

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
>El Adobe recomienda enviar áreas de nombres que representen a una persona, como `CRMID`, como identidad principal.


Cada propiedad de `identityMap` representa identidades que pertenecen a un [área de nombres de identidad](../../identity-service/features/namespaces.md) en particular. El nombre de propiedad debe ser el símbolo del área de nombres de identidad, que se puede encontrar en la interfaz de usuario de Adobe Experience Platform en &quot;[!UICONTROL Identities]&quot;. El valor de la propiedad debe ser una matriz de identidades pertenecientes a ese área de nombres de identidad.

>[!IMPORTANT]
>
>El identificador de área de nombres pasado en `identityMap` distingue entre mayúsculas y minúsculas. Asegúrese de utilizar el ID de área de nombres correcto para evitar una recopilación de datos incompleta.

Cada objeto de identidad de la matriz de identidades contiene las siguientes propiedades:

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | **(Obligatorio)** El identificador que desea establecer para el área de nombres determinada. |
| `authenticatedState` | Cadena | **(obligatorio)** El estado de autenticación del ID. Los valores posibles son `ambiguous`, `authenticated` y `loggedOut`. |
| `primary` | Booleano | Determina si esta identidad debe utilizarse como fragmento principal en el perfil. De forma predeterminada, el ECID se establece como identificador principal del usuario. Si se omite, el valor predeterminado es `false`. |

El uso del campo `identityMap` para identificar dispositivos o usuarios lleva al mismo resultado que el uso del método [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=es) desde [!DNL ID Service API]. Consulte la [documentación de la API del servicio de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=es) para obtener más información.

## Migración de la API de visitante a ECID {#migrating-visitor-api-ecid}

Al migrar desde la API de visitante, también puede migrar las cookies AMCV existentes. Para habilitar la migración de ECID, establezca el parámetro `idMigrationEnabled` en la configuración. La migración de ID habilita los siguientes casos de uso:

* Cuando algunas páginas de un dominio utilizan la API de visitante y otras páginas utilizan este SDK. Para admitir este caso, SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. Además, SDK escribe cookies AMCV de modo que, si el ECID se obtiene primero en una página instrumentada con SDK, las páginas posteriores instrumentadas con la API de visitante tengan el mismo ECID.
* Cuando Adobe Experience Platform Web SDK está configurado en una página que también tiene API de visitante. Para admitir este caso, si no se establece la cookie AMCV, SDK busca la API de visitante en la página y la llama para obtener el ECID.
* Cuando todo el sitio utiliza Adobe Experience Platform Web SDK y no tiene API de visitante, resulta útil migrar los ECID para que se conserve la información del visitante devuelta. Una vez que SDK se implementa con `idMigrationEnabled` durante un tiempo para que se migren la mayoría de las cookies de los visitantes, la configuración se puede desactivar.

### Actualización de características para la migración

Cuando se envían datos con formato XDM a Audience Manager, estos datos deben convertirse en señales al migrar. Las características deben actualizarse para reflejar las nuevas claves que proporciona XDM. Este proceso es más fácil gracias a la [herramienta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=es#getting-started-with-bulk-management) que el Audience Manager ha creado.

## Uso en el reenvío de eventos

Si actualmente tiene habilitado [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) y usa `appmeasurement.js` y `visitor.js`, puede mantener habilitada la característica de reenvío de eventos y esto no causará ningún problema. En el back-end, el Adobe AAM recupera cualquier segmento de y lo añade a la llamada a Analytics. Si la llamada a Analytics contiene esos segmentos, Analytics no llamará al Audience Manager para reenviar ningún dato, por lo que no hay ninguna recopilación de datos doble. Tampoco es necesario utilizar Location Hint al utilizar Web SDK, ya que se llama a los mismos extremos de segmentación en el backend.
