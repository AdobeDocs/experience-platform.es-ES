---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general de la biblioteca JavaScript de privacidad de Adobe
topic-legacy: overview
description: La biblioteca JavaScript de privacidad de Adobe permite recuperar identidades de interesados para usarlas en Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 6%

---

# Resumen de la biblioteca JavaScript de privacidad de Adobe

Como encargado del tratamiento de datos, Adobe procesa los datos personales de acuerdo con los permisos e instrucciones de su empresa. Como responsable del tratamiento de datos, determinará qué datos personales Adobe trata y almacena en su nombre. Según la información que elija enviar a través de las soluciones de Adobe Experience Cloud, el Adobe puede almacenar información privada aplicable a regulaciones de privacidad como la [!DNL General Data Protection Regulation] (RGPD) y [!DNL California Consumer Privacy Act] (CCPA). Consulte el documento en [privacidad en Adobe Experience Cloud](https://www.adobe.com/es/privacy/marketing-cloud.html) para obtener más información sobre cómo las soluciones de Experience Cloud recopilan datos privados.

La variable **Biblioteca JavaScript de privacidad de Adobe** permite a los responsables del tratamiento de datos automatizar la recuperación de todas las identidades de interesados generadas por [!DNL Experience Cloud] soluciones para un dominio específico. Uso de la API proporcionada por [Adobe Experience Platform Privacy Service](home.md), estas identidades se pueden utilizar para crear solicitudes de acceso y eliminación de datos privados pertenecientes a esos interesados.

>[!NOTE]
>
>La variable [!DNL Privacy JS Library] normalmente solo necesita instalarse en páginas relacionadas con la privacidad y no es necesario que esté instalado en todas las páginas de un sitio web o dominio.

## Funciones

La variable [!DNL Privacy JS Library] proporciona varias funciones para administrar identidades en [!DNL Privacy Service]. Estas funciones solo se pueden utilizar para administrar las identidades almacenadas en el explorador para un visitante específico. No se pueden utilizar para enviar información a la variable [!DNL Experience Cloud Central Service] directamente.

La siguiente tabla describe las diferentes funciones que proporciona la biblioteca:

| Función | Descripción |
| --- | --- |
| `retrieveIdentities` | Devuelve una matriz de identidades coincidentes (`validIds`) recuperadas de [!DNL Privacy Service], así como una matriz de identidades que no se encontraron (`failedIds`). |
| `removeIdentities` | Quita cada identidad coincidente (válida) del explorador. Devuelve una matriz de identidades coincidentes (`validIds`), con cada identidad que contenga una `isDeletedClientSide` booleano que indica si se ha eliminado este ID. |
| `retrieveThenRemoveIdentities` | Recupera una matriz de identidades coincidentes (`validIds`) y, a continuación, elimina esas identidades del explorador. Aunque esta función es similar a `removeIdentities`, se recomienda utilizarlo cuando la solución de Adobe que está utilizando requiera una solicitud de acceso antes de poder eliminarla (por ejemplo, cuando se debe recuperar un identificador único antes de proporcionarlo en una solicitud de eliminación). |

>[!NOTE]
>
>`removeIdentities` y `retrieveThenRemoveIdentities` elimine únicamente las identidades del explorador para soluciones de Adobe específicas que las admitan. Por ejemplo, Adobe Audience Manager no elimina los ID de demdex que están almacenados en cookies de terceros, mientras que Adobe Target elimina todas las cookies que almacenan sus ID.

Dado que las tres funciones representan procesos asíncronos, cualquier identidad recuperada debe gestionarse mediante llamadas de retorno o promesas.


## Instalación

Para empezar a usar la variable [!DNL Privacy JS Library], debe instalarlo en el equipo mediante uno de los métodos siguientes:

* Instale utilizando npm ejecutando el siguiente comando: `npm install @adobe/adobe-privacy`
* Descargue desde [Repositorio de GitHub Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

También puede instalar la biblioteca a través de una extensión de etiqueta . Consulte la descripción general de la [Extensión de la etiqueta de privacidad de Adobe](../tags/extensions/client/privacy/overview.md) para obtener más información.

## Cree una instancia de [!DNL Privacy JS Library]

Todas las aplicaciones que utilizan la variable [!DNL Privacy JS Library] debe crear una instancia de `AdobePrivacy` , que debe configurarse en una solución de Adobe específica. Por ejemplo, una instancia de Adobe Analytics tendría un aspecto similar al siguiente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obtener una lista completa de los parámetros admitidos para las distintas soluciones de Adobe, consulte la sección del apéndice de [Parámetros de configuración de la solución Adobe](#adobe-solution-configuration-parameters).

## Ejemplos de código {#samples}

Los siguientes ejemplos de código muestran cómo usar el [!DNL Privacy JS Library] para varios escenarios comunes, siempre que no utilice etiquetas.

### Recuperar identidades

Este ejemplo muestra cómo recuperar una lista de identidades de [!DNL Experience Cloud].

#### JavaScript

El siguiente código define una función, `handleRetrievedIDs`, que se utilizará como llamada de retorno o promesa para gestionar las identidades recuperadas por `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variable | Descripción |
| --- | --- |
| `validIds` | Un objeto JSON que contiene todos los ID que se recuperaron correctamente. |
| `failedIDs` | Un objeto JSON que contiene todos los ID de los que no se recuperaron [!DNL Privacy Service], o no se encontraron. |

#### Resultado 

Si el código se ejecuta correctamente, `validIDs` se rellena con una lista de identidades recuperadas.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Eliminar identidades

Este ejemplo muestra cómo eliminar una lista de identidades del explorador.

#### JavaScript

El siguiente código define una función, `handleRemovedIDs`, que se utilizará como llamada de retorno o promesa para gestionar las identidades recuperadas por `removeIdentities` una vez que se han eliminado del explorador.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variable | Descripción |
| --- | --- |
| `validIds` | Un objeto JSON que contiene todos los ID que se recuperaron correctamente. |
| `failedIDs` | Un objeto JSON que contiene todos los ID de los que no se recuperaron [!DNL Privacy Service], o no se encontraron. |

#### Resultado 

Si el código se ejecuta correctamente, `validIDs` se rellena con una lista de identidades recuperadas.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Pasos siguientes

Al leer este documento, se le han introducido las funcionalidades principales de la variable [!DNL Privacy JS Library]. Después de utilizar la biblioteca para recuperar una lista de identidades, puede utilizarlas para crear solicitudes de acceso a datos y eliminarlas del [!DNL Privacy Service] API. Consulte la [Guía de API del Privacy Service](api/overview.md) para obtener más información.

## Apéndice

Esta sección contiene información complementaria para usar la variable [!DNL Privacy JS Library].

### Parámetros de configuración de la solución Adobe {#config-params}

A continuación se muestra una lista de los parámetros de configuración aceptados para las soluciones de Adobe admitidas, que se utilizan cuando [creación de instancias de un objeto AdobePrivacy](#instantiate-the-privacy-js-library).

**Todas las soluciones**

| Parámetro | Descripción |
| --- | --- |
| `key` | ID único que identifica al usuario o al interesado. Esta propiedad está diseñada para utilizarse con sus propios fines de seguimiento interno y no se utiliza en el Adobe. |

**Adobe Analytics**

| Parámetro | Descripción |
| --- | --- |
| `cookieDomainPeriods` | El número de puntos de un dominio utilizado para el seguimiento de cookies (el valor predeterminado es `2`, p. ej. `.domain.com`). No la defina aquí a menos que se especifique en la señalización web de JavaScript. |
| `dataCenter` | El centro de datos de recopilación de datos de Adobe. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. Los valores posibles son: <ul><li>`d1`: Centro de datos de San José</li><li>`d2`: Centro de datos de Dallas</li></ul> |
| `reportSuite` | El ID del grupo de informes que se especifica en la señalización web de JavaScript (por ejemplo, `s_code.js` o `dtm`). |
| `trackingServer` | Un dominio de recopilación de datos que no es SSL. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |
| `trackingServerSecure` | Un dominio de recopilación de datos SSL. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |
| `visitorNamespace` | El espacio de nombres utilizado para agrupar visitantes. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |

**Adobe Audience Manager**

| Parámetro | Descripción |
| --- | --- |
| `aamUUIDCookieName` | Nombre de la cookie de origen que contiene el ID de usuario único devuelto desde Adobe Audience Manager. |

**Servicio de identidad de Adobe Experience Cloud (ECID)**

| Parámetro | Descripción |
| --- | --- |
| `imsOrgID` | Su ID de la organización IMS. |

**Adobe Target**

| Parámetro | Descripción |
| --- | --- |
| `clientCode` | Código de cliente que identifica a un cliente en el sistema Adobe Target. |
