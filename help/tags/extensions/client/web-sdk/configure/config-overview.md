---
title: Información general sobre ajustes de configuración
description: Obtenga información sobre las opciones disponibles al configurar la extensión de etiquetas Web SDK.
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Información general sobre ajustes de configuración

La extensión de etiquetas Adobe Experience Platform Web SDK proporciona varias opciones que se pueden personalizar. Estas opciones de configuración son el equivalente de etiqueta de usar el comando [`configure`](/help/collection/js/commands/configure/overview.md) en la biblioteca de JavaScript.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].

## Componentes de compilación personalizados

Si la optimización del tamaño de la compilación es una prioridad para su organización, puede deshabilitar determinadas funciones que no utiliza para reducir el tamaño de compilación de la extensión. Consulte [Componentes de compilación personalizada](custom-build-components.md) para obtener más información.

## Instancias de SDK

La mayoría de las implementaciones suelen necesitar una sola instancia de SDK. Sin embargo, si su organización requiere varias instancias de seguimiento de Web SDK, puede utilizar el botón **[!UICONTROL Add instance]**. Las siguientes secciones generales están disponibles al configurar cada instancia de etiqueta de Web SDK:

* [**[!UICONTROL SDK instance]**](general.md): configuración general de la instancia. Todos los campos de esta sección son obligatorios.
* [**[!UICONTROL Datastreams]**](datastreams.md): adónde desea que vayan los datos para cada entorno de etiquetas.
* [**[!UICONTROL Consent]**](consent.md): configuración de consentimiento predeterminada para la extensión.
* [**[!UICONTROL Identity]**](identity.md): configuración de migración de cookies y visitantes.
* [**[!UICONTROL Personalization]**](personalization.md): personalizar la experiencia del visitante en un nivel individual.
* [**[!UICONTROL Data collection]**](data-collection.md): incluir u omitir lo que se recopila automáticamente.
* [**[!UICONTROL Streaming media]**](streaming-media.md): configuración específica de la recopilación de medios de streaming.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): modifique las opciones de configuración cuando se cumplan determinadas condiciones.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): especifique la ruta de acceso base para Edge Network.
