---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: Compatibilidad con IAB TCF 2.0 en la plataforma de datos del cliente en tiempo real
topic: privacy events
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 1%

---


# Compatibilidad con IAB TCF 2.0 en [!DNL Real-time Customer Data Platform]

El [!DNL Transparency & Consent Framework] (TCF), tal como se describe en la [!DNL Interactive Advertising Bureau] (IAB), es un marco técnico estándar abierto que permite a las organizaciones obtener, registrar y actualizar el consentimiento de los consumidores para el tratamiento de sus datos personales, de conformidad con el [!DNL General Data Protection Regulation] RGPD de la Unión Europea. La segunda iteración del marco, TCF 2.0, ofrece más flexibilidad para la forma en que los consumidores pueden dar o denegar el consentimiento, incluida la posibilidad y la forma en que los proveedores pueden utilizar determinadas características del procesamiento de datos, como la geolocalización precisa.

>[!NOTE]
>
>Puede encontrar más información sobre TCF 2.0 en el sitio web [de](https://iabeurope.eu/tcf-2-0/)IAB Europe, incluidos materiales de apoyo y especificaciones técnicas.

[!DNL Real-time Customer Data Platform (Real-time CDP)] forma parte de la lista [de proveedores registrada](https://iabeurope.eu/vendor-list-tcf-v2-0/)IAB TCF 2.0, con el ID **565**. De conformidad con los requisitos de TCF 2.0, [!DNL Real-time CDP] le permite recopilar datos de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento pueden tenerse en cuenta si los perfiles se incluyen en los segmentos de audiencia exportados, según el caso de uso.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] solo puede cumplir con la versión 2.0 del TCF (o bueno). Las versiones anteriores de TCF no son compatibles.

Este documento proporciona información general sobre cómo configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por el CMP, y cómo [!DNL Real-time CDP] transmitir las opciones de consentimiento del usuario al exportar segmentos.

## Requisitos previos

Para seguir esta guía, debe utilizar una Plataforma de Gestión de Consentimiento (CMP), ya sea comercial o propia, que esté integrada y sea compatible con el TCF de la IAB. Consulte la [lista de CMP](https://iabeurope.eu/cmp-list/) compatibles para obtener más información.

>[!IMPORTANT]
>
>Si el ID de su CMP no es válido, [!DNL Real-time CDP] seguirá procesando sus datos tal cual. Para hacer cumplir TCF 2.0, debe confirmar que su CMP tiene un ID válido que se ha registrado en IAB TCF 2.0 antes de enviar datos a [!DNL Experience Platform].

Esta guía también requiere una comprensión práctica de los siguientes servicios de Adobe Experience Platform:

* [Modelo de datos de experiencia (XDM)](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil](../../../profile/home.md)del cliente en tiempo real: Aprovecha [!DNL Identity Service] para crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos del Data Lake y persiste en los perfiles de los clientes en su propio almacén de datos independiente.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Biblioteca de JavaScript del lado del cliente que le permite integrar varios [!DNL Platform] servicios en el sitio web orientado al cliente.
   * [Comandos](../../../edge/fundamentals/supporting-consent.md)de consentimiento del SDK: Información general sobre el caso de uso de los comandos del SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio](../../../segmentation/home.md)de segmentación de Adobe Experience Platform: Permite dividir [!DNL Real-time Customer Profile] los datos en grupos de individuos que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.

Además de los [!DNL Platform] servicios mencionados anteriormente, también debe estar familiarizado con [los destinos](../../destinations/destinations-overview.md) y su uso en [!DNL Real-time CDP].

## Resumen del flujo de consentimiento del cliente {#summary}

Las siguientes secciones describen cómo se recopilan y aplican los datos de consentimiento una vez configurado correctamente el sistema.

### Recopilación de datos de consentimiento

[!DNL Real-time CDP] le permite recopilar datos de consentimiento del cliente a través del siguiente proceso:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos a través de un cuadro de diálogo en su sitio web.
1. El CMP detecta el cambio de preferencia de consentimiento y genera los datos de consentimiento de IAB en consecuencia.
1. Utilizando el [!DNL Experience Platform Web SDK], los datos de consentimiento generados (devueltos por el CMP) se envían a Adobe Experience Platform.
1. Los datos de consentimiento recopilados se ingieren en un conjunto de datos [!DNL Profile]habilitado cuyo esquema contiene campos de consentimiento de la IAB.

Además de los comandos del SDK activados por los enlaces de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir [!DNL Experience Platform] a través de cualquier dato XDM generado por el cliente que se cargue directamente en un conjunto de datos [!DNL Profile]habilitado.

Cualquier segmento compartido con [!DNL Platform] Adobe Audience Manager (a través del conector de [!DNL Audience Manager] origen o de otro modo) también puede contener datos de consentimiento, siempre que los campos correspondientes se hayan aplicado a esos segmentos a través de [!DNL Experience Cloud Identity Service]. Para obtener más información sobre la recopilación de datos de consentimiento en [!DNL Audience Manager], consulte el documento del complemento de [Adobe Audience Manager para IAB TCF](https://docs.adobe.com/help/es-ES/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Aplicación de consentimiento descendente

Una vez que los datos de consentimiento de la IAB se han ingerido con éxito, se realizan los siguientes procesos en los servicios [!DNL Real-time CDP] intermedios:

1. [!DNL Real-time Customer Profile] actualiza los datos de consentimiento almacenados para el perfil de ese cliente.
1. [!DNL Real-time CDP] procesa los ID de cliente solo si se proporciona el permiso de proveedor para [!DNL Real-time CDP] (565) para cada ID de un clúster.
1. Cuando se exportan segmentos a destinos que pertenecen a miembros de la lista de proveedores de TCF 2.0, [!DNL Real-time CDP] solo se incluyen perfiles si se proporcionan los permisos de proveedor tanto para [!DNL Real-time CDP] (565) *como* para cada ID de un clúster.

El resto de las secciones de este documento proporcionan instrucciones sobre cómo configurar [!DNL Real-time CDP] y sus operaciones de datos para cumplir los requisitos de recopilación y cumplimiento descritos anteriormente.

## Determinar cómo generar datos de consentimiento del cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir que sus clientes proporcionen su consentimiento mientras interactúan con su servicio. Una forma común de lograrlo es mediante el uso de un cuadro de diálogo de consentimiento de cookie, similar al siguiente ejemplo:

![](../assets/iab/cmp-dialog.png)

Este cuadro de diálogo debe permitir que el cliente adhesión o salga de lo siguiente:

| Opción de consentimiento | Descripción |
| --- | --- |
| **Fines** | Los propósitos definen para qué propósitos publicitarios una marca puede utilizar los datos de un cliente. Para poder [!DNL Real-time CDP] procesar los ID de cliente, se deben seleccionar los siguientes objetivos: <ul><li>**Objetivo 1**: Almacenar y/o acceder a información en un dispositivo</li><li>**Objetivo 10**: Desarrollar y mejorar productos</li></ul> |
| **Permisos de proveedor** | Además de los propósitos de publicidad, el cuadro de diálogo también debe permitir al cliente adhesión o dejar de utilizar sus datos por proveedores específicos, incluido [!DNL  Real-time CDP] (565). |

### Cadenas de consentimiento {#consent-strings}

Independientemente del método que utilice para recopilar los datos, el objetivo es generar un valor de cadena basado en las opciones de consentimiento elegidas por el cliente, denominadas cadena de consentimiento.

En la especificación TCF, las cadenas de consentimiento se utilizan para codificar los detalles relevantes sobre la configuración de consentimiento del cliente, en términos de propósitos de mercadotecnia específicos, según se definen en las políticas y los proveedores. [!DNL Real-time CDP] utiliza estas cadenas para almacenar la configuración de consentimiento para cada cliente y, por lo tanto, debe generarse una nueva cadena de consentimiento cada vez que cambie dicha configuración.

Las cadenas de consentimiento sólo pueden ser creadas por un CMP registrado en el TCF de IAB. Para obtener más información sobre cómo generar cadenas de consentimiento usando su CMP particular, consulte la guía [de formato de la cadena de](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) consentimiento en la repo de IAB TCF GitHub.

## Crear conjuntos de datos con campos de consentimiento de IAB {#datasets}

Los datos de consentimiento del cliente deben enviarse a un conjunto de datos cuyo esquema contenga campos de consentimiento de IAB. Consulte el tutorial sobre la [creación de conjuntos de datos para capturar el consentimiento](./dataset-preparation.md) TCF 2.0 para crear los dos conjuntos de datos necesarios antes de continuar con esta guía.

## Actualizar directivas de combinación [!DNL Profile] para incluir datos de consentimiento {#merge-policies}

Una vez que haya creado un conjunto de datos [!DNL Profile]habilitado para recopilar datos de consentimiento, debe asegurarse de que las directivas de combinación se hayan configurado para incluir siempre los campos de consentimiento de IAB en los perfiles del cliente. Esto implica establecer la prioridad del conjunto de datos para que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos potencialmente conflictivos.

Para obtener más información sobre cómo trabajar con políticas de combinación, consulte la guía [del usuario de directivas de](../../../profile/ui/merge-policies.md)combinación. Al configurar las políticas de combinación, debe asegurarse de que los segmentos incluyen todos los atributos de consentimiento requeridos proporcionados por la combinación [de privacidad de](./dataset-preparation.md#privacy-mixin)XDM, como se describe en la guía sobre la preparación de conjuntos de datos.

## Integrar el SDK [!DNL Experience Platform] web para recopilar datos de consentimiento del cliente {#sdk}

>[!NOTE]
>
>Se requiere el uso del SDK [!DNL Experience Platform] web para procesar los datos de consentimiento directamente en Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no se admite actualmente.
>
>[!DNL Experience Cloud Identity Service] no obstante, sigue siendo compatible con el procesamiento de consentimiento en Adobe Audience Manager, y el cumplimiento de TCF 2.0 solo requiere que la biblioteca se actualice a la [versión 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una vez configurado el CMP para generar cadenas de consentimiento, debe integrar el SDK [!DNL Experience Platform] Web para recopilar dichas cadenas y enviarlas a [!DNL Platform]. El SDK [!DNL Platform] proporciona dos comandos que se pueden utilizar para enviar datos de consentimiento de IAB a Platform (explicados en las subsecciones siguientes) y que se deben utilizar cuando un cliente proporcione información de consentimiento por primera vez y en cualquier momento en que ese consentimiento cambie posteriormente.

**El SDK no interactúa con ningún CMP de forma predeterminada**. Depende de usted determinar cómo integrar el SDK en su sitio web, escuchar los cambios de consentimiento en el CMP y llamar al comando correspondiente.

### Crear una nueva configuración de Edge

Para que el SDK pueda enviar datos a [!DNL Experience Platform], primero debe crear una nueva configuración Edge para [!DNL Platform] en [!DNL Adobe Experience Platform Launch]. En la documentación [del](../../../edge/fundamentals/edge-configuration.md)SDK se proporcionan pasos específicos para crear una nueva configuración.

Después de proporcionar un nombre único para la configuración, seleccione el botón de alternar situado junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los siguientes valores para completar el resto del formulario:

| Campo de configuración de Edge | Valor |
| --- | --- |
| [!UICONTROL Simulador para pruebas] | El nombre del [!DNL Platform] simulador de pruebas [](../../../sandboxes/home.md) que contiene la conexión de flujo y los conjuntos de datos necesarios para configurar la configuración de Edge. |
| [!UICONTROL Entrada de flujo continuo] | Una conexión de flujo válida para [!DNL Experience Platform]. Consulte el tutorial sobre la [creación de una conexión](../../../ingestion/tutorials/create-streaming-connection-ui.md) de flujo continuo si no tiene una entrada de flujo continuo existente. |
| [!UICONTROL Conjunto de datos de evento] | Seleccione el [!DNL XDM ExperienceEvent] conjunto de datos creado en el paso [](#datasets)anterior. |
| [!UICONTROL Conjunto de datos de perfil] | Seleccione el [!DNL XDM Individual Profile] conjunto de datos creado en el paso [](#datasets)anterior. |

![](../assets/iab/edge-config.png)

Cuando termine, haga clic en **[!UICONTROL Guardar]** en la parte inferior de la pantalla y siga las indicaciones adicionales para completar la configuración.

### Comandos de cambio de consentimiento

Una vez que haya creado la configuración de Edge descrita en la sección anterior, puede utilizar los comandos del SDK para enviar datos de consentimiento a [!DNL Platform]. En las secciones siguientes se proporcionan ejemplos de cómo se puede utilizar cada comando SDK en distintos escenarios.

>[!NOTE]
>
>Para obtener una introducción a la sintaxis común de todos los comandos [!DNL Platform] del SDK, consulte el documento sobre la [ejecución de comandos](../../../edge/fundamentals/executing-commands.md).

#### Uso de enlaces de cambio de consentimiento de CMP

Muchos CMP proporcionan enlaces listos para usar que escuchan eventos de cambio de consentimiento. Cuando se producen estos eventos, puede utilizar el comando `setConsent` para actualizar los datos de consentimiento del cliente.

El `setConsent` comando espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, &quot;setConsent&quot;) y (2) una carga útil que contiene una `consent` matriz, que debe contener al menos un objeto que proporcione los campos de consentimiento requeridos, como se muestra a continuación:

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
| `standard` | La norma de consentimiento que se utiliza. Este valor debe establecerse en &quot;IAB&quot; para el procesamiento del consentimiento TCF 2.0. |
| `version` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en &quot;2.0&quot; para el procesamiento del consentimiento TCF 2.0. |
| `value` | La cadena de consentimiento con codificación base 64 generada por la CP/RP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en &quot;true&quot;. |

El `setConsent` comando debe utilizarse como parte de un enlace CMP que detecte cambios en la configuración del consentimiento. El siguiente JavaScript proporciona un ejemplo de cómo se puede utilizar el `setConsent` comando para el `OnConsentChanged` gancho de OneTrust:

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

#### Uso de eventos

También puede recopilar datos de consentimiento TCF 2.0 en cada evento activado [!DNL Platform] mediante el `sendEvent` comando.

>[!NOTE]
>
>Para utilizar este método, debe haber agregado el [!DNL Experience Event Privacy mixin] a su [!DNL Profile]esquema [!DNL XDM ExperienceEvent] habilitado. Consulte la sección sobre la [actualización del esquema](./dataset-preparation.md#event-schema) ExperienceEvent en la guía de preparación de conjuntos de datos para ver los pasos para configurarlo.

El `sendEvent` comando debe utilizarse como llamada de retorno en los oyentes de evento adecuados del sitio web. El comando espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, &quot;sendEvent&quot;) y (2) una carga útil que contiene un `xdm` objeto que proporciona los campos de consentimiento requeridos como JSON:

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
| `xdm.consentStrings` | Matriz que debe contener al menos un objeto que proporcione los campos de consentimiento necesarios. |
| `consentStandard` | La norma de consentimiento que se utiliza. Este valor debe establecerse en &quot;IAB&quot; para el procesamiento del consentimiento TCF 2.0. |
| `consentStandardVersion` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en &quot;2.0&quot; para el procesamiento del consentimiento TCF 2.0. |
| `consentStringValue` | La cadena de consentimiento con codificación base 64 generada por la CP/RP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en &quot;true&quot;. |

### Gestión de las respuestas del SDK

Todos los [!DNL Platform SDK] comandos devuelven promesas que indican si la llamada se ha realizado correctamente o no. A continuación, puede usar estas respuestas para lógica adicional, como mostrar mensajes de confirmación al cliente. Consulte la sección sobre la [gestión de errores](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) o éxitos en la guía sobre la ejecución de comandos de SDK para ver ejemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de realizar el inicio de exportar segmentos, debe asegurarse de que los segmentos incluyen todos los campos de consentimiento requeridos. Consulte la sección sobre la [configuración de políticas](#merge-policies) de combinación para obtener más información.

Una vez recopilados los datos de consentimiento del cliente y creados los segmentos de audiencia que contienen los atributos de consentimiento necesarios, puede aplicar el cumplimiento de TCF 2.0 al exportar dichos segmentos a destinos descendentes.

Siempre que la configuración de consentimiento `gdprApplies` se establezca en `true` para un conjunto de perfiles del cliente, cualquier dato de esos perfiles que se exporta a destinos posteriores se filtrará en función de las preferencias de consentimiento para cada perfil. Durante el proceso de exportación se omite cualquier perfil que no cumpla las preferencias de consentimiento requeridas.

Los clientes deben dar su consentimiento a los siguientes fines (como se describe en las políticas [](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)TCF 2.0) para que sus perfiles se incluyan en segmentos que se exportan a destinos:

* **Objetivo 1**: Almacenar y/o acceder a información en un dispositivo
* **Objetivo 10**: Desarrollar y mejorar productos

TCF 2.0 también requiere que la fuente de datos compruebe el permiso del proveedor del destino antes de enviar datos a ese destino. Como tal, [!DNL Real-time CDP] comprueba si el permiso de proveedor del destino está adhesión para todos los ID del clúster antes de incluir los datos enlazados a ese destino.

>[!NOTE]
>
>Cualquier segmento que se comparta con Adobe Audience Manager contendrá los mismos valores de consentimiento TCF 2.0 que sus [!DNL Platform] homólogos. Dado que [!DNL Audience Manager] comparte el mismo ID de proveedor que [!DNL Real-time CDP] (565), se requieren los mismos propósitos y permisos de proveedor. Consulte el documento en el complemento [Adobe Audience Manager para TCF](https://docs.adobe.com/help/es-ES/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) IAB para obtener más información.

## Test your implementation {#test-implementation}

Una vez configurada la implementación de TCF 2.0 y que haya exportado segmentos a destinos, no se exportarán los datos que no cumplan los requisitos de consentimiento. Sin embargo, para ver si los perfiles del cliente correctos se filtraron durante la exportación, debe comprobar manualmente los almacenes de datos de los destinos para ver si el consentimiento se aplicó correctamente.

Es importante tener en cuenta que si varios ID conforman un clúster y se aplica TCF 2.0, se excluirá todo el clúster si ni siquiera un solo ID contiene los propósitos y permisos de proveedor correctos.

## Pasos siguientes

Este documento cubrió el proceso de configuración de las operaciones de datos en [!DNL Real-time CDP] para ser compatible con TCF 2.0. Para obtener más información sobre las demás funciones de privacidad proporcionadas por [!DNL Real-time CDP], consulte la siguiente documentación:

* [Privacidad en tiempo real CDP](../privacy-overview.md)
* [Administración de datos en tiempo real CDP](../data-governance-overview.md)