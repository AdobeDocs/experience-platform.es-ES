---
keywords: Experience Platform;inicio;temas populares;asignación de destino;Asignación de destino
solution: Experience Platform
title: Asignación de datos de Evento de Adobe Target a XDM
topic: overview
description: Obtenga información sobre cómo asignar campos de evento de Adobe Target a un esquema de modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Asignaciones de campos de asignación de destino

Adobe Experience Platform le permite ingestar datos de Adobe Target a través del conector de origen de Destinatario. Al utilizar el conector, todos los datos de los campos de Destinatario deben asignarse a los campos [Modelo de datos de experiencia (XDM)](../../../../xdm/home.md) asociados a la clase XDM ExperienceEvent.

La siguiente tabla describe los campos de un esquema de Experience Evento (*campo XDM ExperienceEvent*) y los campos de Destinatario correspondientes a los que deben asignarse (*campo Solicitud de Destinatario*). También se proporcionan notas adicionales para algunas asignaciones.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Campo ExperienceEvent de XDM | Campo Solicitud de destinatario | Notas |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identificador de solicitud único |
| **`dataSource`** |  | Configurado en &quot;1&quot; para todos los clientes. |
| `dataSource._id` | Un valor generado por el sistema que no se puede pasar con la solicitud. | ID única de esta fuente de datos. Esto lo proporcionaría el individuo o el sistema que creó la fuente de datos. |
| `dataSource.code` | Un valor generado por el sistema que no se puede pasar con la solicitud. | Un acceso directo al @id completo. Se puede usar al menos uno de los códigos o @id. A veces, este código se denomina código de integración de fuentes de datos. |
| `dataSource.tags` | Un valor generado por el sistema que no se puede pasar con la solicitud. | Las etiquetas se utilizan para indicar cómo las aplicaciones que utilizan esos alias deben interpretar los alias representados por una fuente de datos determinada.<br><br>Ejemplos:<br><ul><li>`isAVID`:: Fuentes de datos que representan ID de visitante de Analytics.</li><li>`isCRSKey`:: Fuentes de datos que representan alias que deben utilizarse como claves en CRS.</li></ul>Las etiquetas se establecen cuando se crea la fuente de datos, pero también se incluyen en los mensajes de canalización al hacer referencia a una fuente de datos determinada. |
| **`timestamp`** | Marca de hora de evento |
| **`channel`** | `context.channel` | Solo funciona con envío de vista. Las opciones son &quot;web&quot; y &quot;mobile&quot;, siendo &quot;web&quot; el valor predeterminado. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | El nombre del operador de telefonía móvil se resolvió en función de la dirección IP de la solicitud. |
| `environment.ipV4` | `mboxRequest.ipAddress` (si está en formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (si está en formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Asignación interna de destinatario para entornos definidos por el cliente (como dev, qa o prod). |
| `experience.target.supplementalDataID` | Identificador que se utiliza para unir eventos de Destinatario con eventos de Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matriz) de actividades para las que el visitante ha calificado |
| `experience.target.activities[i].activityID` | ID de cualquier actividad determinada para la que el visitante esté cualificado |
| `experience.target.activities[i].version` | Versión de cualquier actividad determinada para la que el visitante esté cualificado |
| `experience.target.activities[i].activityEvents` | Incluye los detalles de los eventos de actividad que el usuario ha alcanzado con este evento. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Una de las siguientes propiedades de `deviceAtlas` (o NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (cadena vacía) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (cadena vacía) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID aleatorio (obligatorio) |
| `placeContext.geo.city` | El nombre de la ciudad se resolvió en función de la dirección IP de la solicitud. |
| `placeContext.geo.countryCode` | Código de país resuelto en función de la dirección IP de la solicitud. |
| `placeContext.geo.dmaId` | El código de área de mercado designado se ha resuelto en función de la dirección IP de la solicitud. |
| `placeContext.geo.postalCode` | El código postal se resolvió en función de la dirección IP de la solicitud. |
| `placeContext.geo.stateProvince` | Estado o provincia resuelto en función de la dirección IP de la solicitud. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Solo se establece si los detalles del pedido están presentes en la solicitud. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
