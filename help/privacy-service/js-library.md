---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general sobre la biblioteca JavaScript de privacidad de Adobe
topic: overview
description: La biblioteca JavaScript de privacidad de Adobe le permite recuperar identidades de sujeto de datos para utilizarlas en Privacy Service.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 6%

---


# Información general sobre la biblioteca JavaScript de privacidad de Adobe

Como procesador de datos, Adobe procesa los datos personales de acuerdo con las instrucciones y los permisos de su compañía. Como responsable del tratamiento de datos, determinará qué datos personales Adobe trata y almacena en su nombre. Según la información que elija enviar a través de las soluciones de Adobe Experience Cloud, Adobe puede almacenar información privada aplicable a las regulaciones de privacidad, como [!DNL General Data Protection Regulation] (GDPR) y [!DNL California Consumer Privacy Act] (CCPA). Consulte el documento sobre [privacidad en Adobe Experience Cloud](https://www.adobe.com/es/privacy/marketing-cloud.html) para obtener más información sobre cómo las soluciones de Experience Cloud recopilan datos privados.

La **biblioteca JavaScript de privacidad de Adobe** permite a los controladores de datos automatizar la recuperación de todas las identidades de sujeto de datos generadas por las soluciones [!DNL Experience Cloud] para un dominio específico. Utilizando la API proporcionada por [Adobe Experience Platform Privacy Service](home.md), estas identidades se pueden utilizar para crear solicitudes de acceso y eliminar solicitudes de datos privados pertenecientes a esos sujetos de datos.

>[!NOTE]
>
>El [!DNL Privacy JS Library] generalmente sólo necesita instalarse en páginas relacionadas con la privacidad y no es necesario que se instale en todas las páginas de un sitio Web o dominio.

## Funciones

El [!DNL Privacy JS Library] proporciona varias funciones para administrar identidades en [!DNL Privacy Service]. Estas funciones solo se pueden usar para administrar las identidades almacenadas en el navegador para un visitante específico. No se pueden utilizar para enviar información directamente a [!DNL Experience Cloud Central Service].

La siguiente tabla describe las diferentes funciones proporcionadas por la biblioteca:

| Función | Descripción |
| --- | --- |
| `retrieveIdentities` | Devuelve una matriz de identidades coincidentes (`validIds`) que se recuperaron de [!DNL Privacy Service], así como una matriz de identidades que no se encontraron (`failedIds`). |
| `removeIdentities` | Quita cada identidad coincidente (válida) del explorador. Devuelve una matriz de identidades coincidentes (`validIds`), con cada identidad que contiene un booleano `isDeletedClientSide` que indica si este ID se ha eliminado. |
| `retrieveThenRemoveIdentities` | Recupera una matriz de identidades coincidentes (`validIds`) y, a continuación, quita esas identidades del explorador. Aunque esta función es similar a `removeIdentities`, es mejor utilizarla cuando la solución de Adobe que está utilizando requiere una solicitud de acceso antes de poder eliminarla (por ejemplo, cuando se debe recuperar un identificador único antes de proporcionarlo en una solicitud de eliminación). |

>[!NOTE]
>
>`removeIdentities` y  `retrieveThenRemoveIdentities` solo elimine identidades del explorador para soluciones de Adobe específicas que las admitan. Por ejemplo, Adobe Audience Manager no elimina los ID de demdex almacenados en cookies de terceros, mientras que Adobe Target elimina todas las cookies que almacenan sus ID.

Dado que las tres funciones representan procesos asincrónicos, cualquier identidad recuperada debe gestionarse mediante rellamadas o promesas.


## Instalación

Para realizar inicios mediante el uso de [!DNL Privacy JS Library], debe instalarlo en el equipo mediante uno de los siguientes métodos:

* Para realizar la instalación con npm, ejecute el siguiente comando: `npm install @adobe/adobe-privacy`
* Utilice la extensión de lanzamiento de Adobe con el nombre `AdobePrivacy`
* Descarga desde el [repositorio de GitHub Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Cree una instancia de [!DNL Privacy JS Library]

Todas las aplicaciones que utilicen el [!DNL Privacy JS Library] deben crear una instancia de un nuevo objeto `AdobePrivacy`, que debe configurarse en una solución de Adobe específica. Por ejemplo, una instancia de Adobe Analytics tendría un aspecto similar al siguiente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obtener una lista completa de los parámetros admitidos para distintas soluciones de Adobe, consulte la sección del apéndice sobre los parámetros de configuración de la solución de Adobe [admitidos](#adobe-solution-configuration-parameters).

## Ejemplos de código

Los siguientes ejemplos de código muestran cómo utilizar [!DNL Privacy JS Library] en varios escenarios comunes, siempre que no utilice [!DNL Launch] o DTM.

### Recuperar identidades

Este ejemplo muestra cómo recuperar una lista de identidades de [!DNL Experience Cloud].

#### JavaScript

El siguiente código define una función, `handleRetrievedIDs`, que se utilizará como llamada de retorno o promesa para manejar las identidades recuperadas por `retrieveIdentities`.

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
| `failedIDs` | Un objeto JSON que contiene todos los ID que no se recuperaron de [!DNL Privacy Service] o que no se encontraron de otro modo. |

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

El siguiente código define una función, `handleRemovedIDs`, que se utilizará como llamada de retorno o promesa de administrar las identidades recuperadas por `removeIdentities` después de haber sido eliminadas del explorador.

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
| `failedIDs` | Un objeto JSON que contiene todos los ID que no se recuperaron de [!DNL Privacy Service] o que no se encontraron de otro modo. |

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

Al leer este documento, se le han presentado las funcionalidades principales del [!DNL Privacy JS Library]. Después de utilizar la biblioteca para recuperar una lista de identidades, puede utilizarlas para crear acceso a datos y eliminar solicitudes a la API [!DNL Privacy Service]. Consulte la [guía para desarrolladores de Privacy Service](api/getting-started.md) para obtener más información.

## Apéndice

Esta sección contiene información adicional para utilizar [!DNL Privacy JS Library].

### Parámetros de configuración de la solución Adobe

A continuación se muestra una lista de los parámetros de configuración aceptados para las soluciones de Adobe admitidas, que se utilizan al [crear una instancia de un objeto AdobePrivacy](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parámetro | Descripción |
| --- | --- |
| `cookieDomainPeriods` | Períodos numéricos en un dominio para el seguimiento de cookies (el valor predeterminado es 2). |
| `dataCenter` | Centro de datos de recopilación de datos de Adobe. Esto solo debe incluirse si se especifica en la señalización web JavaScript. Los valores posibles son: <ul><li>&quot;d1&quot;: Centro de datos de San José.</li><li>&quot;d2&quot;: Centro de datos de Dallas.</li></ul> |
| `reportSuite` | ID del grupo de informes tal como se especifica en la señalización web JavaScript (por ejemplo, &quot;s_code.js&quot; o &quot;dtm&quot;). |
| `trackingServer` | Dominio de recopilación de datos (no SSL). Esto solo debe incluirse si se especifica en la señalización web JavaScript. |
| `trackingServerSecure` | Dominio de recopilación de datos (SSL). Esto solo debe incluirse si se especifica en la señalización web JavaScript. |
| `visitorNamespace` | Área de nombres utilizada para agrupar visitantes. Esto solo debe incluirse si se especifica en la señalización web JavaScript. |

**Adobe Target**

| Parámetro | Descripción |
| --- | --- |
| `clientCode` | Código de cliente que identifica a un cliente en Adobe Target System. |

**Adobe Audience Manager**

| Parámetro | Descripción |
| --- | --- |
| `aamUUIDCookieName` | Nombre de la cookie de origen que contiene el ID de usuario único devuelto por Adobe Audience Manager. |

**Servicio Adobe ID (ECID)**

| Parámetro | Descripción |
| --- | --- |
| `imsOrgID` | Su ID de la organización IMS. |