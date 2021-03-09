---
title: Tipos de acción en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de acción proporcionados por la extensión web SDK de Adobe Experience Platform en Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---


# Tipos de acción

Después de configurar la [extensión del SDK web de Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure los tipos de acción.

Esta página describe los tipos de acción disponibles.

## Enviar evento

Envía un evento a Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar en consecuencia. Seleccione una instancia (si tiene más de una). Si el evento se produce al principio de una carga de página o durante un cambio de vista en una aplicación de una sola página, seleccione **[!UICONTROL Ocurrencias al principio de una vista]**.

Los datos que desee enviar se pueden enviar en el campo **[!UICONTROL XDM Data]**. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Definir consentimiento

Una vez que haya recibido el consentimiento del usuario, este consentimiento debe comunicarse al SDK web de Adobe Experience Platform mediante el tipo de acción &quot;Definir consentimiento&quot;. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Compatibilidad con las preferencias de consentimiento del cliente](../consent/supporting-consent.md). Al utilizar Adobe versión 2.0, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporcionará un campo opcional para incluir un mapa de identidad de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como &quot;Pendiente&quot; o &quot;Fuera&quot; porque es probable que la llamada de consentimiento sea la primera llamada a activar.

## Restablecer ID de combinación de eventos

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, seleccione el ID de combinación que desee restablecer y active la acción según sea necesario.

## Siguientes pasos

Después de establecer los tipos de acción, [configure los tipos de elementos de datos](data-element-types.md).