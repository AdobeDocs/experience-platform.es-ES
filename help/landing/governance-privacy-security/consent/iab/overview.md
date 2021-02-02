---
keywords: Experience Platform;hogar;IAB;IAB 2.0;consentimiento;Consentimiento
solution: Experience Platform
title: Compatibilidad con IAB TCF 2.0 en Experience Platform
topic: privacy events
description: Obtenga información sobre cómo configurar las operaciones y esquemas de datos para transmitir las opciones de consentimiento del usuario al activar segmentos a destinos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b2d3e4608dc0640472966edccd3fb5a612d7583c
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---


# Compatibilidad con IAB TCF 2.0 en Experience Platform

El [!DNL Transparency & Consent Framework] (TCF), como se describe en el [!DNL Interactive Advertising Bureau] (IAB), es un marco técnico estándar abierto que permite a las organizaciones obtener, registrar y actualizar el consentimiento del consumidor para el procesamiento de sus datos personales, de conformidad con el [!DNL General Data Protection Regulation] (RGPD) de la Unión Europea. La segunda iteración del marco, TCF 2.0, ofrece más flexibilidad para la forma en que los consumidores pueden dar o denegar el consentimiento, incluida la posibilidad y la forma en que los proveedores pueden utilizar determinadas características del procesamiento de datos, como la geolocalización precisa.

