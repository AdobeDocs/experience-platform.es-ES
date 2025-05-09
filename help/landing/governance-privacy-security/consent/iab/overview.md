---
keywords: Experience Platform;inicio;IAB;IAB 2.0;consentimiento;Consentimiento
solution: Experience Platform
title: Compatibilidad con IAB TCF 2.0 en Experience Platform
description: Aprenda a configurar las operaciones y los esquemas de datos para transmitir las opciones de consentimiento del cliente al activar segmentos a destinos en Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2524'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en Experience Platform

El [!DNL Transparency & Consent Framework] (TCF), tal como lo describe [!DNL Interactive Advertising Bureau] (IAB) es un marco técnico de estándar abierto diseñado para permitir que las organizaciones obtengan, registren y actualicen el consentimiento del consumidor para el procesamiento de sus datos personales, de conformidad con el [!DNL General Data Protection Regulation] (RGPD) de la Unión Europea. La segunda iteración del marco, TCF 2.0, concede más flexibilidad para la forma en que los consumidores pueden proporcionar o retener el consentimiento, incluido si los proveedores pueden utilizar determinadas características del procesamiento de datos, como la geolocalización precisa, y cómo pueden hacerlo.

>[!NOTE]
>
>Encontrará más información sobre TCF 2.0 en el [sitio web de IAB Europe](https://iabeurope.eu/), que incluye material de apoyo y especificaciones técnicas.

Adobe Experience Platform forma parte de la lista de proveedores registrada [IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf/), con el identificador **565**. De conformidad con los requisitos de TCF 2.0, Experience Platform le permite recopilar datos de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta para determinar si los perfiles se incluyen en los segmentos de audiencia exportados, según su caso de uso.

>[!IMPORTANT]
>
>Experience Platform solo puede cumplir con la versión 2.0 del TCF (o posterior). Las versiones anteriores de TCF no son compatibles.

Este documento proporciona información general sobre cómo configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por la plataforma de administración de consentimiento (CMP). También explica cómo Experience Platform transmite las opciones de consentimiento del usuario al exportar segmentos.

## Requisitos previos

Para seguir esta guía, debe utilizar una CMP, ya sea comercial o propia, integrada y compatible con el TCF de IAB. Consulte la [lista de CMP compatibles](https://iabeurope.eu/cmp-list/) para obtener más información.

>[!IMPORTANT]
>
>Si el ID de CMP no es válido, Experience Platform seguirá procesando los datos tal cual. Para aplicar TCF 2.0, debe confirmar que la CMP tiene un ID válido registrado con IAB TCF 2.0 antes de enviar datos a Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes servicios de Experience Platform:

* [Modelo de datos de experiencia (XDM)](/help/xdm/home.md): El marco de trabajo estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Servicio de identidad de Adobe Experience Platform](/help/identity-service/home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](/help/profile/home.md): Utiliza [!DNL Identity Service] para crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. [!DNL Real-Time Customer Profile] extrae datos del lago de datos y conserva los perfiles de los clientes en su propio almacén de datos independiente.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Una biblioteca JavaScript del lado del cliente que le permite integrar varios servicios de Experience Platform en su sitio web del lado del cliente.
   * [Comandos de consentimiento de SDK](../../../../web-sdk/commands/setconsent.md): Un caso de uso que describe los comandos de SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio de segmentación de Adobe Experience Platform](/help/segmentation/home.md): permite dividir los datos de [!DNL Real-Time Customer Profile] en grupos de personas que comparten características similares y responden de manera similar a las estrategias de marketing.

Además de los servicios de Experience Platform enumerados arriba, también debería estar familiarizado con [destinos](/help/data-governance/home.md) y su función en el ecosistema de Experience Platform.

## Resumen del flujo de consentimiento del cliente {#summary}

Las secciones siguientes describen cómo se recopilan y aplican los datos de consentimiento después de configurar correctamente el sistema.

### Recopilación de datos de consentimiento

