---
title: Recuperando ID de Experience Cloud
seo-title: SDK web de Adobe Experience Platform recuperando ID de Experience Cloud
description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
seo-description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 9%

---


# Identidad: recuperación del ID de Experience Cloud

El SDK web de Adobe Experience Platform aprovecha [Adobe Identity Service](../../identity-service/ecid.md). Esto garantiza que cada dispositivo tenga un identificador único que se mantenga en el dispositivo, de modo que la actividad entre páginas se pueda relacionar.

## Identidad de origen

El [!DNL Identity Service] almacena la identidad en una cookie en un dominio de origen. El [!DNL Identity Service] intenta establecer la cookie mediante un encabezado HTTP en el dominio. Si esto falla, el [!DNL Identity Service] volverá a configurar cookies mediante Javascript. Adobe recomienda configurar un CNAME para garantizar que las cookies no se vean restringidas por las restricciones de ITP del lado del cliente.

## Identidad de terceros

El [!DNL Identity Service] tiene la capacidad de sincronizar un ID con un dominio de terceros (demdex.net) para habilitar el seguimiento entre sitios. Cuando se habilita, la primera solicitud de un visitante (por ejemplo, alguien sin ECID) se realiza en demdex.net. Esto solo se realizará en los exploradores que lo permitan (por ejemplo, Chrome) y se controla mediante el `thirdPartyCookiesEnabled` parámetro en la configuración. Si desea deshabilitar esta función en conjunto, establezca `thirdPartyCookiesEnabled` en false.

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

Además, [!DNL Identity Service] le permite sincronizar sus propios identificadores con el ECID mediante el comando `syncIdentity` .

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
