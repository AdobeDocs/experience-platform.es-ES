---
title: Recuperación del ID de Experience Cloud
seo-title: SDK web de Adobe Experience Platform Recuperación de Experience Cloud ID
description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
seo-description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 9bd6feb767e39911097bbe15eb2c370d61d9842a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 7%

---


# (Beta) Recuperación de Experience Cloud ID

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

El SDK web de Adobe Experience Platform aprovecha el servicio [de identidad de](../../identity-service/ecid.md)Adobe. Esto garantiza que cada dispositivo tenga un identificador único que se mantenga en el dispositivo, de modo que la actividad entre páginas se pueda relacionar.

## Identidad de origen

El servicio de ID almacena la identidad en una cookie en un dominio de origen. Los servicios de ID intentan establecer la cookie mediante un encabezado HTTP en el dominio si esto falla, el servicio de ID volverá a configurar las cookies mediante JavaScript. Adobe recomienda configurar un CNAME para garantizar que las cookies no se vean restringidas por las restricciones de ITP del lado del cliente.

## Identidad de terceros

Los servicios de ID pueden sincronizar un ID con un dominio de terceros (demdex.net) para habilitar el seguimiento en todo el sitio. Cuando se habilita, la primera solicitud de un visitante (por ejemplo, alguien sin ECID) se realiza en demdex.net. Esto solo se realizará en los exploradores que lo permitan (por ejemplo, Chrome) y se controla mediante el `thirdPartyCookiesEnabled` parámetro en la configuración. Si desea deshabilitar esta función, defina `thirdPartyCookiesEnabled` en falso.

## Recuperación del ID de Visitante

Si desea utilizar este ID único, utilice el `getIdentity` comando. `getIdentity` devuelve el ECID existente para el visitante actual. Para los visitantes que no tienen un ECID todavía por primera vez, este comando genera un nuevo ECID.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el ID de Experience Cloud. No se utiliza en una implementación estándar.

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

Además, el servicio de identidad le permite sincronizar sus propios identificadores con el ECID mediante el `syncIdentity` comando.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Opciones de sincronización de identidades

#### Símbolo de Área de nombres de identidad

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

La clave para el objeto es el símbolo de Área de nombres [de](../../identity-service/namespaces.md) identidad. Puede encontrarlo en la interfaz de usuario de Adobe Experience Platform en Identidades.

#### `id`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Cadena | Sí | none |

Es el ID que desea sincronizar para la Área de nombres dada.

#### `primary`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Si esta identidad se utiliza como fragmento principal en el perfil unificado. De forma predeterminada, el ECID se establece como identificador principal del usuario.

#### `hashEnabled`

| **Tipo** | **Requerido** | **Valor predeterminado** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Si se habilita, se hash la identidad mediante hash SHA256.