Experience Platform le permite recopilar datos de consentimiento del cliente mediante el siguiente proceso:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos a través de un cuadro de diálogo en su sitio web.
1. Su CMP detecta el cambio de preferencia de consentimiento y genera los datos de consentimiento TCF en consecuencia.
1. Mediante Experience Platform Web SDK, los datos de consentimiento generados (devueltos por CMP) se envían a Adobe Experience Platform.
1. Los datos de consentimiento recopilados se incorporan a un conjunto de datos habilitado para [!DNL Profile] cuyo esquema contiene campos de consentimiento TCF.

Además de los comandos de SDK activados por los vínculos de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir a Experience Platform a través de cualquier dato XDM generado por el cliente que se cargue directamente en un conjunto de datos habilitado para [!DNL Profile].

Cualquier segmento compartido con Experience Platform por Adobe Audience Manager (a través del conector de origen [!DNL Audience Manager] o de otro modo) también puede contener datos de consentimiento si se han aplicado los campos apropiados a esos segmentos a través de [!DNL Experience Cloud Identity Service]. Para obtener más información sobre la recopilación de datos de consentimiento en [!DNL Audience Manager], consulte el documento en el complemento [Adobe Audience Manager para TCF de IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es).

### Aplicación del consentimiento descendente

Una vez que los datos de consentimiento de TCF se han introducido correctamente, los siguientes procesos tienen lugar en los servicios de Experience Platform descendentes:

1. [!DNL Real-Time Customer Profile] actualiza los datos de consentimiento almacenados para el perfil de ese cliente.
1. Experience Platform procesa los ID de cliente solo si se proporciona el permiso de proveedor para Experience Platform (565) para cada ID de un clúster.
1. Al exportar segmentos a destinos que pertenecen a miembros de la lista de proveedores de TCF 2.0, Experience Platform solo incluye perfiles si los permisos de proveedor para Experience Platform (565) *y* el destino individual se proporcionan para cada ID de un clúster.

El resto de las secciones de este documento proporcionan directrices sobre cómo configurar Experience Platform y sus operaciones de datos para cumplir los requisitos de recopilación y aplicación descritos anteriormente.

## Determine cómo generar datos de consentimiento de cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir a los clientes proporcionar consentimiento a medida que interactúan con el servicio. Un cuadro de diálogo de consentimiento de cookies es una forma común de obtener el consentimiento del cliente. A continuación se muestra un ejemplo del cuadro de diálogo CMP.

