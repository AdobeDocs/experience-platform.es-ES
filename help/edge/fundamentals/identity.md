---
title: Recuperando ID de Experience Cloud
seo-title: Adobe Experience Platform Web SDK Recuperación de ID de Experience Cloud
description: Obtenga información sobre cómo obtener el Adobe Experience Cloud Id.
seo-description: Obtenga información sobre cómo obtener el Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: d2870df230811486c09ae29bf9f600beb24fe4f8
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---


# Identidad: recuperación del ID de Experience Cloud

Adobe Experience Platform [!DNL Web SDK] aprovecha el servicio [de identidad de](../../identity-service/ecid.md)Adobe. Esto garantiza que cada dispositivo tenga un identificador único que se mantenga en el dispositivo, de modo que la actividad entre páginas se pueda relacionar.

## Identidad de origen

El [!DNL Identity Service] almacena la identidad en una cookie en un dominio de origen. El [!DNL Identity Service] intenta establecer la cookie mediante un encabezado HTTP en el dominio. Si esto falla, el [!DNL Identity Service] volverá a configurar cookies mediante Javascript. Adobe recomienda configurar un CNAME para garantizar que las cookies no se vean restringidas por las restricciones de ITP del lado del cliente.

## Identidad de terceros

El [!DNL Identity Service] tiene la capacidad de sincronizar un ID con un dominio de terceros (demdex.net) para habilitar el seguimiento entre sitios. Cuando se habilita, la primera solicitud de un visitante (por ejemplo, alguien sin ECID) se realiza en demdex.net. Esto solo se realizará en los exploradores que lo permitan (por ejemplo, Chrome) y se controla mediante el `thirdPartyCookiesEnabled` parámetro en la configuración. Si desea deshabilitar esta función en conjunto, establezca `thirdPartyCookiesEnabled` en false.

## Migración de ID

Al migrar desde la API de Visitante, también puede migrar las cookies AMCV existentes. Para habilitar la migración ECID, establezca el `idMigrationEnabled` parámetro en la configuración. La migración de ID está configurada para habilitar algunos casos de uso:

* Cuando algunas páginas de un dominio utilizan la API de Visitante y otras páginas utilizan este SDK. Para admitir este caso, el SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. Además, el SDK escribe cookies AMCV de modo que si el ECID se obtiene primero en una página instrumentada con el SDK web de AEP, las páginas subsiguientes instrumentadas con la API de Visitante tengan el mismo ECID.
* Cuando el SDK web de AEP está configurado en una página que también tiene API de Visitante. Para admitir este caso, si no se establece la cookie AMCV, el SDK busca la API de Visitante en la página y la llama para obtener el ECID.
* Cuando todo el sitio utiliza el SDK web de AEP y no tiene la API de Visitante, resulta útil migrar los ECID para conservar la información de visitante de retorno. Una vez que el SDK se haya implementado `idMigrationEnabled` durante un período de tiempo para migrar la mayoría de las cookies de visitante, la configuración se puede desactivar.

## Recuperación del ID de Visitante

Si desea utilizar este ID único, utilice el `getIdentity` comando. `getIdentity` devuelve el ECID existente para el visitante actual. Para los visitantes que no tienen un ECID todavía por primera vez, este comando genera un nuevo ECID.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el [!DNL Experience Cloud] ID. No se utiliza en una implementación estándar.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Sincronización de identidades

>[!NOTE]
>
>El `syncIdentity` método se ha eliminado en la versión 2.1.0, además de la función de hash. Si utiliza la versión 2.1.0 o posterior y desea sincronizar identidades, puede enviarlas directamente en la `xdm` opción del `sendEvent` comando, en el `identityMap` campo.

Además, [!DNL Identity Service] le permite sincronizar sus propios identificadores con el ECID mediante el comando `syncIdentity` .

>[!NOTE]
>
>Se recomienda encarecidamente pasar todas las identidades disponibles en cada `sendEvent` comando. Esto desbloquea una serie de casos de uso, incluida la personalización. Ahora que puede pasar esas identidades en el `sendEvent` comando, se pueden colocar directamente en el DataLayer.

La sincronización de identidades permite identificar un dispositivo o usuario con varias identidades, establecer su estado de autenticación y decidir qué identificador se considera el principal. Si no se ha establecido ningún identificador como `primary`, el valor predeterminado principal es el `ECID`.

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
})
```


### Opciones de sincronización de identidades

#### Símbolo de Área de nombres de identidad

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

La clave para el objeto es el símbolo de Área de nombres [de](../../identity-service/namespaces.md) identidad. Puede encontrarlo en la interfaz de usuario de Adobe Experience Platform, en [!UICONTROL Identidades].

#### `id`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

Es el ID que desea sincronizar para la Área de nombres dada.

#### `authenticationState`

| **Tipo** | **Requerido** | **Valor predeterminado** | **Valores posibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Cadena | Sí | ambiguo | ambiguo, autenticado y registradoOut |

El estado de autenticación del ID.

#### `primary`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Determina si esta identidad debe utilizarse como fragmento principal en el perfil unificado. De forma predeterminada, el ECID se establece como identificador principal del usuario.

#### `hashEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Si se habilita, se hash la identidad mediante hash SHA256.
