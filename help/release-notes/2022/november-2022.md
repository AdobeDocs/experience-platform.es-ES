---
title: Notas de la versión de noviembre de 2022 de Adobe Experience Platform
description: Las notas de la versión de noviembre de 2022 de Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 63%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: jueves, 23 de noviembre de 2022**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Extensión [!DNL AWS] para el reenvío de eventos | Ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL AWS] información general sobre las extensiones](../../tags/extensions/server/aws/overview.md) para obtener más detalles. |
| Extensión [!DNL Google Ads Enhanced Conversions] para el reenvío de eventos | Ahora puede enviar datos de conversión a [!DNL Google Ads] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Google Ads Enhanced Conversions] información general sobre las extensiones](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más detalles. |
| Extensión [!DNL Microsoft Azure] para el reenvío de eventos | Ahora puede enviar datos a [!DNL Microsoft Azure] mediante una extensión de [reenvío de eventos](../../tags/ui/event-forwarding/overview.md). Consulte la [[!DNL Microsoft Azure] información general sobre las extensiones](../../tags/extensions/server/azure/overview.md) para obtener más detalles. |

Para obtener más información sobre las capacidades de recopilación de datos de Experience Platform, consulte la [descripción general de la recopilación de datos](../../collection/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Asignar campos a clases personalizadas al agregar directamente a un esquema | Al [agregar un campo individual directamente a un esquema](../../xdm/ui/resources/schemas.md#add-individual-fields), anteriormente solo podía asignar el campo a un grupo de campos como su recurso principal. Ahora, además de los grupos de campos, puede [asignar el campo a una clase personalizada](../../xdm/ui/resources/schemas.md#add-to-class) como su recurso principal. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).