![Ejemplo de cuadro de diálogo Plataforma de administración de consentimiento.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Este cuadro de diálogo debe permitir al cliente adherirse o excluirse de lo siguiente:

| Opción de consentimiento | Descripción |
| --- | --- |
| **Propósitos** | Los objetivos definen para qué fines técnicos de publicidad una marca puede utilizar los datos de un cliente. Se deben optar por los siguientes fines para que Experience Platform procese los ID de cliente: <ul><li>**Propósito 1**: Almacenar o tener acceso a información en un dispositivo</li><li>**Propósito 10**: Desarrollar y mejorar productos</li></ul> |
| **Permisos de proveedor** | Además de los fines técnicos de la publicidad, el cuadro de diálogo también debe permitir que el cliente decida si quiere o no que sus datos sean utilizados por proveedores específicos, incluido Adobe Experience Platform (565). |

### Cadenas de consentimiento {#consent-strings}

Independientemente del método que utilice para recopilar los datos, el objetivo es generar un valor de cadena basado en las opciones de consentimiento elegidas por el cliente, denominado cadena de consentimiento.

En la especificación del TCF, las cadenas de consentimiento se utilizan para codificar detalles relevantes sobre la configuración de consentimiento de un cliente, en términos de propósitos de marketing específicos definidos por políticas y proveedores. Experience Platform utiliza estas cadenas para almacenar la configuración de consentimiento de cada cliente y, por lo tanto, se debe generar una nueva cadena de consentimiento cada vez que cambia dicha configuración.

Las cadenas de consentimiento solo las puede crear una CMP registrada en el TCF de IAB. Para obtener más información sobre cómo generar cadenas de consentimiento utilizando su CMP particular, consulte la [guía de formato de cadena de consentimiento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) en el repositorio de GitHub de TCF de IAB.

## Creación de conjuntos de datos con campos de consentimiento TCF {#datasets}

Los datos de consentimiento del cliente deben enviarse a conjuntos de datos cuyos esquemas contengan campos de consentimiento TCF. Consulte el tutorial sobre [creación de conjuntos de datos para capturar el consentimiento de TCF 2.0](./dataset.md) para saber cómo crear el conjunto de datos de perfil requerido (y un conjunto de datos de evento de experiencia opcional) antes de continuar con esta guía.

## Actualizar [!DNL Profile] políticas de combinación para incluir datos de consentimiento {#merge-policies}

Una vez que haya creado un conjunto de datos habilitado para [!DNL Profile] para recopilar datos de consentimiento, debe asegurarse de que las políticas de combinación se hayan configurado para incluir siempre campos de consentimiento TCF en los perfiles de cliente. Esto implica establecer la prioridad del conjunto de datos de modo que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos que puedan entrar en conflicto.

Para obtener más información sobre cómo trabajar con políticas de combinación, consulte [información general sobre políticas de combinación](/help/profile/merge-policies/overview.md). Al configurar las políticas de combinación, debe asegurarse de que los segmentos incluyan todos los atributos de consentimiento requeridos proporcionados por el [grupo de campos de esquema de privacidad XDM](./dataset.md#privacy-field-group), como se describe en la guía sobre preparación del conjunto de datos.

## Integración de Experience Platform Web SDK para recopilar datos de consentimiento del cliente {#sdk}

>[!NOTE]
>
>Se requiere el uso de Experience Platform Web SDK para procesar los datos de consentimiento directamente en Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no es compatible.
>
>[!DNL Experience Cloud Identity Service] sigue siendo compatible con el procesamiento de consentimiento en Adobe Audience Manager, sin embargo, y el cumplimiento con TCF 2.0 solo requiere que la biblioteca se actualice a [versión 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una vez configurada la CMP para generar cadenas de consentimiento, se debe integrar Experience Platform Web SDK para recopilar esas cadenas y enviarlas a Experience Platform. Experience Platform SDK proporciona dos comandos que se pueden utilizar para enviar datos de consentimiento TCF a Experience Platform (explicados en las subsecciones siguientes). Estos comandos deben utilizarse cuando un cliente proporciona información de consentimiento por primera vez y siempre que el consentimiento cambie a partir de entonces.

**SDK no interactúa con ninguna CMP predeterminada**. Depende de usted determinar cómo integrar SDK en su sitio web, detectar cambios de consentimiento en la CMP y llamar al comando correspondiente.

### Crear un flujo de datos

Para que SDK envíe datos a Experience Platform, primero debe crear un flujo de datos para Experience Platform. En la [documentación de SDK](/help/datastreams/overview.md) se proporcionan pasos específicos para crear un conjunto de datos.

Después de proporcionar un nombre único para la secuencia de datos, selecciona el botón de alternancia situado junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los siguientes valores para completar el resto del formulario:

| Campo de secuencia de datos | Valor |
| --- | --- |
| [!UICONTROL espacio aislado] | Nombre de la zona protegida [sandbox](/help/sandboxes/home.md) de Experience Platform que contiene la conexión de flujo continuo y los conjuntos de datos necesarios para configurar la secuencia de datos. |
| [!UICONTROL Entrada de transmisión] | Una conexión de flujo continuo válida para Experience Platform. Vea el tutorial sobre [creación de una conexión de flujo continuo](/help/ingestion/tutorials/create-streaming-connection-ui.md) si no tiene una entrada de flujo continuo existente. |
| [!UICONTROL Conjunto de datos del evento] | Seleccione el conjunto de datos [!DNL XDM ExperienceEvent] creado en el [paso anterior](#datasets). Si ha incluido el grupo de campos [[!UICONTROL Consentimiento TCF 2.0 de IAB]](/help/xdm/field-groups/event/iab.md) en el esquema de este conjunto de datos, puede rastrear los eventos de cambio de consentimiento a lo largo del tiempo mediante el comando [`sendEvent`](#sendEvent), que almacena esos datos en este conjunto de datos. Tenga en cuenta que los valores de consentimiento almacenados en este conjunto de datos son **no** utilizados en flujos de trabajo de aplicación automáticos. |
| [!UICONTROL Conjunto de datos del perfil] | Seleccione el conjunto de datos [!DNL XDM Individual Profile] creado en el [paso anterior](#datasets). Al responder a los vínculos de cambio de consentimiento de CMP mediante el comando [`setConsent`](#setConsent), los datos recopilados se almacenan en este conjunto de datos. Dado que este conjunto de datos tiene un perfil habilitado, los valores de consentimiento almacenados en este conjunto de datos se respetan durante los flujos de trabajo de aplicación automáticos. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Cuando termine, seleccione **[!UICONTROL Guardar]** en la parte inferior de la pantalla y siga las indicaciones adicionales para completar la configuración.

### Realizar comandos de cambio de consentimiento

Una vez creado el conjunto de datos descrito en la sección anterior, puede empezar a utilizar comandos de SDK para enviar datos de consentimiento a Experience Platform. Las secciones siguientes proporcionan ejemplos de cómo cada comando de SDK se puede utilizar en diferentes escenarios.

#### Uso de los vínculos de cambio de consentimiento de CMP {#setConsent}

Muchas CMP proporcionan vínculos predeterminados que escuchan eventos de cambio de consentimiento. Cuando se produzcan estos eventos, puede utilizar el comando [`setConsent`](/help/web-sdk/commands/setconsent.md) para actualizar los datos de consentimiento de ese cliente.

El comando `setConsent` espera dos argumentos:

1. Una cadena que indica el tipo de comando (en este caso, &quot;setConsent&quot;).
1. Carga útil que contiene una matriz `consent`. La matriz debe contener al menos un objeto que proporcione los campos de consentimiento requeridos.

El comando `setConsent` se muestra a continuación:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Propiedad de carga útil | Descripción |
| --- | --- |
| `standard` | El estándar de consentimiento que se está utilizando. Este valor debe establecerse en `IAB` para el procesamiento de consentimiento TCF 2.0. |
| `version` | Número de versión del estándar de consentimiento indicado en `standard`. Este valor debe establecerse en `2.0` para el procesamiento de consentimiento TCF 2.0. |
| `value` | Cadena de consentimiento codificada en base 64 generada por CMP. |
| `gdprApplies` | Un valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión actualmente. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. Si no se define, el valor predeterminado es `true`. |

El comando `setConsent` debe utilizarse como parte de un vínculo CMP que detecte cambios en la configuración de consentimiento. El siguiente JavaScript proporciona un ejemplo de cómo se puede utilizar el comando `setConsent` para el vínculo `OnConsentChanged` de OneTrust:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Uso de eventos {#sendEvent}

También puede recopilar datos de consentimiento TCF 2.0 en cada evento activado en Experience Platform mediante el comando `sendEvent`.

>[!NOTE]
>
>Para utilizar este método, debe haber agregado el grupo de campos Privacidad de Experience Event al esquema [!DNL XDM ExperienceEvent] habilitado para [!DNL Profile]. Consulte la sección sobre [actualización del esquema de ExperienceEvent](./dataset.md#event-schema) en la guía de preparación de conjuntos de datos para ver los pasos sobre cómo configurarlo.

El comando `sendEvent` debe utilizarse como llamada de retorno en los detectores de eventos adecuados del sitio web. El comando espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, `sendEvent`) y (2) una carga útil que contiene un objeto `xdm` que proporciona los campos de consentimiento requeridos como JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Propiedad de carga útil | Descripción |
| --- | --- |
| `xdm.consentStrings` | Matriz que debe contener al menos un objeto que proporcione los campos de consentimiento requeridos. |
| `consentStandard` | El estándar de consentimiento que se está utilizando. Este valor debe establecerse en `IAB` para el procesamiento de consentimiento TCF 2.0. |
| `consentStandardVersion` | Número de versión del estándar de consentimiento indicado en `standard`. Este valor debe establecerse en `2.0` para el procesamiento de consentimiento TCF 2.0. |
| `consentStringValue` | Cadena de consentimiento codificada en base 64 generada por CMP. |
| `gdprApplies` | Un valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión actualmente. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. Si no se define, el valor predeterminado es `true`. |

### Gestión de respuestas de SDK

Muchos comandos de Web SDK devuelven promesas que indican si la llamada se realizó correctamente o no. A continuación, puede utilizar estas respuestas para lógicas adicionales, como mostrar mensajes de confirmación al cliente. Consulte [Respuestas de comandos](/help/web-sdk/commands/command-responses.md) para obtener más información.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de empezar a exportar segmentos, debe asegurarse de que los segmentos incluyan todos los campos de consentimiento requeridos. Consulte la sección sobre [configuración de políticas de combinación](#merge-policies) para obtener más información.

Una vez que haya recopilado datos de consentimiento de clientes y haya creado segmentos de audiencia que contengan los atributos de consentimiento necesarios, puede aplicar la conformidad con TCF 2.0 al exportar esos segmentos a destinos descendentes.

Si la configuración de consentimiento `gdprApplies` se establece en `true` para un conjunto de perfiles de clientes, cualquier dato de esos perfiles que se exporte a destinos de flujo descendente se filtrará en función de las preferencias de consentimiento TCF para cada perfil. Cualquier perfil que no cumpla las preferencias de consentimiento requeridas se omitirá durante el proceso de exportación.

Los clientes deben aceptar los siguientes propósitos (descritos en [políticas TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que sus perfiles se incluyan en segmentos que se exportan a destinos:

* **Propósito 1**: Almacenar o tener acceso a información en un dispositivo
* **Propósito 10**: Desarrollar y mejorar productos

TCF 2.0 también requiere que el origen de los datos compruebe el permiso del proveedor de destino antes de enviar datos a ese destino. De este modo, Experience Platform comprueba si el permiso de proveedor del destino está activado para todos los ID del clúster antes de incluir los datos enlazados a dicho destino.

>[!NOTE]
>
>Cualquier segmento que se comparta con Adobe Audience Manager contiene los mismos valores de consentimiento TCF 2.0 que sus homólogos de Experience Platform. Dado que [!DNL Audience Manager] comparte el mismo ID de proveedor que Experience Platform (565), se requieren los mismos propósitos y permisos de proveedor. Consulte el documento del complemento [Adobe Audience Manager para TCF de IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es) para obtener más información.

## Prueba de la implementación {#test-implementation}

Una vez configurada la implementación de TCF 2.0 y exportados los segmentos a destinos, los datos que no cumplan los requisitos de consentimiento no se exportarán. Para ver si los perfiles de cliente correctos se filtraron durante la exportación, debe comprobar manualmente los almacenes de datos de sus destinos para ver si el consentimiento se aplicó correctamente.

>[!IMPORTANT]
>
>Si hay varios ID que conforman un clúster y se aplica TCF 2.0, se excluye todo el clúster si incluso un único ID no contiene los propósitos y permisos de proveedor correctos.

## Pasos siguientes

Este documento abarcaba el proceso de configuración de las operaciones de datos de Experience Platform para cumplir con las obligaciones comerciales descritas en TCF 2.0. Consulte la descripción general de [gobernanza, privacidad y seguridad](../../overview.md) para obtener más información sobre las capacidades relacionadas con la privacidad de Experience Platform.
