---
title: Solución de problemas de identidad en recopilación de datos
description: Diagnostique problemas de identidad comunes en las implementaciones de Web SDK, como inflación de visitantes, incoherencias de ECID, conflictos de cookies y problemas de FPID.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Solución de problemas de identidad en recopilación de datos

Los problemas de identidad suelen aparecer como síntomas en los informes descendentes (recuentos de visitantes inflados, perfiles fragmentados o personalización interrumpida) en lugar de como errores en la propia implementación. Esta página le ayuda a diagnosticar y resolver los problemas de identidad más comunes en las implementaciones de Web SDK. Para obtener información general sobre cómo funciona la identidad en la recopilación de datos, consulte [descripción general de la identidad](./overview.md).

## Inspeccionar valores de identidad {#inspect-identity}

Antes de solucionar un problema específico, recupere los valores de identidad actuales que utiliza Web SDK. Utilice el comando [`getIdentity`](/help/collection/js/commands/getidentity.md) para ver el ECID y otras señales de identidad:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

También puede inspeccionar los valores de identidad en las herramientas para desarrolladores del explorador:

1. Abra la ficha **Aplicación** (Chrome/Edge) o **Almacenamiento** (Firefox/Safari).
2. Busque cookies con el prefijo `kndctr_` en su dominio. La cookie `kndctr_<ORG_ID>_AdobeOrg_identity` contiene el ECID.
3. Abra la ficha **Red** y busque una solicitud `interact` o `collect` a Edge Network. Inspeccione la carga útil de solicitud para `identityMap` y la carga útil de respuesta para los identificadores de identidad.

## Problemas comunes {#common-issues}

+++**Inflación en el recuento de visitantes**

**Síntoma**: los informes de Analytics muestran más visitantes únicos de lo esperado o la misma persona aparece como varios visitantes en varias sesiones.

**Causas posibles**:

