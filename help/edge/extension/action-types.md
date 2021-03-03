---
title: Tipos de acción en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de acción proporcionados por la extensión web SDK de Adobe Experience Platform en Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---


# Tipos de acción

Después de configurar la [extensión del SDK web de Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure los tipos de acción.

Esta página describe los tipos de acción disponibles.

## Enviar evento

Envía un evento a Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar en consecuencia. Seleccione una instancia (si tiene más de una). Si el evento se produce al principio de una carga de página o durante un cambio de vista en una aplicación de una sola página, seleccione **[!UICONTROL Ocurrencias al principio de una vista]**.

Los datos que desee enviar se pueden enviar en el campo **[!UICONTROL XDM Data]**. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Definir consentimiento

Una vez que haya recibido el consentimiento del usuario, este consentimiento debe comunicarse al SDK web de Adobe Experience Platform mediante el tipo de acción &quot;Definir consentimiento&quot;. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Si utiliza el estándar de Adobe, actualmente puede establecer el consentimiento como Entrada o Salida, o puede proporcionarlo mediante un elemento de datos. Si utiliza el estándar TCF de IAB, proporcione la versión y el valor que desea utilizar, así como información adicional sobre el RGPD.

En esta acción, también se le proporcionará un campo opcional para incluir un mapa de identidad de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como &quot;Pendiente&quot; porque es probable que la llamada de consentimiento sea la primera llamada a activarse.

## Restablecer ID de combinación de eventos

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, seleccione el ID de combinación que desee restablecer y active la acción según sea necesario.

## Siguientes pasos

Después de establecer los tipos de acción, [configure los tipos de elementos de datos](data-element-types.md).