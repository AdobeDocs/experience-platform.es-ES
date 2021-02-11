---
title: Tipos de acciones de extensión del SDK web de plataforma
description: Tipos de acciones de extensión de SDK web de Adobe Experience Platform en Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---


# Tipos de acción

Después de configurar la [extensión del SDK web de Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure los tipos de acción.

Esta página describe los tipos de acciones disponibles.

## Enviar evento

Envía un evento a Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar en consecuencia. Debe seleccionar una instancia (si tiene más de una). Si el evento se produce al principio de una carga de página o durante un cambio de vista en una aplicación de una sola página, seleccione **[!UICONTROL Se produce en el inicio de una vista]**.

Los datos que desee enviar se pueden enviar en el campo **[!UICONTROL Datos XDM]**. Debe ser un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o mediante un **[!UICONTROL elemento de datos]** **[!UICONTROL Código personalizado]**.

## Definir consentimiento

Una vez que haya recibido el consentimiento de su usuario, esto debe comunicarse al SDK web de Adobe Experience Platform. Para ello, utilice el tipo de acción Definir consentimiento. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Si utiliza el estándar de Adobe, actualmente puede establecer el consentimiento como Entrada o Salida, o puede proporcionarlo mediante un elemento de datos. Si utiliza el estándar TCF de IAB, proporcione la versión y el valor que desea utilizar, así como información adicional sobre el RGPD.

En esta acción también se le proporciona un campo opcional para incluir un mapa de identidad, de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. Esto puede resultar útil cuando el consentimiento se configura como Pendiente porque la llamada de consentimiento probablemente sea la primera llamada a activación.

## Restablecer ID de combinación de eventos

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, debe seleccionar el ID de combinación que desea restablecer y activar la acción según sea necesario.

## Qué sigue

Después de configurar los tipos de acciones, [configure los tipos de elementos de datos](data-element-types.md).