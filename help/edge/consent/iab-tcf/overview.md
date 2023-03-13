---
title: Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento de IAB TCF 2.0 mediante el SDK web de Adobe Experience Platform
keywords: consentimiento;setConsent;Grupo de campos de privacidad de perfil;Grupo de campos de privacidad de evento de experiencia;Grupo de campos de privacidad;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es compatible con el marco de transparencia y consentimiento del Interactive Advertising Bureau, versión 2.0 (IAB TCF 2.0). Esta guía muestra los requisitos para admitir IAB TCF 2.0 a través de la integración del SDK web de Adobe Experience Platform con Adobe Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics y Experience Edge.

Además, las siguientes guías están disponibles para ayudarle a aprender a integrar IAB TCF 2.0 con y sin etiquetas.

- [Con etiquetas](./with-launch.md)
- [Sin etiquetas](./without-launch.md)

## Primeros pasos

Para implementar el SDK web con IAB TCF 2.0, se necesita una comprensión práctica del Modelo de datos de experiencia (XDM) y los Eventos de experiencia. Antes de empezar, revise el siguiente documento:

- [Información general del sistema del modelo de datos de experiencia (XDM)](../../../xdm/home.md): La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## Integración de Experience Platform

Para enviar datos de consentimiento a Adobe Experience Platform mediante el SDK, se requiere lo siguiente:

- Un conjunto de datos cuyo esquema se basa en [!DNL XDM Individual Profile] y contiene campos de consentimiento TCF 2.0, habilitados para su uso en [!DNL Real-Time Customer Profile].
- Un conjunto de datos configurado con Platform y el conjunto de datos habilitado para perfil mencionado anteriormente.

Consulte la guía de [Cumplimiento de TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener instrucciones sobre la creación de los conjuntos de datos y el conjunto de datos necesarios.

## Integración de Audience Manager

Adobe Audience Manager AAM () incluye compatibilidad con IAB TCF 2.0, que le permite evaluar, cumplir y reenviar las opciones de privacidad del cliente a socios comerciales. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrarse con Audience Manager a través del SDK web de Adobe Experience Platform, asegúrese de tener configurado un conjunto de datos para reenviar a Adobe Audience Manager.

## Integración de Experience Events y Adobe Analytics

Mientras que las audiencias de Real-Time CDP y Audience Manager realizan un seguimiento de las preferencias de consentimiento actuales de un cliente, los eventos de experiencia pueden contener las preferencias de consentimiento de un cliente que estaban activas cuando se recopiló el evento.

Para recopilar información de consentimiento sobre eventos, se requiere lo siguiente:

- Un conjunto de datos basado en [!DNL XDM Experience Event] clase, con el [!DNL Experience Event] grupo de campos esquema de privacidad.
- Un conjunto de datos configurado con [!DNL XDM Experience Event] conjunto de datos anterior.

Para obtener más información sobre cómo convertir un evento de experiencia XDM en una visita de Analytics, comience leyendo el [Resumen de Analytics](../../data-collection/adobe-analytics/analytics-overview.md) documentación.

## Integración del SDK web de Adobe Experience Platform

Las secciones siguientes describen los principales puntos de integración entre IAB TCF 2.0 y el SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Incluso sin Real-Time CDP o Audience Manager configurados, puede integrar IAB TCF 2.0 con el SDK web. Las preferencias de consentimiento se pueden utilizar para controlar la recopilación de eventos de experiencia y configurar una cookie de identidad.

### Consentimiento predeterminado

El consentimiento predeterminado se utiliza cuando no hay ninguna preferencia de consentimiento ya guardada para un cliente. Esto significa que las opciones de consentimiento predeterminadas pueden controlar el comportamiento del SDK web de Adobe Experience Platform y cambiar según la región de un cliente.

Por ejemplo, si tiene un cliente que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado se podría establecer en `in`, pero dentro de la jurisdicción del RGPD, el consentimiento predeterminado podría establecerse en `pending`. La plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK.

### Configuración del consentimiento cuando cambia

El SDK web de Adobe Experience Platform tiene un `setConsent` , que comunica las preferencias de consentimiento del cliente a todos los servicios de Adobe mediante IAB TCF 2.0. Si se integra con Real-Time CDP, se actualiza el perfil del cliente. Si se integra con Audience Manager, se actualiza la información del cliente. Al llamar a esto también se establece una cookie con una preferencia de consentimiento de todo o nada que controla si se permite el envío de futuros eventos de experiencia. Se pretende que se llame a esta acción cada vez que cambie el consentimiento. En cargas de páginas futuras, se leerá la cookie de consentimiento de Experience Edge para determinar si se pueden enviar eventos de experiencia y si se puede establecer una cookie de identidad.

De forma similar a la integración IAB TCF 2.0 de Audience Manager, Experience Edge da su consentimiento cuando un cliente ha dado su consentimiento explícito para los siguientes fines:

- **Objetivo 1:** Almacenar o acceder a información en un dispositivo
- **Objetivo 10:** Desarrollar y mejorar productos
- **Objetivo especial 1:** Garantice la seguridad, evite el fraude y depure. (Según las regulaciones del TCF de IAB, esto siempre se acepta)
- **Permiso de proveedor de Adobe:** Consentimiento de Adobe (proveedor 565)

Para obtener más información sobre `setConsent` , lea la documentación sobre [Consentimiento de apoyo](../../consent/supporting-consent.md).

### Añadir el consentimiento a los eventos de experiencia

El SDK web de Adobe Experience Platform tiene un `sendEvent` que recopila un evento de experiencia. Si está realizando la integración con Eventos de experiencia o Adobe Analytics y desea conocer las preferencias de consentimiento de cada Evento de experiencia, debe añadir la información de consentimiento a cada `sendEvent` comando.

Para obtener más información sobre `sendEvent` , lea la documentación sobre [seguimiento de eventos](../../fundamentals/tracking-events.md).

## Pasos siguientes

Ahora que tiene una comprensión básica del marco de transparencia y consentimiento IAB 2.0, consulte cualquiera de las guías sobre el uso de IAB TCF 2.0 [con etiquetas](./with-launch.md) o [sin etiquetas](./without-launch.md).
