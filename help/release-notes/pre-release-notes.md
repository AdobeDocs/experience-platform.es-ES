---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 34%

---

# Notas previas al lanzamiento de Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento está diseñado como **vista previa** de las notas de la versión del mes actual. Los elementos de la versión están sujetos a cambios y se pueden añadir o eliminar en la versión final.

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de lanzamiento: Agosto de 2025**

Estas son las nuevas funciones y actualizaciones de las existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Alertas de capacidad de rendimiento de streaming | Tres nuevas alertas permiten a los usuarios suscribirse y configurar alertas para administrar y supervisar de forma proactiva el rendimiento de la capacidad de rendimiento de flujo continuo. Las nuevas alertas incluyen casos en los que el rendimiento de streaming alcanzó el 80 %, el 90 % o supera los límites de capacidad. Para obtener más información, lea la guía [reglas de alerta de capacidad](../observability/alerts/rules.md#capacity). |

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../observability/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| --- | --- |
| [!DNL Acxiom Real ID Audience] destino | Use el destino [!DNL Acxiom Real ID Audience Connection] para mejorar audiencias con la tecnología [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) y activar audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más. |


**Destinos actualizados**

| Destino | Descripción |
| --- | --- |
| Detalles de caducidad de autenticación para [!DNL LinkedIn] destinos | No vuelva a preocuparse por las credenciales caducadas. La información de caducidad de la cuenta ahora está visible directamente en la interfaz de Experience Platform, por lo que puede ver cuándo caducará la autenticación de [!DNL LinkedIn] y renovarla antes de que cause interrupciones en los flujos de datos. |
| Compatibilidad con cifrado para [!DNL Data Landing Zone] destinos | Proteja los datos exportados con cifrado. Ahora puede adjuntar claves públicas con formato RSA para cifrar los archivos exportados, lo que le proporciona el mismo nivel de seguridad que otros destinos de almacenamiento en la nube para la información confidencial. |
| Actualización interna de [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) | Desde el martes, 11 de agosto de 2025, puede ver dos tarjetas **[!DNL Microsoft Bing]** una al lado de la otra en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino **[!DNL Microsoft Bing]** existente a **[!UICONTROL (obsoleto) Microsoft Bing]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Microsoft Bing]**. Use la nueva conexión **[!UICONTROL Microsoft Bing]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL (obsoleto) de Microsoft Bing]**, se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br><br>Si está creando flujos de datos a través de la [API del servicio de flujo](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar su [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores:<ul><li>ID de especificación de flujo: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de especificación de conexión: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Después de esta actualización, es posible que experimente una **caída en el número de perfiles activados** en sus flujos de datos a [!DNL Microsoft Bing]. Esta caída se debe a la introducción del **requisito de asignación ECID** para todas las activaciones en esta plataforma de destino. |
| Identificadores adicionales para [!DNL Amazon Ads] destinos | El destino de Amazon Ads ahora admite nuevas identidades (`firstName`, `lastName`, `street`, `city`, `state`, `zip`, `country`). Estos campos están pensados para mejorar las tasas de coincidencia de audiencia y se pasan en texto sin formato, con hashing SHA256 opcional. |
| [!DNL Marketo] consolidación de tarjetas de destino | Simplifique la configuración de destino de [!DNL Marketo] con nuestra tarjeta de destino unificada. Hemos consolidado [!DNL Marketo] tarjetas V2 y V3 en una opción optimizada, lo que facilita la elección del destino correcto y la introducción rápida. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Ampliar las programaciones de exportación de conjuntos de datos para flujos de datos creados antes de noviembre de 2024 | Si su organización tiene flujos de datos de exportación de conjuntos de datos creados antes de noviembre de 2024, estos dejarán de funcionar el 1 de septiembre de 2025. Si necesita que los flujos de datos sigan exportando datos después del 1 de septiembre de 2025, debe ampliar sus programaciones para cada destino al que esté exportando conjuntos de datos, siguiendo los pasos de [esta guía](../destinations/ui/dataset-expiration-update.md). |
| Funciones mejoradas de búsqueda, filtrado y etiquetado para destinos | Mejore su flujo de trabajo de administración de destinos con funciones mejoradas de búsqueda, filtrado y etiquetado en las pestañas Examinar y Cuentas. Ahora puede buscar flujos de datos y cuentas específicos por nombre, filtrar por varios criterios, incluida la plataforma de destino, el estado y las fechas, y crear etiquetas personalizadas para organizar los destinos. La ordenación de columnas también está disponible para campos clave como el último tiempo de ejecución del flujo de datos, lo que facilita la identificación y administración de las conexiones de destino. |

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Esquemas basados en modelos | Simplifique el modelado de datos con esquemas basados en modelos. Ahora puede crear esquemas más fácilmente con ejemplos explicativos y directrices completas. Actualmente, esta función está disponible para los titulares de licencias de Campaign Orchestration y se ampliará a los clientes de Data Distiller en GA, lo que hace que el modelado de datos sea más accesible y eficiente. |

Para obtener más información, lea la [descripción general de XDM](../xdm/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Estimaciones de audiencia | Las estimaciones de audiencia ahora se generan automáticamente en el Generador de segmentos. Este valor se actualiza siempre que se modifica la audiencia y siempre refleja las reglas de audiencia más recientes. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| [!BADGE Compatibilidad con vínculos privados de Beta]{type=Informative} en la interfaz de usuario de Azure | Mantenga sus datos seguros con conexiones de red privada. Ahora puede crear puntos de conexión privados y configurar flujos de datos que omitan la Internet pública, lo que le ofrece una seguridad mejorada y un aislamiento de red para sus datos confidenciales. |
| [!DNL Marketo] actualizaciones de la documentación de origen | Obtenga una visibilidad completa de cómo se transforman los datos de [!DNL Marketo] al entrar en Experience Platform. Todas las asignaciones de campos ahora incluyen explicaciones detalladas de las transformaciones de datos, para que pueda comprender exactamente cómo `PersonID` se convierte en `leadID` y `eventType` se convierte en `activityType`. |
| Compatibilidad con la autenticación principal de servicio para [!DNL Azure Blob Storage] | Ahora puede conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform con la autenticación de entidad de seguridad de servicio. |

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
