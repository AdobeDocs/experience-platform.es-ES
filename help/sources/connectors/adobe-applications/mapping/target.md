---
solution: Experience Platform
title: Asignación de datos de evento de Adobe Target a XDM
description: Obtenga información sobre cómo asignar campos de evento de Adobe Target a un esquema de modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Asignaciones de campo de asignación de destino

En la tabla siguiente se describen los campos de un esquema de evento de experiencia del modelo de datos de experiencia (XDM) y los campos correspondientes de Adobe Target a los que se deben asignar. También se proporcionan notas adicionales para algunas asignaciones.

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para ver todo el contenido de la tabla.

| Campo de ExperienceEvent de XDM | Campo de solicitud de destino | Notas |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identificador de solicitud único |
| **`dataSource`** | | Configurado en &quot;1&quot; para todos los clientes. |
| `dataSource._id` | Un valor generado por el sistema que no se puede pasar con la solicitud. | El ID único de esta fuente de datos. Esto lo proporciona la persona o sistema que creó la fuente de datos. |
| `dataSource.code` | Un valor generado por el sistema que no se puede pasar con la solicitud. | Un acceso directo al @id completo. Se puede utilizar al menos uno de los códigos o @id. En ocasiones, este código se denomina código de integración de la fuente de datos. |
| `dataSource.tags` | Un valor generado por el sistema que no se puede pasar con la solicitud. | Las etiquetas se utilizan para indicar cómo las aplicaciones que utilizan los alias representados por una fuente de datos determinada deben interpretarlos.<br><br>Ejemplos:<br><ul><li>`isAVID`: Fuentes de datos que representan los ID de visitante de Analytics.</li><li>`isCRSKey`: fuentes de datos que representan alias que deben utilizarse como claves en CRS.</li></ul>Las etiquetas se establecen cuando se crea la fuente de datos, pero también se incluyen en los mensajes de canalización al hacer referencia a una fuente de datos determinada. |
| **`timestamp`** | Marca de tiempo del evento |
| **`channel`** | `context.channel` | Solo funciona con la entrega de vista. Las opciones son &quot;web&quot; y &quot;móvil&quot;, siendo &quot;web&quot; la predeterminada. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | El ID del Experience Cloud (ECID) también se conoce como MCID y sigue utilizándose en áreas de nombres. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | El nombre del operador de telefonía móvil se resuelve en función de la dirección IP de la solicitud. |
| `environment.ipV4` | `mboxRequest.ipAddress` (en formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (en formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Asignación interna de Target para entornos definidos por el cliente (como dev, qa o prod). |
| `experience.target.supplementalDataID` | Identificador utilizado para unir eventos de Target con eventos de Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matriz) de actividades para las que el visitante cumple los requisitos |
| `experience.target.activities[i].activityID` | El ID de cualquier actividad para la que el visitante cumple los requisitos |
| `experience.target.activities[i].version` | La versión de cualquier actividad para la que el visitante cumple los requisitos |
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
| `placeContext.geo.city` | Nombre de ciudad resuelto en función de la dirección IP de la solicitud. |
| `placeContext.geo.countryCode` | El código de país se resuelve en función de la dirección IP de la solicitud. |
| `placeContext.geo.dmaId` | El código de área de mercado designado se resuelve en función de la dirección IP de la solicitud. |
| `placeContext.geo.postalCode` | El código postal se resuelve en función de la dirección IP de la solicitud. |
| `placeContext.geo.stateProvince` | Estado o provincia resueltos en función de la dirección IP de la solicitud. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Se configura solo si los detalles del pedido están presentes en la solicitud. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
