---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general sobre la biblioteca JavaScript de privacidad de Adobe
description: La biblioteca JavaScript de privacidad de Adobe le permite recuperar las identidades de los interesados para utilizarlas en Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 3%

---

# Información general sobre Adobe Privacy JavaScript Library

Como procesador de datos, el Adobe procesa los datos personales de acuerdo con los permisos e instrucciones que su empresa proporcione. Como responsable del tratamiento de datos, usted determina los datos personales que el Adobe trata y almacena en su nombre. Según la información que decida enviar a través de las soluciones de Adobe Experience Cloud, el Adobe puede almacenar información privada aplicable a las regulaciones de privacidad como [!DNL General Data Protection Regulation] (RGPD) y [!DNL California Consumer Privacy Act] (CCPA). Consulte el documento sobre la [privacidad en Adobe Experience Cloud](https://www.adobe.com/es/privacy/marketing-cloud.html) para obtener más información sobre cómo las soluciones de Experience Cloud recopilan datos privados.

La **Biblioteca JavaScript de privacidad de Adobe** permite a los controladores de datos automatizar la recuperación de todas las identidades de sujetos de datos generadas por las soluciones de [!DNL Experience Cloud] para un dominio específico. Usando la API proporcionada por [Adobe Experience Platform Privacy Service](home.md), estas identidades se pueden usar para crear solicitudes de acceso y eliminación de datos privados que pertenecen a esos interesados.

>[!NOTE]
>
>[!DNL Privacy JS Library] solo suele tener que instalarse en páginas relacionadas con la privacidad y no es necesario que esté instalado en todas las páginas de un sitio web o dominio.

## Funciones

[!DNL Privacy JS Library] proporciona varias funciones para administrar identidades en [!DNL Privacy Service]. Estas funciones solo se pueden utilizar para administrar las identidades almacenadas en el explorador para un visitante específico. No se pueden usar para enviar información directamente a [!DNL Experience Cloud Central Service].

En la tabla siguiente se describen las diferentes funciones que proporciona la biblioteca:

| Función | Descripción |
| --- | --- |
| `retrieveIdentities` | Devuelve una matriz de identidades coincidentes (`validIds`) recuperadas de [!DNL Privacy Service], así como una matriz de identidades que no se encontraron (`failedIds`). |
| `removeIdentities` | Quita del explorador todas las identidades coincidentes (válidas). Devuelve una matriz de identidades coincidentes (`validIds`), cada una de las cuales contiene un valor booleano `isDeletedClientSide` que indica si se ha eliminado este identificador. |
| `retrieveThenRemoveIdentities` | Recupera una matriz de identidades coincidentes (`validIds`) y, a continuación, quita esas identidades del explorador. Aunque esta función es similar a `removeIdentities`, se recomienda utilizarla cuando la solución de Adobe que está utilizando requiera una solicitud de acceso antes de poder realizar la eliminación (por ejemplo, cuando se debe recuperar un identificador único antes de proporcionarlo en una solicitud de eliminación). |

>[!NOTE]
>
>`removeIdentities` y `retrieveThenRemoveIdentities` solo quitan identidades del explorador para las soluciones de Adobe específicas que las admiten. Por ejemplo, Adobe Audience Manager no elimina los ID de demdex, que se almacenan en cookies de terceros, mientras que Adobe Target elimina todas las cookies que almacenan sus ID.

Dado que las tres funciones representan procesos asincrónicos, cualquier identidad recuperada debe gestionarse mediante llamadas de retorno o promesas.


## Instalación

Para empezar a usar [!DNL Privacy JS Library], debe instalarlo en el equipo mediante uno de los métodos siguientes:

* Instale utilizando npm ejecutando el siguiente comando: `npm install @adobe/adobe-privacy`
* Descargar del [repositorio de GitHub del Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

También puede instalar la biblioteca mediante una extensión de etiqueta. Consulte la descripción general de la [extensión de Adobe de privacidad](../tags/extensions/client/privacy/overview.md) para obtener más información.

## Crear una instancia de [!DNL Privacy JS Library]

Todas las aplicaciones que usan [!DNL Privacy JS Library] deben crear una instancia de un nuevo objeto `AdobePrivacy`, que debe configurarse para una solución de Adobe específica. Por ejemplo, una instancia para Adobe Analytics tendría un aspecto similar al siguiente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obtener una lista completa de los parámetros admitidos para las distintas soluciones de Adobe, consulte la sección del apéndice sobre [parámetros de configuración de la solución de Adobe admitidos](#adobe-solution-configuration-parameters).

## Muestras de código {#samples}

Los siguientes ejemplos de código muestran cómo utilizar [!DNL Privacy JS Library] en varios escenarios comunes, siempre que no utilice etiquetas.

### Recuperar identidades

Este ejemplo muestra cómo recuperar una lista de identidades de [!DNL Experience Cloud].

#### JavaScript

El siguiente código define una función, `handleRetrievedIDs`, que se utilizará como llamada de retorno o como promesa para gestionar las identidades recuperadas por `retrieveIdentities`.

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
| `validIds` | Objeto JSON que contiene todos los ID recuperados correctamente. |
| `failedIDs` | No se pudo encontrar un objeto JSON que contenga todos los identificadores que no se recuperaron de [!DNL Privacy Service] o que de otra manera no se recuperaron. |

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

En este ejemplo se muestra cómo quitar una lista de identidades del explorador.

#### JavaScript

El siguiente código define una función, `handleRemovedIDs`, que se utilizará como llamada de retorno o promesa para gestionar las identidades recuperadas por `removeIdentities` después de que se hayan eliminado del explorador.

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
| `validIds` | Objeto JSON que contiene todos los ID recuperados correctamente. |
| `failedIDs` | No se pudo encontrar un objeto JSON que contenga todos los identificadores que no se recuperaron de [!DNL Privacy Service] o que de otra manera no se recuperaron. |

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

Al leer este documento, se le han presentado las funcionalidades principales de [!DNL Privacy JS Library]. Después de usar la biblioteca para recuperar una lista de identidades, puede usar esas identidades para crear solicitudes de acceso a datos y eliminación para la API [!DNL Privacy Service]. Consulte la [guía de API de Privacy Service](api/overview.md) para obtener más información.

## Apéndice

Esta sección contiene información complementaria para utilizar [!DNL Privacy JS Library].

### Parámetros de configuración de solución de Adobe {#config-params}

A continuación se muestra una lista de los parámetros de configuración aceptados para las soluciones de Adobe admitidas que se usaron al [crear una instancia de un objeto AdobePrivacy](#instantiate-the-privacy-js-library).

**Todas las soluciones**

| Parámetro | Descripción |
| --- | --- |
| `key` | ID único que identifica al usuario o al interesado. Esta propiedad está pensada para utilizarse con fines de seguimiento interno y no se utiliza en el Adobe. |

**Adobe Analytics**

| Parámetro | Descripción |
| --- | --- |
| `cookieDomainPeriods` | El número de períodos en un dominio usado para el seguimiento de cookies (el valor predeterminado es `2`, p. ej. `.domain.com`). No la defina aquí a menos que se especifique en la señalización web de JavaScript. |
| `dataCenter` | El centro de datos de recopilación de datos de Adobe. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. Los valores potenciales son: <ul><li>`d1`: centro de datos de San José</li><li>`d2`: centro de datos de Dallas</li></ul> |
| `reportSuite` | La ID del grupo de informes según se ha especificado en la señalización web de JavaScript (por ejemplo, `s_code.js` o `dtm`). |
| `trackingServer` | Un dominio de recopilación de datos no SSL. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |
| `trackingServerSecure` | Un dominio de recopilación de datos SSL. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |
| `visitorNamespace` | Área de nombres utilizada para agrupar visitantes. Esto solo debe incluirse si se especifica en la señalización web de JavaScript. |

**Adobe Audience Manager**

| Parámetro | Descripción |
| --- | --- |
| `aamUUIDCookieName` | Nombre de la cookie de origen que contiene el ID de usuario único devuelto desde Adobe Audience Manager. |

**Servicio de identidad de Adobe Experience Cloud (ECID)**

| Parámetro | Descripción |
| --- | --- |
| `imsOrgID` | Su ID de organización. |

**Adobe Target**

| Parámetro | Descripción |
| --- | --- |
| `clientCode` | Código de cliente que identifica a un cliente en Adobe Target System. |
