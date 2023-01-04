---
keywords: Experience Platform;inicio;IAB;IAB 2.0;consentimiento;consentimiento
solution: Experience Platform
title: Compatibilidad con IAB TCF 2.0 en Experience Platform
topic-legacy: privacy events
description: Aprenda a configurar sus operaciones de datos y esquemas para transmitir las opciones de consentimiento del cliente al activar segmentos en destinos en Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Compatibilidad con IAB TCF 2.0 en Experience Platform

La variable [!DNL Transparency & Consent Framework] (TCF), tal como se describe en la [!DNL Interactive Advertising Bureau] (IAB) es un marco técnico estándar abierto destinado a permitir que las organizaciones obtengan, registren y actualicen el consentimiento de los consumidores para el tratamiento de sus datos personales, de conformidad con las disposiciones de la Unión Europea [!DNL General Data Protection Regulation] (RGPD). La segunda iteración del marco, TCF 2.0, ofrece más flexibilidad para la forma en que los consumidores pueden proporcionar o denegar el consentimiento, incluida la posibilidad y la forma en que los proveedores pueden utilizar determinadas características del procesamiento de datos, como la geolocalización precisa.

>[!NOTE]
>
>Puede encontrar más información sobre TCF 2.0 en la [Sitio web de la IAB Europe](https://iabeurope.eu/tcf-2-0/), incluidos los materiales de apoyo y las especificaciones técnicas.

Adobe Experience Platform forma parte de la [Lista de proveedores de TCF 2.0 de IAB](https://iabeurope.eu/vendor-list-tcf-v2-0/), en el ID **565**. De conformidad con los requisitos de TCF 2.0, Platform le permite recopilar datos de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento se pueden tener en cuenta si los perfiles se incluyen en segmentos de audiencia exportados, según su caso de uso.

>[!IMPORTANT]
>
>Platform solo puede cumplir con la versión 2.0 del TCF (o bueno). Las versiones anteriores de TCF no son compatibles.

Este documento proporciona información general sobre cómo configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por su CMP, y cómo Platform transmite las opciones de consentimiento del usuario al exportar segmentos.

## Requisitos previos

Para seguir esta guía, debe utilizar una plataforma de administración de consentimiento (CMP), ya sea comercial o propia, que esté integrada y sea compatible con el TCF de IAB. Consulte la [lista de CMP compatibles](https://iabeurope.eu/cmp-list/) para obtener más información.

>[!IMPORTANT]
>
>Si el ID de su CMP no es válido, Platform seguirá procesando los datos tal cual. Para aplicar TCF 2.0, debe confirmar que su CMP tiene un ID válido que se ha registrado con IAB TCF 2.0 antes de enviar datos a Platform.

Esta guía también requiere una comprensión práctica de los siguientes servicios de Platform:

* [Modelo de datos de experiencia (XDM)](../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Servicio de identidad de Adobe Experience Platform](../../../../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../../../profile/home.md): Aprovechamientos [!DNL Identity Service] para crear perfiles de cliente detallados a partir de sus conjuntos de datos en tiempo real. [!DNL Real-Time Customer Profile] extrae datos del lago de datos y mantiene los perfiles de cliente en su propio almacén de datos independiente.
* [SDK web de Adobe Experience Platform](../../../../edge/home.md): Una biblioteca JavaScript del lado del cliente que le permite integrar varios servicios de Platform en su sitio web de cliente.
   * [Comandos de consentimiento SDK](../../../../edge/consent/supporting-consent.md): Una descripción general del caso de uso de los comandos del SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio de segmentación de Adobe Experience Platform](../../../../segmentation/home.md): Permite dividir [!DNL Real-Time Customer Profile] datos en grupos de individuos que comparten características similares y que responderán de manera similar a las estrategias de marketing.

Además de los servicios de Platform enumerados anteriormente, también debe estar familiarizado con [destinos](../../../../data-governance/home.md) y su papel en el ecosistema de la Plataforma.

## Resumen del flujo de consentimiento del cliente {#summary}

Las secciones siguientes describen cómo se recopilan y aplican los datos de consentimiento una vez configurado correctamente el sistema.

### Recopilación de datos de consentimiento

Platform le permite recopilar datos de consentimiento del cliente mediante el siguiente proceso:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos mediante un cuadro de diálogo en el sitio web.
1. Su CMP detecta el cambio de preferencia de consentimiento y genera los datos de consentimiento TCF correspondientes.
1. Con el SDK web de Platform, los datos de consentimiento generados (devueltos por la CMP) se envían a Adobe Experience Platform.
1. Los datos de consentimiento recopilados se incorporan en un [!DNL Profile]Conjunto de datos habilitado para , cuyo esquema contiene campos de consentimiento TCF.

Además de los comandos del SDK activados por los enlaces de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir en el Experience Platform a través de cualquier dato XDM generado por el cliente que se cargue directamente en un [!DNL Profile]conjunto de datos habilitado para .

Cualquier segmento compartido con Platform por Adobe Audience Manager (a través de la variable [!DNL Audience Manager] conector de origen o de otro modo) también puede contener datos de consentimiento, siempre que se hayan aplicado los campos adecuados a esos segmentos mediante [!DNL Experience Cloud Identity Service]. Para obtener más información sobre la recopilación de datos de consentimiento en [!DNL Audience Manager], consulte el documento en la [Complemento de Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es).

### Aplicación del consentimiento descendente

Una vez introducidos correctamente los datos de consentimiento TCF, se llevan a cabo los siguientes procesos en los servicios de Platform descendentes:

1. [!DNL Real-Time Customer Profile] actualiza los datos de consentimiento almacenados para el perfil de ese cliente.
1. Platform procesa los ID de cliente solo si se proporciona el permiso de proveedor para Platform (565) para cada ID de un clúster.
1. Al exportar segmentos a destinos que pertenecen a miembros de la lista de proveedores de TCF 2.0, Platform solo incluye perfiles si el proveedor tiene permisos para ambas plataformas (565) *y* el destino individual se proporciona para cada ID de un clúster.

El resto de las secciones de este documento proporcionan instrucciones sobre cómo configurar Platform y sus operaciones de datos para cumplir los requisitos de recopilación y cumplimiento descritos anteriormente.

## Determinar cómo generar datos de consentimiento del cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir que sus clientes den su consentimiento mientras interactúan con su servicio. Una forma común de lograrlo es mediante el uso de un cuadro de diálogo de consentimiento de cookie, similar al siguiente ejemplo:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Este cuadro de diálogo debe permitir al cliente activar o desactivar lo siguiente:

| Opción de consentimiento | Descripción |
| --- | --- |
| **Finalidades** | Los propósitos definen para qué fines técnicos de publicidad una marca puede utilizar los datos de un cliente. Se deben elegir los siguientes fines para que Platform procese los ID de cliente: <ul><li>**Objetivo 1**: Almacenar o acceder a información en un dispositivo</li><li>**Objetivo 10**: Desarrollar y mejorar productos</li></ul> |
| **Permisos del proveedor** | Además de los fines técnicos de los anuncios, el cuadro de diálogo también debe permitir al cliente activar o desactivar el uso de sus datos por proveedores específicos, incluido Adobe Experience Platform (565). |

### Cadenas de consentimiento {#consent-strings}

Independientemente del método que utilice para recopilar los datos, el objetivo es generar un valor de cadena basado en las opciones de consentimiento elegidas por el cliente, llamadas una cadena de consentimiento.

En la especificación TCF, las cadenas de consentimiento se utilizan para codificar detalles relevantes sobre la configuración de consentimiento de un cliente, en términos de propósitos de marketing específicos definidos por políticas y proveedores. Platform utiliza estas cadenas para almacenar la configuración de consentimiento de cada cliente y, por lo tanto, se debe generar una nueva cadena de consentimiento cada vez que cambie dicha configuración.

Las cadenas de consentimiento solo se pueden crear mediante una CMP registrada en el TCF de IAB. Para obtener más información sobre cómo generar cadenas de consentimiento utilizando su CMP particular, consulte la [guía de formato de cadena de consentimiento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) en el repositorio GitHub de IAB TCF.

## Crear conjuntos de datos con campos de consentimiento TCF {#datasets}

Los datos de consentimiento del cliente deben enviarse a conjuntos de datos cuyos esquemas contienen campos de consentimiento TCF. Consulte el tutorial en [creación de conjuntos de datos para capturar el consentimiento TCF 2.0](./dataset.md) para obtener información sobre cómo crear el conjunto de datos de perfil requerido (y un conjunto de datos de evento de experiencia opcional) antes de continuar con esta guía.

## Actualizar [!DNL Profile] combinar directivas para incluir datos de consentimiento {#merge-policies}

Una vez que haya creado un [!DNL Profile]conjunto de datos habilitado para recopilar datos de consentimiento, debe asegurarse de que las políticas de combinación se hayan configurado para incluir siempre campos de consentimiento TCF en sus perfiles de cliente. Esto implica establecer la prioridad del conjunto de datos para que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos potencialmente conflictivos.

Para obtener más información sobre cómo trabajar con políticas de combinación, consulte la [información general sobre políticas de combinación](../../../../profile/merge-policies/overview.md). Al configurar las políticas de combinación, debe asegurarse de que los segmentos incluyen todos los atributos de consentimiento requeridos que proporciona el [Grupo de campos de esquema de privacidad XDM](./dataset.md#privacy-field-group), tal como se describe en la guía sobre la preparación del conjunto de datos.

## Integración del SDK web del Experience Platform para recopilar datos de consentimiento del cliente {#sdk}

>[!NOTE]
>
>Se requiere el uso del SDK web de Experience Platform para procesar los datos de consentimiento directamente en Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no es compatible actualmente.
>
>[!DNL Experience Cloud Identity Service] no obstante, sigue siendo compatible con el procesamiento de consentimiento en Adobe Audience Manager y el cumplimiento de TCF 2.0 solo requiere que la biblioteca se actualice a [versión 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una vez configurado el CMP para generar cadenas de consentimiento, debe integrar el SDK web del Experience Platform para recopilar esas cadenas y enviarlas a Platform. El SDK de plataforma proporciona dos comandos que se pueden utilizar para enviar datos de consentimiento TCF a Platform (tal como se explica en las subsecciones siguientes), y que deben utilizarse cuando un cliente proporcione información de consentimiento por primera vez y cada vez que ese consentimiento cambie a partir de entonces.

**El SDK no interactúa con ninguna CMP lista para usar**. Depende de usted determinar cómo integrar el SDK en su sitio web, detectar cambios de consentimiento en el CMP y llamar al comando correspondiente.

### Crear un nuevo conjunto de datos

Para que el SDK envíe datos a Experience Platform, primero debe crear un nuevo conjunto de datos para Platform. En la sección [Documentación del SDK](../../../../edge/datastreams/overview.md).

Después de proporcionar un nombre único para el conjunto de datos, seleccione el botón de alternancia situado junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los siguientes valores para completar el resto del formulario:

| Campo Datastream | Valor |
| --- | --- |
| [!UICONTROL Zona protegida] | El nombre de la plataforma [entorno limitado](../../../../sandboxes/home.md) que contiene la conexión de flujo continuo y los conjuntos de datos necesarios para configurar el conjunto de datos. |
| [!UICONTROL Entrada de flujo continuo] | Conexión de flujo continuo válida para el Experience Platform. Consulte el tutorial en [creación de una conexión de flujo continuo](../../../../ingestion/tutorials/create-streaming-connection-ui.md) si no tiene una entrada de flujo continuo existente. |
| [!UICONTROL Conjunto de datos del evento] | Seleccione el [!DNL XDM ExperienceEvent] conjunto de datos creado en [paso anterior](#datasets). Si ha incluido la variable [[!UICONTROL Consentimiento TCF 2.0 de IAB] grupo de campos](../../../../xdm/field-groups/event/iab.md) en el esquema de este conjunto de datos, puede rastrear eventos de cambio de consentimiento a lo largo del tiempo usando la variable [`sendEvent`](#sendEvent) almacenando esos datos en este conjunto de datos. Tenga en cuenta que los valores de consentimiento almacenados en este conjunto de datos son **not** se utiliza en flujos de trabajo de aplicación automática. |
| [!UICONTROL Conjunto de datos de perfil] | Seleccione el [!DNL XDM Individual Profile] conjunto de datos creado en [paso anterior](#datasets). Al responder a los enlaces de cambio de consentimiento de CMP mediante la variable [`setConsent`](#setConsent) , los datos recopilados se almacenarán en este conjunto de datos. Dado que este conjunto de datos tiene habilitado Perfil, los valores de consentimiento almacenados en este conjunto de datos se respetan durante los flujos de trabajo de aplicación automática. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Cuando termine, seleccione **[!UICONTROL Guardar]** en la parte inferior de la pantalla y siga las indicaciones adicionales para completar la configuración.

### Creación de comandos de cambio de consentimiento

Una vez creado el conjunto de datos descrito en la sección anterior, puede empezar a utilizar comandos del SDK para enviar datos de consentimiento a Platform. Las secciones siguientes proporcionan ejemplos de cómo se puede utilizar cada comando SDK en distintos escenarios.

>[!NOTE]
>
>Para obtener una introducción a la sintaxis común de todos los comandos del SDK de Platform, consulte el documento sobre [ejecución de comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de enlaces de cambio de consentimiento CMP {#setConsent}

Muchas CMP proporcionan enlaces listos para usar que escuchan eventos de cambio de consentimiento. Cuando se produzcan estos eventos, puede usar la variable `setConsent` para actualizar los datos de consentimiento de ese cliente.

La variable `setConsent` espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, &quot;setConsent&quot;) y (2) una carga útil que contiene un `consent` matriz, que debe contener al menos un objeto que proporcione los campos de consentimiento necesarios, como se muestra a continuación:

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

| Propiedad Payload | Descripción |
| --- | --- |
| `standard` | El estándar de consentimiento que se está utilizando. Este valor debe establecerse en `IAB` para el procesamiento del consentimiento TCF 2.0. |
| `version` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en `2.0` para el procesamiento del consentimiento TCF 2.0. |
| `value` | La cadena de consentimiento codificado base-64 generada por la CMP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. El valor predeterminado es `true` si no está definida. |

La variable `setConsent` debe utilizarse como parte de un vínculo CMP que detecte cambios en la configuración del consentimiento. El siguiente JavaScript proporciona un ejemplo de cómo `setConsent` se puede usar para OneTrust&#39;s `OnConsentChanged` gancho:

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

También puede recopilar datos de consentimiento TCF 2.0 en cada evento activado en Platform mediante el uso de la variable `sendEvent` comando.

>[!NOTE]
>
>Para utilizar este método, debe haber agregado el grupo de campos Privacidad del evento de experiencia a su [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] esquema. Consulte la sección sobre [actualización del esquema ExperienceEvent](./dataset.md#event-schema) en la guía de preparación del conjunto de datos para ver los pasos sobre cómo configurarlo.

La variable `sendEvent` debe utilizarse como llamada de retorno en los detectores de eventos adecuados del sitio web. El comando espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, `sendEvent`) y (2) una carga útil que contenga un `xdm` objeto que proporciona los campos de consentimiento requeridos como JSON:

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

| Propiedad Payload | Descripción |
| --- | --- |
| `xdm.consentStrings` | Matriz que debe contener al menos un objeto que proporcione los campos de consentimiento necesarios. |
| `consentStandard` | El estándar de consentimiento que se está utilizando. Este valor debe establecerse en `IAB` para el procesamiento del consentimiento TCF 2.0. |
| `consentStandardVersion` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en `2.0` para el procesamiento del consentimiento TCF 2.0. |
| `consentStringValue` | La cadena de consentimiento codificado base-64 generada por la CMP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. El valor predeterminado es `true` si no está definida. |

### Gestión de respuestas del SDK

Todo [!DNL Platform SDK] los comandos devuelven promesas que indican si la llamada se ha realizado correctamente o no. A continuación, puede utilizar estas respuestas para lógica adicional, como mostrar mensajes de confirmación al cliente. Consulte la sección sobre [gestión de éxito o error](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) en la guía sobre la ejecución de comandos SDK para ver ejemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de comenzar a exportar segmentos, debe asegurarse de que sus segmentos incluyen todos los campos de consentimiento necesarios. Consulte la sección sobre [configuración de directivas de combinación](#merge-policies) para obtener más información.

Una vez recopilados los datos de consentimiento del cliente y creados los segmentos de audiencia que contienen los atributos de consentimiento necesarios, puede aplicar el cumplimiento de TCF 2.0 al exportar dichos segmentos a destinos descendentes.

Siempre que la configuración de consentimiento `gdprApplies` está configurado como `true` para un conjunto de perfiles de clientes, cualquier dato de esos perfiles que se exporte a destinos descendentes se filtra según las preferencias de consentimiento TCF para cada perfil. Cualquier perfil que no cumpla las preferencias de consentimiento requeridas se omite durante el proceso de exportación.

Los clientes deben dar su consentimiento a los siguientes fines (tal como se describe en [Políticas de TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que sus perfiles se incluyan en segmentos que se exportan a destinos:

* **Objetivo 1**: Almacenar o acceder a información en un dispositivo
* **Objetivo 10**: Desarrollar y mejorar productos

TCF 2.0 también requiere que la fuente de datos compruebe el permiso del proveedor de destino antes de enviar datos a ese destino. De este modo, Platform comprueba si el permiso de proveedor del destino se ha elegido en para todos los ID del clúster antes de incluir los datos enlazados a ese destino.

>[!NOTE]
>
>Cualquier segmento compartido con Adobe Audience Manager contendrá los mismos valores de consentimiento de TCF 2.0 que sus homólogos de Platform. Since [!DNL Audience Manager] comparte el mismo ID de proveedor que Platform (565), se requieren los mismos propósitos y permisos de proveedor. Consulte el documento en la [Complemento de Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es) para obtener más información.

## Probar la implementación {#test-implementation}

Una vez que haya configurado la implementación de TCF 2.0 y haya exportado segmentos a destinos, no se exportarán los datos que no cumplan los requisitos de consentimiento. Sin embargo, para ver si los perfiles de cliente correctos se filtraron durante la exportación, debe comprobar manualmente los almacenes de datos de los destinos para ver si el consentimiento se aplicó correctamente.

Es importante tener en cuenta que si varios ID conforman un clúster y se aplica TCF 2.0, todo el clúster se excluirá si incluso un único ID no contiene los propósitos correctos y los permisos del proveedor.

## Pasos siguientes

Este documento abarcaba el proceso de configuración de las operaciones de datos de Platform para cumplir con sus obligaciones comerciales, tal como se describe en TCF 2.0. Consulte la información general sobre [administración, privacidad y seguridad](../../overview.md) para obtener más información sobre las funcionalidades relacionadas con la privacidad de Platform.