| Causa | Cómo identificar | Resolución |
| --- | --- | --- |
| Duración corta de la cookie | Compruebe la caducidad de `kndctr_` cookies en el explorador. Si caducan en 7 días o menos, es probable que las directivas del explorador restrinjan la duración de la cookie. | Implemente [ID de dispositivos de origen (FPID)](./fpid.md) establecidos desde un servidor mediante un registro A/AAAA de DNS para prolongar la persistencia de las cookies. |
| Falta FPID en la primera solicitud | Inspeccione la primera solicitud de Edge Network al cargar la página. Si no hay ninguna cookie FPID presente, Edge Network genera un nuevo ECID. Si el FPID se establece después de la primera solicitud, el ECID generado en esa primera solicitud quedará huérfano. | Establezca la cookie FPID antes de que Web SDK envíe su primera solicitud. Ver [Cuándo se establece la cookie](./fpid.md#when-to-set-cookie). |
| `orgId` no coinciden entre dominios | Compare el valor de configuración de `orgId` entre sus dominios. Los valores no coincidentes causan ámbitos de identidad independientes. | Use el mismo [`orgId`](/help/collection/js/commands/configure/orgid.md) en todos los dominios de la organización. |
| Titular de consentimiento que elimina las cookies | Si la implementación de consentimiento borra todas las cookies antes de que se conceda el consentimiento y, a continuación, se inicializa el SDK web, se genera un nuevo ECID. | Configure su banner de consentimiento para conservar las cookies de `kndctr_` o retrasar la inicialización de Web SDK hasta que se establezca el consentimiento. Ver también [Consentimiento e identidad](./consent.md). |
| Cookies FPID configuradas por JavaScript | Las cookies configuradas con `document.cookie` están sujetas a restricciones del explorador (ITP, ETP) que limitan su duración, a veces a tan solo 24 horas. | Establezca cookies FPID desde el servidor mediante un registro A/AAAA DNS, no desde JavaScript. |

+++

+++**ECID cambia inesperadamente entre páginas**

**Síntoma**: El ECID es diferente en páginas diferentes del mismo dominio o cambia al cargar cada página.

**Pasos de diagnóstico**:

1. Confirme que la cookie de identidad `kndctr_` esté presente en ambas páginas. Si falta en una página, compruebe que Web SDK esté configurado en esa página.
2. Compruebe que el dominio de la cookie está configurado con suficiente amplitud. Una cookie configurada en `shop.example.com` no está disponible en `www.example.com`. Asegúrese de que la recopilación de origen y la infraestructura de configuración de cookies utilizan el mismo ámbito de dominio.
3. Compruebe si JavaScript borra las cookies durante la navegación (por ejemplo, las herramientas de privacidad o los scripts agresivos de consentimiento de cookies).
4. Si utiliza una aplicación de una sola página, compruebe que Web SDK se haya configurado una vez al inicializar la aplicación, no se haya reiniciado con cada cambio de ruta. El reinicio puede generar un nuevo ECID.

+++

+++**FPID no está inicializando el ECID**

**Síntoma**: ha establecido una cookie FPID, pero `getIdentity` devuelve un ECID que no es coherente en todas las visitas o el FPID no aparece en las cargas de solicitud de Edge Network.

**Pasos de diagnóstico**:

1. **Compruebe el formato de la cookie FPID**: el FPID debe ser un [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122) válido. Abra las herramientas para desarrolladores del explorador, busque la cookie FPID y confirme que el valor coincide con el patrón `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`.
2. **Compruebe el nombre de la cookie en el conjunto de datos**: Si utiliza el [método de cookie del conjunto de datos](./fpid.md#setting-cookie-datastreams), el nombre de la cookie configurado en el conjunto de datos debe coincidir exactamente con el nombre de la cookie que establece su servidor.
3. **Confirme que la cookie se envía en la solicitud**: en la pestaña Red, inspeccione el encabezado `Cookie` de la solicitud Edge Network. Se debe incluir la cookie FPID.
4. **Comprobar prioridad de identidad**: Si un ECID existente ya está almacenado en una cookie `kndctr_`, tiene prioridad sobre el FPID. El FPID solo siembra un nuevo ECID cuando no hay ningún ECID existente. Consulte [Cómo funcionan los FPID](./fpid.md#how-fpids-work) para ver el orden de prioridad completo.
5. **Valide el CNAME**: Si utiliza el método de cookie de secuencia de datos, confirme que el CNAME de la colección de origen está configurado correctamente y que las solicitudes se enrutan a través de él.

+++

+++**La identidad entre dominios no funciona**

**Síntoma**: Un visitante que hace clic de un dominio a otro se trata como un visitante nuevo en el dominio de destino.

**Pasos de diagnóstico**:

1. **Compruebe la dirección URL**: inspeccione la dirección URL de destino cuando el visitante haga clic en el vínculo. Debe contener un parámetro de cadena de consulta `adobe_mc`. Si falta el parámetro, el dominio de origen no lo anexa. Consulte [Implementar el uso compartido entre dominios](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Comprobar el tiempo**: El parámetro `adobe_mc` caduca a los cinco minutos. Si la página de destino tarda demasiado en cargarse (por ejemplo, debido a redirecciones o a una red lenta), el parámetro puede caducar antes de que Web SDK pueda leerlo.
3. **Verificar `orgId` coincidencia**: ambos dominios deben usar el mismo [`orgId`](/help/collection/js/commands/configure/orgid.md). Los ID de organización no coincidentes hacen que el dominio de destino rechace la identidad entregada.
4. **Confirmar que Web SDK está en el destino**: la página de destino debe tener Web SDK instalado y configurado. Sin él, se omite el parámetro `adobe_mc`.
5. **Comprobar la eliminación de direcciones URL**: algunos servicios de redirección, CDN o lógica del lado del servidor eliminan parámetros de cadena de consulta desconocidos. Compruebe que `adobe_mc` sobrevive a cualquier redirección intermedia entre las páginas de origen y destino.

+++

+++**Error en el traspaso de identidad de móvil a web**

**Síntoma**: Un visitante que se inicia en la aplicación móvil y abre un explorador WebView o móvil se trata como un visitante nuevo en el lado web.

**Pasos de diagnóstico**:

1. **Compruebe la dirección URL**: registre la dirección URL que se pasa al WebView. Debe contener un parámetro `adobe_mc` generado por [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **Comprobar versiones de SDK**: la extensión de Mobile Identity for Edge Network debe ser la versión 1.1.0 o posterior, y Web SDK debe ser la versión 2.11.0 o posterior.
3. **Comprobar la sincronización**: al igual que el uso compartido entre dominios, el parámetro `adobe_mc` caduca pasados cinco minutos. Asegúrese de que WebView se carga rápidamente después de crear la dirección URL.
4. **Confirmar `orgId` coincidencia**: El identificador de organización de Experience Cloud debe ser el mismo en las configuraciones de SDK móvil y SDK web.

+++
