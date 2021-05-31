---
title: Recuperación de ID de Experience Cloud mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo recuperar Adobe Experience Cloud ID (ECID) mediante el SDK web de Adobe Experience Platform.
seo-description: Obtenga información sobre cómo obtener el Adobe Experience Cloud Id.
keywords: Identidad;Identidad de origen;Servicio de identidad;Identidad de terceros;Migración de ID;ID de visitante;identidad de terceros;Cookies de tercerosEnabled;idMigrationEnabled;getIdentity;Sincronización de identidades;syncIdentity;sendEvent;identityMap;principal;ecid;espacio de nombres;id de área de nombres;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# Recuperar Adobe Experience Cloud ID

El SDK web de Adobe Experience Platform aprovecha el [servicio de identidad de Adobe](../../identity-service/ecid.md). Esto garantiza que cada dispositivo tenga un identificador único que se mantenga en el dispositivo, de modo que la actividad entre páginas se pueda vincular.

## Identidad de origen

El [!DNL Identity Service] almacena la identidad en una cookie en un dominio de origen. El [!DNL Identity Service] intenta establecer la cookie mediante un encabezado HTTP en el dominio. Si esto falla, [!DNL Identity Service] volverá a configurar las cookies a través de Javascript. Adobe recomienda configurar un CNAME para garantizar que las cookies no se vean restringidas por las restricciones ITP del lado del cliente.

## Identidad de terceros

El [!DNL Identity Service] tiene la capacidad de sincronizar un ID con un dominio de terceros (demdex.net) para habilitar el seguimiento entre sitios. Cuando esto está habilitado, la primera solicitud para un visitante (por ejemplo, alguien sin ECID) se realiza en demdex.net. Esto solo se hará en exploradores que lo permitan (como Chrome) y está controlado por el parámetro `thirdPartyCookiesEnabled` en la configuración. Si desea deshabilitar esta función al mismo tiempo, establezca `thirdPartyCookiesEnabled` en false.

## Migración de ID

Al migrar desde la API de visitante, también puede migrar las cookies AMCV existentes. Para habilitar la migración de ECID, configure el parámetro `idMigrationEnabled` en la configuración. La migración de ID habilita los siguientes casos de uso:

* Cuando algunas páginas de un dominio utilizan la API de visitante y otras páginas utilizan este SDK. Para admitir este caso, el SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. Además, el SDK escribe cookies AMCV de modo que si el ECID se obtiene primero en una página instrumentada con el SDK, las páginas posteriores instrumentadas con la API de visitante tendrán el mismo ECID.
* Cuando el SDK web de Adobe Experience Platform se configura en una página que también tiene la API de visitante. Para admitir este caso, si no se establece la cookie AMCV, el SDK busca la API de visitante en la página y la llama para obtener el ECID.
* Cuando todo el sitio utiliza el SDK web de Adobe Experience Platform y no tiene la API de visitante, resulta útil migrar los ECID para conservar la información de visitante de retorno. Después de que el SDK se implemente con `idMigrationEnabled` durante un periodo de tiempo para que se migren la mayoría de las cookies del visitante, la configuración se puede desactivar.

## Actualización de características para la migración

Cuando se envían datos con formato XDM al Audience Manager, estos datos deben convertirse en señales al migrar. Los rasgos deberán actualizarse para reflejar las nuevas claves que proporciona XDM. Este proceso se facilita mediante el uso de la [herramienta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que el Audience Manager ha creado.

## Reenvío del lado del servidor

Si actualmente tiene habilitado el reenvío del lado del servidor y está utilizando `appmeasurement.js`. y `visitor.js` puede mantener habilitada la función de reenvío del lado del servidor, lo que no provocará ningún problema. En el servidor, Adobe busca cualquier segmento de AAM y lo agrega a la llamada de Analytics. Si la llamada a Analytics contiene estos segmentos, Analytics no llamará al Audience Manager para reenviar datos, por lo que no hay ninguna recopilación de datos doble. Tampoco hay necesidad de indicio de ubicación al utilizar el SDK web, ya que se llaman los mismos puntos finales de segmentación en el servidor.

## Recuperación del ID de visitante y el ID de región

Si desea utilizar el ID de visitante único, utilice el comando `getIdentity`. `getIdentity` devuelve el ECID existente para el visitante actual. Para los visitantes nuevos que aún no tienen un ECID, este comando genera un nuevo ECID. `getIdentity` también devuelve el ID de región del visitante. Consulte la [Guía del usuario de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) para obtener más información.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el ID [!DNL Experience Cloud] o necesitan la sugerencia de ubicación de Adobe Audience Manager. No se utiliza en una implementación estándar.

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

## Sincronización de identidades

>[!NOTE]
>
>El método `syncIdentity` se ha eliminado en la versión 2.1.0, además de la función de hash. Si utiliza la versión 2.1.0 o posterior y desea sincronizar identidades, puede enviarlas directamente en la opción `xdm` del comando `sendEvent`, en el campo `identityMap`.

Además, el [!DNL Identity Service] permite sincronizar sus propios identificadores con el ECID mediante el comando `syncIdentity`.

>[!NOTE]
>
>Se recomienda pasar todas las identidades disponibles en cada comando `sendEvent`. Esto desbloquea una serie de casos de uso, incluida la personalización. Ahora que puede pasar esas identidades en el comando `sendEvent`, se pueden colocar directamente en la capa de datos.

La sincronización de identidades permite identificar un dispositivo o usuario que utiliza varias identidades, establecer su estado de autenticación y decidir qué identificador se considera el principal. Si no se ha establecido ningún identificador como `primary`, el valor predeterminado principal es `ECID`.

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

Cada propiedad dentro de `identityMap` representa identidades que pertenecen a un [área de nombres de identidad](../../identity-service/namespaces.md) particular. El nombre de la propiedad debe ser el símbolo del área de nombres de identidad, que puede encontrar en la interfaz de usuario de Adobe Experience Platform en &quot;[!UICONTROL Identities]&quot;. El valor de la propiedad debe ser una matriz de identidades pertenecientes a ese área de nombres de identidad.

Cada objeto de identidad de la matriz de identidades está estructurado de la siguiente manera:

### `id`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | ninguna |

Este es el ID que desea sincronizar para el área de nombres dada.

### `authenticationState`

| **Tipo** | **Requerido** | **Valor predeterminado** | **Valores posibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Cadena | Sí | ambiguo | ambiguo, autenticado y registradoOut |

El estado de autenticación del ID.

### `primary`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Determina si esta identidad debe utilizarse como fragmento principal en el perfil unificado. De forma predeterminada, el ECID se establece como identificador principal para el usuario.