>[!NOTE]
>
>Puede encontrar más información sobre TCF 2.0 en el [sitio web de IAB Europe](https://iabeurope.eu/tcf-2-0/), que incluye materiales de soporte y especificaciones técnicas.

Adobe Experience Platform forma parte de la lista de proveedor registrada [IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf-v2-0/), con el identificador **565**. De conformidad con los requisitos de TCF 2.0, Platform le permite recopilar datos de consentimiento del cliente e integrarlos en sus perfiles de cliente almacenados. Estos datos de consentimiento pueden tenerse en cuenta si los perfiles se incluyen en los segmentos de audiencia exportados, según el caso de uso.

>[!IMPORTANT]
>
>Platform sólo puede cumplir con la versión 2.0 del TCF (o bueno). Las versiones anteriores de TCF no son compatibles.

Este documento proporciona una visión general de cómo configurar las operaciones de datos y los esquemas de perfil para aceptar los datos de consentimiento del cliente generados por el CMP, y cómo Platform transmite las opciones de consentimiento del usuario al exportar segmentos.

## Requisitos previos

Para seguir esta guía, debe utilizar una Plataforma de Gestión de Consentimiento (CMP), ya sea comercial o propia, que esté integrada y sea compatible con el TCF de la IAB. Consulte la [lista de CMPs](https://iabeurope.eu/cmp-list/) compatibles para obtener más información.

>[!IMPORTANT]
>
>Si el ID de su CMP no es válido, Platform seguirá procesando los datos tal cual. Para hacer cumplir TCF 2.0, debe confirmar que su CMP tiene un ID válido que se ha registrado en IAB TCF 2.0 antes de enviar datos a Platform.

Esta guía también requiere una comprensión práctica de los siguientes servicios de la Plataforma:

* [Modelo de datos de experiencia (XDM)](../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil](../../../../profile/home.md) del cliente en tiempo real: Aprovecha  [!DNL Identity Service] para crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos del Data Lake y persiste en los perfiles de los clientes en su propio almacén de datos independiente.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Una biblioteca JavaScript del lado del cliente que le permite integrar varios servicios de plataforma en su sitio web orientado al cliente.
   * [Comandos](../../../../edge/consent/supporting-consent.md) de consentimiento del SDK: Información general sobre el caso de uso de los comandos del SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio](../../../../segmentation/home.md) de segmentación de Adobe Experience Platform: Permite dividir  [!DNL Real-time Customer Profile] los datos en grupos de individuos que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.

Además de los servicios de la Plataforma enumerados anteriormente, también debe estar familiarizado con [destinos](../../../../data-governance/home.md) y su función en el ecosistema de la Plataforma.

## Resumen del flujo de consentimiento del cliente {#summary}

Las siguientes secciones describen cómo se recopilan y aplican los datos de consentimiento una vez configurado correctamente el sistema.

### Recopilación de datos de consentimiento

Platform le permite recopilar datos de consentimiento del cliente a través del siguiente proceso:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos a través de un cuadro de diálogo en su sitio web.
1. El CMP detecta el cambio de preferencia de consentimiento y genera los datos de consentimiento TCF en consecuencia.
1. Con el SDK web de plataforma, los datos de consentimiento generados (devueltos por el CMP) se envían a Adobe Experience Platform.
1. Los datos de consentimiento recopilados se ingieren en un conjunto de datos habilitado para [!DNL Profile] cuyo esquema contiene campos de consentimiento TCF.

Además de los comandos del SDK activados por los enlaces de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir al Experience Platform a través de cualquier dato XDM generado por el cliente que se cargue directamente en un conjunto de datos habilitado para [!DNL Profile].

Cualquier segmento compartido con Platform por Adobe Audience Manager (a través del conector de origen [!DNL Audience Manager] o de otro modo) también puede contener datos de consentimiento, siempre que los campos correspondientes se hayan aplicado a esos segmentos mediante [!DNL Experience Cloud Identity Service]. Para obtener más información sobre la recopilación de datos de consentimiento en [!DNL Audience Manager], consulte el documento del complemento [Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Aplicación de consentimiento descendente

Una vez que los datos de consentimiento TCF se han ingerido correctamente, los siguientes procesos tienen lugar en los servicios de plataforma descendentes:

1. [!DNL Real-time Customer Profile] actualiza los datos de consentimiento almacenados para el perfil de ese cliente.
1. La plataforma procesa los ID de cliente solo si se proporciona el permiso de proveedor para Platform (565) para cada ID de un clúster.
1. Al exportar segmentos a destinos que pertenecen a miembros de la lista de proveedores de TCF 2.0, Platform solo incluye perfiles si los permisos de proveedor para la plataforma (565) *y* el destino individual se proporcionan para cada ID de un clúster.

El resto de las secciones de este documento proporcionan instrucciones sobre cómo configurar Platform y sus operaciones de datos para cumplir los requisitos de recopilación y cumplimiento descritos anteriormente.

## Determinar cómo generar datos de consentimiento del cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir que sus clientes proporcionen su consentimiento mientras interactúan con su servicio. Una forma común de lograrlo es mediante el uso de un cuadro de diálogo de consentimiento de cookie, similar al siguiente ejemplo:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Este cuadro de diálogo debe permitir que el cliente adhesión o salga de lo siguiente:

| Opción de consentimiento | Descripción |
| --- | --- |
| **Fines** | Los propósitos definen para qué propósitos publicitarios una marca puede utilizar los datos de un cliente. Para que Platform pueda procesar los ID de cliente, se deben seleccionar los siguientes objetivos: <ul><li>**Objetivo 1**: Almacenar y/o acceder a información en un dispositivo</li><li>**Objetivo 10**: Desarrollar y mejorar productos</li></ul> |
| **Permisos de proveedor** | Además de los propósitos de publicidad, el cuadro de diálogo también debe permitir al cliente adhesión o dejar de utilizar sus datos por proveedores específicos, incluido Adobe Experience Platform (565). |

### Cadenas de consentimiento {#consent-strings}

Independientemente del método que utilice para recopilar los datos, el objetivo es generar un valor de cadena basado en las opciones de consentimiento elegidas por el cliente, denominadas cadena de consentimiento.

En la especificación TCF, las cadenas de consentimiento se utilizan para codificar los detalles relevantes sobre la configuración de consentimiento del cliente, en términos de propósitos de mercadotecnia específicos, según se definen en las políticas y los proveedores. Platform utiliza estas cadenas para almacenar la configuración de consentimiento de cada cliente y, por lo tanto, debe generarse una nueva cadena de consentimiento cada vez que cambie dicha configuración.

Las cadenas de consentimiento sólo pueden ser creadas por un CMP registrado en el TCF de IAB. Para obtener más información sobre cómo generar cadenas de consentimiento usando su CMP particular, consulte la [guía de formato de cadenas de consentimiento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) en la repo de IAB TCF GitHub.

## Crear conjuntos de datos con campos de consentimiento TCF {#datasets}

Los datos de consentimiento del cliente deben enviarse a conjuntos de datos cuyos esquemas contengan campos de consentimiento TCF. Consulte el tutorial sobre [creación de conjuntos de datos para capturar el consentimiento de TCF 2.0](./dataset.md) para obtener información sobre cómo crear los dos conjuntos de datos necesarios antes de continuar con esta guía.

## Actualizar [!DNL Profile] directivas de combinación para incluir datos de consentimiento {#merge-policies}

Una vez creado un conjunto de datos habilitado para [!DNL Profile] para recopilar datos de consentimiento, debe asegurarse de que las políticas de combinación se hayan configurado para incluir siempre los campos de consentimiento TCF en los perfiles del cliente. Esto implica establecer la prioridad del conjunto de datos para que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos potencialmente conflictivos.

Para obtener más información sobre cómo trabajar con políticas de combinación, consulte la [guía del usuario de directivas de combinación](../../../../profile/ui/merge-policies.md). Al configurar las políticas de combinación, debe asegurarse de que los segmentos incluyen todos los atributos de consentimiento requeridos proporcionados por la [combinación de privacidad XDM](./dataset.md#privacy-mixin), como se describe en la guía sobre la preparación de conjuntos de datos.

## Integrar el SDK web de Experience Platform para recopilar datos de consentimiento del cliente {#sdk}

>[!NOTE]
>
>Se requiere el uso del SDK web de Experience Platform para procesar los datos de consentimiento directamente en Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no se admite actualmente.
>
>[!DNL Experience Cloud Identity Service] no obstante, sigue siendo compatible con el procesamiento de consentimiento en Adobe Audience Manager, y el cumplimiento de TCF 2.0 solo requiere que la biblioteca se actualice a la  [versión 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Una vez configurado el CMP para generar cadenas de consentimiento, debe integrar el SDK web de Experience Platform para recopilar dichas cadenas y enviarlas a Platform. El SDK de plataforma proporciona dos comandos que se pueden utilizar para enviar datos de consentimiento TCF a Platform (explicados en las subsecciones siguientes), y que se deben utilizar cuando un cliente proporcione información de consentimiento por primera vez y en cualquier momento que ese consentimiento cambie a partir de entonces.

**El SDK no interactúa con ningún CMP de forma predeterminada**. Depende de usted determinar cómo integrar el SDK en su sitio web, escuchar los cambios de consentimiento en el CMP y llamar al comando correspondiente.

### Crear una nueva configuración de Edge

Para que el SDK envíe datos al Experience Platform, primero debe crear una nueva configuración Edge para la plataforma en [!DNL Adobe Experience Platform Launch]. En la [documentación del SDK](../../../../edge/fundamentals/edge-configuration.md) se proporcionan pasos específicos para crear una nueva configuración.

Después de proporcionar un nombre único para la configuración, seleccione el botón de alternar junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los siguientes valores para completar el resto del formulario:

| Campo de configuración de Edge | Valor |
| --- | --- |
| [!UICONTROL Simulador para pruebas] | Nombre de la plataforma [simulador de pruebas](../../../../sandboxes/home.md) que contiene la conexión de flujo de datos y los conjuntos de datos necesarios para configurar la configuración de Edge. |
| [!UICONTROL Entrada de flujo continuo] | Una conexión de transmisión válida para el Experience Platform. Consulte el tutorial sobre [creación de una conexión de flujo continuo](../../../../ingestion/tutorials/create-streaming-connection-ui.md) si no tiene una entrada de flujo continuo existente. |
| [!UICONTROL Conjunto de datos de evento] | Seleccione el conjunto de datos [!DNL XDM ExperienceEvent] creado en el [paso anterior](#datasets). |
| [!UICONTROL Conjunto de datos de perfil] | Seleccione el conjunto de datos [!DNL XDM Individual Profile] creado en el [paso anterior](#datasets). |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Cuando termine, seleccione **[!UICONTROL Guardar]** en la parte inferior de la pantalla y siga las indicaciones adicionales para completar la configuración.

### Comandos de cambio de consentimiento

Una vez que haya creado la configuración de Edge descrita en la sección anterior, puede utilizar los comandos del SDK para enviar datos de consentimiento a Platform. En las secciones siguientes se proporcionan ejemplos de cómo se puede utilizar cada comando SDK en distintos escenarios.

>[!NOTE]
>
>Para obtener una introducción a la sintaxis común de todos los comandos del SDK de plataforma, consulte el documento sobre [ejecución de comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de enlaces de cambio de consentimiento de CMP

Muchos CMP proporcionan enlaces listos para usar que escuchan eventos de cambio de consentimiento. Cuando se producen estos eventos, puede utilizar el comando `setConsent` para actualizar los datos de consentimiento del cliente.

El comando `setConsent` espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, &quot;setConsent&quot;) y (2) una carga útil que contiene una matriz `consent`, que debe contener al menos un objeto que proporcione los campos de consentimiento requeridos, como se muestra a continuación:

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
| `standard` | La norma de consentimiento que se utiliza. Este valor debe establecerse en `IAB` para el procesamiento del consentimiento TCF 2.0. |
| `version` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en `2.0` para el procesamiento del consentimiento TCF 2.0. |
| `value` | La cadena de consentimiento con codificación base 64 generada por la CP/RP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. |

El comando `setConsent` debe utilizarse como parte de un enlace CMP que detecte cambios en la configuración del consentimiento. El siguiente JavaScript proporciona un ejemplo de cómo se puede utilizar el comando `setConsent` para el enlace `OnConsentChanged` de OneTrust:

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

También puede recopilar datos de consentimiento TCF 2.0 en cada evento activado en la plataforma mediante el comando `sendEvent`.

>[!NOTE]
>
>Para utilizar este método, debe haber agregado el [!DNL Experience Event Privacy mixin] al esquema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte la sección sobre [actualización del esquema de ExperienceEvent](./dataset.md#event-schema) en la guía de preparación de conjuntos de datos para ver los pasos para configurarlo.

El comando `sendEvent` debe utilizarse como una llamada de retorno en los oyentes de evento adecuados del sitio web. El comando espera dos argumentos: (1) una cadena que indica el tipo de comando (en este caso, `sendEvent`) y (2) una carga útil que contiene un objeto `xdm` que proporciona los campos de consentimiento requeridos como JSON:

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
| `consentStandard` | La norma de consentimiento que se utiliza. Este valor debe establecerse en `IAB` para el procesamiento del consentimiento TCF 2.0. |
| `consentStandardVersion` | Número de versión de la norma de consentimiento indicada en `standard`. Este valor debe establecerse en `2.0` para el procesamiento del consentimiento TCF 2.0. |
| `consentStringValue` | La cadena de consentimiento con codificación base 64 generada por la CP/RP. |
| `gdprApplies` | Valor booleano que indica si el RGPD se aplica al cliente que ha iniciado sesión. Para que TCF 2.0 se aplique a este cliente, el valor debe establecerse en `true`. |

### Gestión de las respuestas del SDK

Todos los comandos [!DNL Platform SDK] devuelven promesas que indican si la llamada se ha realizado correctamente o no. A continuación, puede usar estas respuestas para lógica adicional, como mostrar mensajes de confirmación al cliente. Consulte la sección sobre [gestión correcta o fallida](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) en la guía sobre la ejecución de comandos de SDK para ver ejemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de realizar el inicio de exportar segmentos, debe asegurarse de que los segmentos incluyen todos los campos de consentimiento requeridos. Consulte la sección sobre [configuración de políticas de combinación](#merge-policies) para obtener más información.

Una vez recopilados los datos de consentimiento del cliente y creados los segmentos de audiencia que contienen los atributos de consentimiento necesarios, puede aplicar el cumplimiento de TCF 2.0 al exportar dichos segmentos a destinos descendentes.

Siempre que la configuración de consentimiento `gdprApplies` se establezca en `true` para un conjunto de perfiles de cliente, cualquier dato de esos perfiles que se exporte a destinos descendentes se filtrará según las preferencias de consentimiento para cada perfil. Durante el proceso de exportación se omite cualquier perfil que no cumpla las preferencias de consentimiento requeridas.

Los clientes deben dar su consentimiento a los siguientes fines (como se describe en [políticas de TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que sus perfiles se incluyan en segmentos que se exportan a destinos:

* **Objetivo 1**: Almacenar y/o acceder a información en un dispositivo
* **Objetivo 10**: Desarrollar y mejorar productos

TCF 2.0 también requiere que la fuente de datos compruebe el permiso del proveedor del destino antes de enviar datos a ese destino. Como tal, Platform comprueba si el permiso de proveedor del destino está adhesión para todos los ID del clúster antes de incluir los datos enlazados a ese destino.

>[!NOTE]
>
>Cualquier segmento que se comparta con Adobe Audience Manager contendrá los mismos valores de consentimiento TCF 2.0 que sus homólogos de la plataforma. Dado que [!DNL Audience Manager] comparte el mismo ID de proveedor que Platform (565), se requieren los mismos propósitos y permisos de proveedor. Consulte el documento del complemento [Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) para obtener más información.

## Probar la implementación {#test-implementation}

Una vez configurada la implementación de TCF 2.0 y que haya exportado segmentos a destinos, no se exportarán los datos que no cumplan los requisitos de consentimiento. Sin embargo, para ver si los perfiles del cliente correctos se filtraron durante la exportación, debe comprobar manualmente los almacenes de datos de los destinos para ver si el consentimiento se aplicó correctamente.

Es importante tener en cuenta que si varios ID conforman un clúster y se aplica TCF 2.0, se excluirá todo el clúster si ni siquiera un solo ID contiene los propósitos y permisos de proveedor correctos.

## Pasos siguientes

Este documento cubrió el proceso de configuración de las operaciones de datos de la Plataforma para cumplir con sus obligaciones comerciales, tal como se describe en el TCF 2.0. Consulte la información general sobre [gobernanza, privacidad y seguridad](../../overview.md) para obtener más información sobre las capacidades relacionadas con la privacidad de la Plataforma.