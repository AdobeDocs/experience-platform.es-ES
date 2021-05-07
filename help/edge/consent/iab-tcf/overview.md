---
title: Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento TCF 2.0 de IAB mediante el SDK web de Adobe Experience Platform
keywords: consentimiento;setConsent;grupo Campo de privacidad de perfil;grupo Campo de privacidad de evento de experiencia;grupo Campo de privacidad;IAB TCF 2.0;CDP en tiempo real;Perfil de datos del cliente en tiempo real
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es compatible con el marco de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0). Esta guía muestra los requisitos para la compatibilidad con IAB TCF 2.0 mediante la integración del SDK web de Adobe Experience Platform con la plataforma de datos del cliente en tiempo real, el Audience Manager, los eventos de experiencia, Adobe Analytics y Experience Edge.

Además, las siguientes guías están disponibles para ayudarle a aprender a integrar IAB TCF 2.0 con y sin Adobe Experience Platform Launch.

- [Con Adobe Experience Platform Launch](./with-launch.md)
- [Sin Adobe Experience Platform Launch](./without-launch.md)

## Primeros pasos

Para implementar el SDK web con IAB TCF 2.0, es necesario tener una comprensión práctica del modelo de datos de experiencia (XDM) y los eventos de experiencia. Antes de comenzar, revise el siguiente documento:

- [Descripción general del sistema del Modelo de datos de experiencia (XDM)](../../../xdm/home.md): La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## Integración de Experience Platform

Para enviar datos de consentimiento a Adobe Experience Platform mediante el SDK, se requiere lo siguiente:

- Conjunto de datos cuyo esquema se basa en la clase [!DNL XDM Individual Profile] y contiene campos de consentimiento TCF 2.0, habilitados para su uso en [!DNL Real-time Customer Profile].
- Una configuración perimetral configurada con Platform y el conjunto de datos habilitado para perfil mencionado anteriormente.

Consulte la guía de [conformidad con TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener instrucciones sobre la creación de los conjuntos de datos y la configuración perimetral necesarios.

## Integración de Audience Manager

Adobe Audience Manager (AAM) incluye compatibilidad con IAB TCF 2.0, que le permite evaluar, cumplir y reenviar las opciones de privacidad del cliente a los socios descendentes. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrarse con Audience Manager a través del SDK web de Adobe Experience Platform, asegúrese de que tiene una configuración edge configurada para reenviar a Adobe Audience Manager.

## Integración de Experience Events y Adobe Analytics

Mientras que las audiencias de CDP en tiempo real y de Audience Manager realizan un seguimiento de las preferencias de consentimiento actuales de un cliente, Experience Events puede mantener las preferencias de consentimiento de un cliente que estaban activas cuando se recopiló el evento.

Para recopilar información de consentimiento sobre eventos, se requiere lo siguiente:

- Un conjunto de datos basado en la clase [!DNL XDM Experience Event], con el grupo de campos [!DNL Experience Event] privacy schema .
- Una configuración de Edge configurada con el conjunto de datos [!DNL XDM Experience Event] anterior.

Para obtener más información sobre cómo convertir un Evento de experiencia XDM en una visita de Analytics, comience leyendo la documentación [Información general de Analytics](../../data-collection/adobe-analytics/analytics-overview.md).

## Integración del SDK web de Adobe Experience Platform

Las secciones siguientes describen los principales puntos de integración entre IAB TCF 2.0 y el SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Incluso sin CDP en tiempo real o sin configuración de Audience Manager, aún puede integrar IAB TCF 2.0 con el SDK web. Las preferencias de consentimiento se pueden utilizar para controlar la recopilación de eventos de experiencias y configurar una cookie de identidad.

### Consentimiento predeterminado

El consentimiento predeterminado se utiliza cuando no hay preferencias de consentimiento ya guardadas para un cliente. Esto significa que las opciones de consentimiento predeterminadas pueden controlar el comportamiento del SDK web de Adobe Experience Platform y cambiar según la región del cliente.

Por ejemplo, si tiene un cliente que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`, pero dentro de la jurisdicción del RGPD, el consentimiento predeterminado podría establecerse en `pending`. Su plataforma de administración de consentimiento (CMP) podría detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK.

### Configuración del consentimiento cuando cambia

El SDK web de Adobe Experience Platform tiene un comando `setConsent`, que comunica las preferencias de consentimiento del cliente a todos los servicios de Adobe mediante IAB TCF 2.0. Si se integra con CDP en tiempo real, esto actualiza el perfil del cliente. Si está integrando con Audience Manager, esto actualiza la información de su cliente. Llamar a esto también establece una cookie con una preferencia de consentimiento de todo o nada que controla si se permite el envío de eventos de experiencia futuros. Se pretende que esta acción se llame siempre que cambie el consentimiento. En futuras cargas de página, se leerá la cookie de consentimiento de Experience Edge para determinar si se pueden enviar eventos de experiencia y si se puede configurar una cookie de identidad.

Al igual que la integración de IAB TCF 2.0 de Audience Manager, Experience Edge da su consentimiento cuando un cliente ha dado su consentimiento explícito para los siguientes fines:

- **Objetivo 1:** Almacenar y/o acceder a información en un dispositivo
- **Objetivo 10:** Desarrollar y mejorar productos
- **Objetivo especial 1:** Garantizar la seguridad, evitar el fraude y depurar. (De acuerdo con las regulaciones del TCF de la IAB, siempre se acepta)
- **Permiso de proveedor de Adobe:** consentimiento para el Adobe (proveedor 565)

Para obtener más información sobre el comando `setConsent`, lea la documentación sobre [Consentimiento de soporte](../../consent/supporting-consent.md).

### Añadir consentimiento a eventos de experiencias

El SDK web de Adobe Experience Platform tiene un comando `sendEvent` que recopila un Evento de experiencia. Si está integrando con Experience Events o Adobe Analytics y desea las preferencias de consentimiento para cada Evento de experiencia, debe agregar la información de consentimiento a cada comando `sendEvent`.

Para obtener más información sobre el comando `sendEvent`, lea la documentación sobre [seguimiento de eventos](../../fundamentals/tracking-events.md).

## Pasos siguientes

Ahora que tiene una comprensión básica del marco de transparencia y consentimiento IAB 2.0, consulte cualquiera de las guías sobre el uso de IAB TCF 2.0 [con Adobe Experience Platform Launch](./with-launch.md) o [sin Adobe Experience Platform Launch](./without-launch.md).
