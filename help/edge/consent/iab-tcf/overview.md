---
title: Información general sobre Transparencia y Consentimiento de IAB 2.0
seo-title: Compatibilidad con las preferencias de consentimiento del SDK web de Adobe Experience Platform de Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Obtenga información sobre cómo admitir las preferencias de consentimiento TCF 2.0 de IAB con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo admitir las preferencias de consentimiento TCF 2.0 de IAB con el SDK web de Experience Platform
keywords: consentimiento;setConsent;Perfil Privacy Mixin;Experience Evento Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Perfil
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# Información general sobre Transparencia y Consentimiento de IAB 2.0

El SDK web de Adobe Experience Platform es compatible con la versión 2.0 de Transparencia y Consentimiento de la agencia de publicidad interactiva (IAB TCF 2.0). En esta guía se muestran los requisitos para la compatibilidad con IAB TCF 2.0 a través del SDK web de Adobe Experience Platform que se integra con la plataforma de datos del cliente en tiempo real, el Audience Manager, los Eventos de experiencias, Adobe Analytics y Experience Edge.

Además, las siguientes guías están disponibles para ayudar a aprender a integrar IAB TCF 2.0 con y sin Adobe Experience Platform Launch.

- [Con Adobe Experience Platform Launch](./with-launch.md)
- [Sin Adobe Experience Platform Launch](./without-launch.md)

## Primeros pasos

Para implementar el SDK web con IAB TCF 2.0, es necesario tener una comprensión práctica del Modelo de datos de experiencia (XDM) y los Eventos de experiencia. Antes de su inicio, consulte los siguientes documentos:

- [Descripción general](../../../xdm/home.md) del sistema del modelo de datos de experiencia (XDM): La estandarización y la interoperabilidad son conceptos clave para Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

## Integración de Experience Platform

Para enviar datos de consentimiento a Adobe Experience Platform mediante el SDK, se requiere lo siguiente:

- Un conjunto de datos cuyo esquema se basa en la clase [!DNL XDM Individual Profile] y contiene los campos de consentimiento TCF 2.0, habilitados para su uso en [!DNL Real-time Customer Profile].
- Una configuración de Edge configurada con Platform y el conjunto de datos habilitado para Perfil mencionado anteriormente.

Consulte la guía sobre [conformidad con TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener instrucciones sobre cómo crear los conjuntos de datos y la configuración de Edge necesarios.

## Integración de Audience Manager

Adobe Audience Manager (AAM) incluye compatibilidad con IAB TCF 2.0, que le permite evaluar, honrar y reenviar las opciones de privacidad de los clientes a los socios de flujo descendente. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrarlo con Audience Manager a través del SDK web de Adobe Experience Platform, asegúrese de tener una configuración de Edge configurada para reenviar a Adobe Audience Manager.

## Eventos de experiencias e integración con Adobe Analytics

Mientras que las audiencias CDP y Audience Manager en tiempo real realizan un seguimiento de las preferencias de consentimiento actuales de un cliente, los Eventos de experiencia pueden tener las preferencias de consentimiento del cliente que estaban activas cuando se recopiló el evento.

Para reunir información sobre el consentimiento de los eventos, se requiere lo siguiente:

- Un conjunto de datos basado en la clase [!DNL XDM Experience Event], con la combinación de privacidad [!DNL Experience Event].
- Una configuración de Edge configurada con el conjunto de datos [!DNL XDM Experience Event] anterior.

Para obtener más información sobre cómo convertir un Evento de experiencias XDM en una visita de Analytics, consulte el inicio [Información general de Analytics](../../data-collection/adobe-analytics/analytics-overview.md).

## Integración con Adobe Experience Platform Web SDK

Las secciones siguientes describen los principales puntos de integración entre IAB TCF 2.0 y Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Incluso sin CDP en tiempo real o Audience Manager configurado, aún puede integrar IAB TCF 2.0 con el SDK web. Las preferencias de consentimiento pueden utilizarse para controlar la colección de Eventos de experiencias y configurar una cookie de identidad.

### Consentimiento predeterminado

El consentimiento predeterminado se utiliza cuando no hay ninguna preferencia de consentimiento ya guardada para un cliente. Esto significa que las opciones de consentimiento predeterminadas pueden controlar el comportamiento del SDK web de Adobe Experience Platform y cambiar según la región del cliente.

Por ejemplo: si tiene un cliente que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`, pero dentro de la jurisdicción del RGPD, el consentimiento predeterminado podría establecerse en `pending`. Su plataforma de administración en la nube (CMP) podría detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK.

### Configuración del consentimiento cuando cambia

Adobe Experience Platform Web SDK tiene un comando `setConsent` que comunica las preferencias de consentimiento del cliente a todos los servicios de Adobe mediante IAB TCF 2.0. Si se integra con CDP en tiempo real, esto actualiza el perfil de su cliente. Si está realizando la integración con Audience Manager, esto actualiza la información del cliente. Al llamar a esto también se establece una cookie con una preferencia de consentimiento de todo o nada que controla si se permite el envío de futuros Eventos de experiencias. Se pretende que esta acción se llame siempre que cambie el consentimiento. En futuras cargas de página, se leerá la cookie de consentimiento de Experience Edge para determinar si se pueden enviar Eventos de experiencia y si se puede configurar una cookie de identidad.

De forma similar a la integración de Audience Manager IAB TCF 2.0, Experience Edge da su consentimiento cuando un cliente ha dado su consentimiento explícito para los siguientes fines:

- **Objetivo 1:** Almacenar y/o acceder a información en un dispositivo
- **Objetivo 10:** Desarrollar y mejorar productos
- **Objetivo especial 1:** Garantizar la seguridad, evitar fraudes y depurar. (De acuerdo con las regulaciones del TCF de la IAB, siempre se acepta)
- **Permiso de proveedor de Adobe:** Consentimiento de Adobe (proveedor 565)

Para obtener más información sobre el comando `setConsent`, lea la documentación sobre [Consentimiento de soporte](../../consent/supporting-consent.md).

### Añadir el consentimiento a Eventos de experiencias

Adobe Experience Platform Web SDK tiene un comando `sendEvent` que recopila un Evento de experiencias. Si está realizando la integración con Eventos de experiencias o Adobe Analytics y desea obtener las preferencias de consentimiento en cada Evento de experiencias, debe agregar la información de consentimiento a cada comando `sendEvent`.

Para obtener más información sobre el comando `sendEvent`, lea la documentación sobre [eventos de seguimiento](../../fundamentals/tracking-events.md).

## Pasos siguientes

Ahora que tiene una comprensión básica de IAB Transparency &amp; Consent Framework 2.0, consulte cualquiera de las guías sobre el uso de IAB TCF 2.0 [con Adobe Experience Platform Launch](./with-launch.md) o [sin Adobe Experience Platform Launch](./without-launch.md).
