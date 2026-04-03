---
title: idMigrationEnabled
description: Permite que Web SDK lea cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

La propiedad `idMigrationEnabled` permite que Web SDK lea cookies AMCV establecidas por implementaciones de Adobe Experience Cloud anteriores. Si su organización actualiza la implementación a Web SDK, esta configuración permite una transición más suave al servicio de Adobe Experience Cloud ID actual. Esta configuración es valiosa para que no observe un marcado aumento de visitantes únicos al actualizar a Web SDK.

Si su organización ejecuta una implementación nueva de Web SDK, habilitar esta configuración no tiene ningún impacto en la recopilación de datos ni en la identificación de visitantes. No hay inconvenientes en dejarlo habilitado para todas las implementaciones.

## Funcionamiento de la migración de identidad {#how-it-works}

La API de visitante almacena el Experience Cloud ID (ECID) en una cookie llamada `AMCV_<ORG_ID>`. Cuando `idMigrationEnabled` es `true` (el valor predeterminado), Web SDK lee automáticamente el ECID de la cookie AMCV y lo utiliza como identidad del visitante en la primera solicitud de Edge Network.

1. Un visitante llega en una página que ahora utiliza Web SDK en lugar de la API de visitante.
1. Web SDK busca una cookie de identidad `kndctr_` existente (su propio formato de cookie). Si no se encuentra ninguna, busca una cookie `AMCV_`.
1. Si se encuentra una cookie `AMCV_`, Web SDK extrae el ECID y lo utiliza para inicializar la identidad del visitante.
1. Web SDK establece una nueva cookie de identidad `kndctr_` con el mismo ECID.
1. En visitas posteriores, Web SDK usa directamente la cookie `kndctr_`. La cookie `AMCV_` ya no es necesaria.

Para que la migración funcione, Web SDK debe configurarse con el mismo [`orgId`](/help/collection/js/commands/configure/orgid.md) que la API de visitante utilizada y debe implementarse en el mismo dominio (o un subdominio del mismo dominio principal) donde se configuró la cookie AMCV.

## Escenarios de migración admitidos

La migración de ID admite los siguientes patrones de transición:

* **Algunas páginas siguen usando la API de visitante mientras que otras utilizan el Web SDK**: SDK lee las cookies AMCV existentes y escribe una nueva cookie con el ECID existente. También escribe cookies AMCV para que las páginas que siguen utilizando la API de visitante sigan reconociendo al mismo visitante.
* **Web SDK y la API de visitante están presentes en la misma página**: si no se ha establecido la cookie AMCV, SDK busca la API de visitante en la página y la utiliza para obtener el ECID.
* **El sitio se ha movido completamente al Web SDK**: puede dejar habilitada la migración durante un período de tiempo para que los visitantes existentes basados en AMCV mantengan la continuidad mientras se realizan las transiciones de las cookies.

>[!IMPORTANT]
>
>No cargue la API de visitante y el SDK web en la misma página al mismo tiempo, a menos que haya confirmado que la cookie AMCV ya está establecida. La ejecución de ambas bibliotecas en una sola página puede provocar condiciones de carrera en las que cada biblioteca intenta administrar la identidad de forma independiente, lo que podría generar ECID duplicados o en conflicto.

## Desactivación de la migración {#turn-off-migration}

Después de que todo el sitio se ejecute en Web SDK y ningún visitante lleve solamente una cookie `AMCV_` sin la cookie `kndctr_` correspondiente, puede deshabilitar de forma segura la migración de identidades estableciendo `idMigrationEnabled` en `false`. Se trata de una optimización de rendimiento menor y reduce el área de superficie de la lógica de identidad.

Como guía, espere hasta que la duración máxima de la cookie AMCV haya transcurrido después de migrar la última página. Si las cookies AMCV tienen una caducidad de dos años, espere dos años después de que la página final se haya transferido a Web SDK. En la práctica, la mayoría de las organizaciones desactivan la migración antes (después de unos meses) y aceptan una cantidad insignificante de inflación debido al pequeño número de visitantes que regresan por primera vez después de una larga ausencia.

## Actualizaciones de rasgos de Audience Manager

Cuando se envían datos con formato XDM a Audience Manager durante la migración, esos datos deben convertirse en señales. Las características deben actualizarse para reflejar las nuevas claves proporcionadas por XDM. Este proceso es más fácil gracias a la [herramienta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=es#getting-started-with-bulk-management).

## Migración de ID de terceros {#third-party-id}

Si la implementación de la API de visitante utilizó ID de terceros (la cookie `demdex.net`), Web SDK también puede migrarlos. Configure [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) a `true` en la configuración de Web SDK. Web SDK lee la cookie de Demdex existente e incluye la identidad de terceros en sus solicitudes de Edge Network, siguiendo el mismo patrón de migración que la cookie de AMCV.

## Validación {#validation}

Para comprobar que la migración de identidad funciona correctamente:

1. Abra una página que anteriormente usaba la API de visitante (ahora con Web SDK) en un explorador que tenga una cookie `AMCV_` existente.
2. En las herramientas para desarrolladores, compruebe que se ha establecido una cookie de identidad `kndctr_` y que ECID coincida con la de la cookie `AMCV_`.
3. Después de la implementación, compare los recuentos de visitantes únicos antes y después de la migración durante el mismo período de tiempo. Un pico significativo en visitantes únicos puede indicar que la migración no está llevando identidades hacia adelante.

>[!TIP]
>
>Use `getIdentity` para recuperar mediante programación el ECID para la comparación:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Configurar `idMigrationEnabled` {#configure}

Establezca el booleano `idMigrationEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `true`. Establezca esta propiedad si desea deshabilitar la capacidad de leer cookies AMCV establecidas por la API de visitante. La mayoría de las organizaciones no necesitan establecer esta propiedad.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Habilitar la migración de ID de visitantes con la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [opciones de configuración de identidad](/help/tags/extensions/client/web-sdk/configure/identity.md).
