---
title: Notas de la versión de Adobe Experience Platform, abril de 2023
description: Notas de la versión de abril de 2023 para Adobe Experience Platform.
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 26 de abril de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Tableros](#dashboards)
- [Preparación de datos](#data-prep)
- [Modelo de datos de experiencia](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Fuentes](#sources)

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Tableros definidos por el usuario | Ahora puede **filtrar datos históricos** desde la información del widget, y utilice datos recientes o un período de análisis personalizado.<br>Ahora también puede **duplicar las utilidades existentes**. Al personalizar un duplicado y editar sus atributos, puede evitar reiniciar desde el principio al crear un nuevo widget único. |

{style="table-layout:auto"}

Para obtener más información sobre los tableros, incluido cómo conceder permisos de acceso y crear utilidades personalizadas, comience por leer [información general sobre los paneles](../../dashboards/home.md).

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones del periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción | El periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción se ha reducido a tres meses. El relleno de los entornos limitados de producción sigue siendo el mismo a los 13 meses. Este cambio solo se aplica a los flujos nuevos y no afecta a los flujos existentes. Para obtener más información, lea la [Información general de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nueva función de asignación para convertir cadenas FPID en ECID | Utilice la variable `fpid_to_ecid` para convertir cadenas FPID en ECID para su uso en aplicaciones de Experience Platform y Experience Cloud. Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mostrar nombres, alternador | El Editor de esquemas ahora proporciona un interruptor para cambiar entre los nombres de campo originales y los nombres para mostrar más legibles. Esta flexibilidad permite mejorar la capacidad de detección de campos y la edición de los esquemas. Los nombres para mostrar de los grupos de campos estándar se generan a partir del sistema, pero también se pueden personalizar a través de la interfaz de usuario si es necesario. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Caducidad de datos de perfil seudónimos | Ya está disponible la caducidad de los datos del perfil seudónimos. Esta versión eliminará continuamente perfiles seudónimos antiguos de la instancia de Experience Platform una vez que se haya activado. Para obtener más información sobre esta función y los perfiles seudónimos, lea la [Guía de caducidad de datos del perfil seudónimo](../../profile/pseudonymous-profiles.md). |

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
