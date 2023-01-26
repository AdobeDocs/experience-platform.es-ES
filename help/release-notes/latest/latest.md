---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: aabf715475b3634ef134226f67b722f84e830556
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 23 de noviembre de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [!DNL AWS] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Amazon Web Services] ([!DNL AWS]) usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL AWS] información general de la extensión](../../tags/extensions/server/aws/overview.md) para obtener más información. |
| [!DNL Google Ads Enhanced Conversions] extensión para el reenvío de eventos | Ahora puede enviar datos de conversión a [!DNL Google Ads] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Google Ads Enhanced Conversions] información general de la extensión](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obtener más información. |
| [!DNL Microsoft Azure] extensión para el reenvío de eventos | Ahora puede enviar datos a [!DNL Microsoft Azure] usando un [reenvío de eventos](../../tags/ui/event-forwarding/overview.md) extensión. Consulte la [[!DNL Microsoft Azure] información general de la extensión](../../tags/extensions/server/azure/overview.md) para obtener más información. |

Para obtener más información sobre las capacidades de recopilación de datos de Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Asignar campos a clases personalizadas al agregarlos directamente a un esquema | When [adición de un campo individual directamente a un esquema](../../xdm/ui/resources/schemas.md#add-individual-fields), anteriormente solo se podía asignar el campo a un grupo de campos como recurso principal. Ahora, además de los grupos de campos, puede [asignar el campo a una clase personalizada](../../xdm/ui/resources/schemas.md#add-to-class) como su recurso principal en su lugar. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- | 
| Disponibilidad beta del origen de Oracle Service Cloud | Utilice la fuente de nube de servicio de Oracle para ingerir los datos de su cuenta de Oracle Service Cloud en Experience Platform. Para obtener más información, consulte la documentación de [Origen de nube de servicio de oracle](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
