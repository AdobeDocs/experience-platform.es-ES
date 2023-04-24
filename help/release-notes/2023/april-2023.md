---
title: Notas de la versión de Adobe Experience Platform, abril de 2023
description: Notas de la versión de abril de 2023 para Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 26 de abril de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Preparación de datos](#data-prep)
- [Fuentes](#sources)

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones del periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción | El periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción se ha reducido a tres meses. El relleno de los entornos limitados de producción sigue siendo el mismo a los 13 meses. Este cambio solo se aplica a los flujos nuevos y no afecta a los flujos existentes. Para obtener más información, lea la [Información general de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nueva función de asignación para convertir cadenas FPID en ECID | Utilice la variable `fpid_to_ecid` para convertir cadenas FPID en ECID para su uso en aplicaciones de Experience Platform y Experience Cloud. Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad de API para filtrar datos de nivel de fila para Microsoft Dynamics, Salesforce CRM y el Marketing Cloud de Salesforce | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para los orígenes de Marketing Cloud de Microsoft Dynamics, Salesforce CRM y Salesforce. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |
| Disponibilidad beta de Shopify Streaming | La variable [Origen de flujo de Shopify](../../sources/connectors/ecommerce/shopify-streaming.md) ya está disponible en versión beta. Utilice la fuente de Shopify Streaming para transmitir los datos de su cuenta de socios de Shopify al Experience Platform. |
| Disponibilidad general de OneTrust Integration | La variable [Origen de integración de OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) es ahora GA. Utilice la fuente de integración de OneTrust para llevar los datos de consentimiento y preferencias de su cuenta de integración de OneTrust al Experience Platform. |
| Disponibilidad general de Oracle Service Cloud | La variable [Origen de nube de servicio de oracle](../../sources/connectors/customer-success/oracle-service-cloud.md) es ahora GA. Utilice el origen de nube de servicio de Oracle para llevar los datos de nube de servicio de Oracle al Experience Platform. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
