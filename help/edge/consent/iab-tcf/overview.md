---
title: Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento TCF 2.0 de IAB mediante el SDK web de Adobe Experience Platform
keywords: consentimiento;setConsent;grupo Campo de privacidad de perfil;grupo Campo de privacidad de evento de experiencia;grupo Campo de privacidad;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es compatible con el marco de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0). Esta guía muestra los requisitos para admitir IAB TCF 2.0 mediante la integración del SDK web de Adobe Experience Platform con Adobe Real-time Customer Data Platform, el Audience Manager, los eventos de experiencia, Adobe Analytics y Experience Edge.

Además, las siguientes guías están disponibles para ayudarle a aprender a integrar IAB TCF 2.0 con y sin etiquetas.

- [Con etiquetas](./with-launch.md)
- [Sin etiquetas](./without-launch.md)

## Primeros pasos

Para implementar el SDK web con IAB TCF 2.0, es necesario tener una comprensión práctica del modelo de datos de experiencia (XDM) y los eventos de experiencia. Antes de comenzar, revise el siguiente documento:

- [Descripción general del sistema del Modelo de datos de experiencia (XDM)](../../../xdm/home.md): La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## Integración de Experience Platform

Para enviar datos de consentimiento a Adobe Experience Platform mediante el SDK, se requiere lo siguiente:

- Un conjunto de datos cuyo esquema se basa en la variable [!DNL XDM Individual Profile] y contiene campos de consentimiento TCF 2.0, habilitados para su uso en [!DNL Real-time Customer Profile].
- Un conjunto de datos configurado con Platform y el conjunto de datos habilitado para Perfil mencionado anteriormente.

Consulte la guía de [Cumplimiento de TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener instrucciones sobre la creación de los conjuntos de datos y el conjunto de datos necesarios.

## Integración de Audience Manager

Adobe Audience Manager (AAM) incluye compatibilidad con IAB TCF 2.0, que le permite evaluar, cumplir y reenviar las opciones de privacidad del cliente a los socios descendentes. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrarse con Audience Manager a través del SDK web de Adobe Experience Platform, asegúrese de que tiene un conjunto de datos configurado para reenviar a Adobe Audience Manager.

## Integración de Experience Events y Adobe Analytics

Mientras que las audiencias de Real-Time CDP y de Audience Manager realizan un seguimiento de las preferencias de consentimiento actuales de un cliente, Experience Events puede mantener las preferencias de consentimiento de un cliente que estaban activas cuando se recopiló el evento.

Para recopilar información de consentimiento sobre eventos, se requiere lo siguiente:

- Un conjunto de datos basado en la variable [!DNL XDM Experience Event] con la [!DNL Experience Event] grupo de campos del esquema de privacidad.
- Un conjunto de datos configurado con la variable [!DNL XDM Experience Event] conjunto de datos anterior.

Para obtener más información sobre cómo convertir un evento de experiencia XDM en una visita de Analytics, comience leyendo el [Información general de Analytics](../../data-collection/adobe-analytics/analytics-overview.md) documentación.

## Integración del SDK web de Adobe Experience Platform

Las secciones siguientes describen los principales puntos de integración entre IAB TCF 2.0 y el SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Incluso sin Real-Time CDP o Audience Manager configurado, puede integrar IAB TCF 2.0 con el SDK web. Las preferencias de consentimiento se pueden utilizar para controlar la recopilación de eventos de experiencias y configurar una cookie de identidad.

### Consentimiento predeterminado

El consentimiento predeterminado se utiliza cuando no hay preferencias de consentimiento ya guardadas para un cliente. Esto significa que las opciones de consentimiento predeterminadas pueden controlar el comportamiento del SDK web de Adobe Experience Platform y cambiar según la región del cliente.

Por ejemplo, si tiene un cliente que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`, pero dentro de la jurisdicción del RGPD, el consentimiento predeterminado podría establecerse en `pending`. Su plataforma de administración de consentimiento (CMP) podría detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK.

### Configuración del consentimiento cuando cambia

El SDK web de Adobe Experience Platform tiene un `setConsent` , que comunica las preferencias de consentimiento del cliente a todos los servicios de Adobe mediante IAB TCF 2.0. Si integra con Real-Time CDP, actualizará el perfil del cliente. Si está integrando con Audience Manager, esto actualiza la información de su cliente. Llamar a esto también establece una cookie con una preferencia de consentimiento de todo o nada que controla si se permite el envío de eventos de experiencia futuros. Se pretende que esta acción se llame siempre que cambie el consentimiento. En futuras cargas de página, se leerá la cookie de consentimiento de Experience Edge para determinar si se pueden enviar eventos de experiencia y si se puede configurar una cookie de identidad.

Al igual que la integración de IAB TCF 2.0 de Audience Manager, Experience Edge da su consentimiento cuando un cliente ha dado su consentimiento explícito para los siguientes fines:

- **Objetivo 1:** Almacenar o acceder a información en un dispositivo
- **Objetivo 10:** Desarrollar y mejorar productos
- **Objetivo especial 1:** Asegúrese de la seguridad, evite el fraude y depure. (De acuerdo con las regulaciones del TCF de la IAB, siempre se acepta)
- **Permiso de proveedor de Adobe:** Consentimiento para el Adobe (Proveedor 565)

Para obtener más información sobre `setConsent` lea la documentación en [Compatibilidad con el consentimiento](../../consent/supporting-consent.md).

### Añadir consentimiento a eventos de experiencias

El SDK web de Adobe Experience Platform tiene un `sendEvent` que recopila un evento de experiencia. Si está integrando con Experience Events o Adobe Analytics y desea preferencias de consentimiento para cada evento de experiencia, debe agregar la información de consentimiento a cada `sendEvent` comando.

Para obtener más información sobre `sendEvent` lea la documentación en [seguimiento de eventos](../../fundamentals/tracking-events.md).

## Pasos siguientes

Ahora que tiene una comprensión básica del marco de transparencia y consentimiento IAB 2.0, consulte cualquiera de las guías sobre el uso de IAB TCF 2.0 [con etiquetas](./with-launch.md) o [sin etiquetas](./without-launch.md).
