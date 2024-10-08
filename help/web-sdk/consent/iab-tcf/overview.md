---
title: Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento de IAB TCF 2.0 mediante el SDK web de Adobe Experience Platform
keywords: consentimiento;setConsent;Grupo de campos de privacidad de perfil;Grupo de campos de privacidad de evento de experiencia;Grupo de campos de privacidad;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en el SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es compatible con el marco interactivo de transparencia y consentimiento de Advertising Bureau, versión 2.0 (IAB TCF 2.0). Esta guía muestra los requisitos para admitir IAB TCF 2.0 a través de la integración del SDK web de Adobe Experience Platform con Adobe Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics y Edge Network.

Además, las siguientes guías están disponibles para ayudarle a aprender a integrar IAB TCF 2.0 con y sin etiquetas.

- [Con etiquetas](./with-tags.md)
- [Sin etiquetas](./without-tags.md)

## Introducción

Para implementar el SDK web con IAB TCF 2.0, se necesita una comprensión práctica del Modelo de datos de experiencia (XDM) y los Eventos de experiencia. Antes de empezar, revise el siguiente documento:

- [Descripción general del sistema Experience Data Model (XDM)](../../../xdm/home.md): la estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## Integración de Experience Platform

Para enviar datos de consentimiento a Adobe Experience Platform mediante el SDK, se requiere lo siguiente:

- Un conjunto de datos cuyo esquema se basa en la clase [!DNL XDM Individual Profile] y contiene campos de consentimiento TCF 2.0, habilitados para su uso en [!DNL Real-Time Customer Profile].
- Un conjunto de datos configurado con Platform y el conjunto de datos habilitado para perfil mencionado anteriormente.

Consulte la guía sobre el [cumplimiento de TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener instrucciones sobre cómo crear los conjuntos de datos y la secuencia de datos necesarios.

## Integración de Audience Manager

Adobe Audience Manager AAM () incluye compatibilidad con IAB TCF 2.0, que le permite evaluar, cumplir y reenviar las opciones de privacidad del cliente a socios comerciales. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrarse con Audience Manager a través del SDK web de Adobe Experience Platform, asegúrese de tener configurado un conjunto de datos para reenviar a Adobe Audience Manager.

## Integración de Experience Events y Adobe Analytics

Mientras que las audiencias de Real-Time CDP y Audience Manager realizan un seguimiento de las preferencias de consentimiento actuales de un cliente, los eventos de experiencia pueden contener las preferencias de consentimiento de un cliente que estaban activas cuando se recopiló el evento.

Para recopilar información de consentimiento sobre eventos, se requiere lo siguiente:

- Un conjunto de datos basado en la clase [!DNL XDM Experience Event], con el grupo de campos de esquema de privacidad [!DNL Experience Event].
- Flujo de datos configurado con el conjunto de datos [!DNL XDM Experience Event] anterior.

Para obtener más información sobre cómo convertir un evento de experiencia XDM en una visita de Analytics, consulte [Envío de datos a Adobe Analytics mediante el SDK web](/help/web-sdk/use-cases/adobe-analytics.md).

## Integración del SDK web de Adobe Experience Platform

Las secciones siguientes describen los principales puntos de integración entre IAB TCF 2.0 y el SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Incluso sin Real-Time CDP o Audience Manager configurados, puede integrar IAB TCF 2.0 con el SDK web. Las preferencias de consentimiento se pueden utilizar para controlar la recopilación de eventos de experiencia y configurar una cookie de identidad.

### Consentimiento predeterminado

El consentimiento predeterminado se utiliza cuando no hay ninguna preferencia de consentimiento ya guardada para un cliente. Esto significa que las opciones de consentimiento predeterminadas pueden controlar el comportamiento del SDK web de Adobe Experience Platform y cambiar según la región de un cliente.

Por ejemplo, si tiene un cliente que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`, pero dentro de la jurisdicción del RGPD, el consentimiento predeterminado podría establecerse en `pending`. Su plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado. Consulte [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) para obtener más información.

### Configuración del consentimiento cuando cambia

El SDK web de Adobe Experience Platform tiene un comando `setConsent`, que comunica las preferencias de consentimiento del cliente a todos los servicios de Adobe mediante IAB TCF 2.0. Si se integra con Real-Time CDP, se actualiza el perfil del cliente. Si se integra con Audience Manager, se actualiza la información del cliente. Al llamar a esto también se establece una cookie con una preferencia de consentimiento de todo o nada que controla si se permite el envío de futuros eventos de experiencia. Se pretende que se llame a esta acción cada vez que cambie el consentimiento. En cargas de páginas futuras, se lee la cookie de consentimiento del Edge Network para determinar si se pueden enviar eventos de experiencia y si se puede configurar una cookie de identidad.

De forma similar a la integración IAB TCF 2.0 de Audience Manager, el Edge Network da su consentimiento cuando un cliente ha dado su consentimiento explícito para los siguientes fines:

- **Propósito 1:** Almacenar o acceder a información en un dispositivo
- **Objetivo 10:** Desarrollar y mejorar productos
- **Propósito especial 1:** Garantizar la seguridad, evitar el fraude y depurar. (Según las regulaciones del TCF de IAB, esto siempre se acepta)
- **Permiso de proveedor de Adobe:** Consentimiento para Adobe (Proveedor 565)

Para obtener más información sobre el comando `setConsent`, lea la documentación del SDK web dedicada en [setConsent](../../../web-sdk/commands/setconsent.md).

### Añadir el consentimiento a los eventos de experiencia

El SDK web de Adobe Experience Platform tiene un comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) que recopila un evento de experiencia. Si está realizando la integración con Eventos de experiencia o Adobe Analytics y desea conocer las preferencias de consentimiento de cada Evento de experiencia, agregue información de consentimiento a cada comando de `sendEvent`.

## Pasos siguientes

Ahora que tiene una comprensión básica del marco de transparencia y consentimiento IAB 2.0, consulte cualquiera de las guías sobre el uso de IAB TCF 2.0 [con etiquetas](./with-tags.md) o [sin etiquetas](./without-tags.md).
