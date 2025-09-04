---
title: Notas de la versión de Adobe Experience Platform, agosto de 2025
description: Las notas de la versión de agosto de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 76acf488ad06ec7b3fe818cf34c86ea76dc614f4
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 97%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de lanzamiento: 19 de agosto de 2025**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Alertas](#alerts)
- [Servicio de catálogo](#catalog-service)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Alertas de capacidad de rendimiento de streaming | Tres nuevas alertas permiten a los usuarios suscribirse y configurar alertas para administrar y monitorizar de forma proactiva el desempeño de la capacidad de rendimiento de streaming. Las nuevas alertas incluyen casos en los que el rendimiento de streaming alcanzó el 80 %, el 90 % o supera los límites de capacidad. Para obtener más información, lea la guía de [reglas de alerta de capacidad](../../observability/alerts/rules.md#capacity). |

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Retención de datos para el perfil del cliente en tiempo real | **Solo** puede actualizar el período de retención de datos del perfil del cliente en tiempo real una vez cada 30 días. |

Para obtener más información sobre el Servicio de catálogo, lea la [información general sobre el Servicio de catálogo](../../catalog/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

>[!IMPORTANT]
>
>**Extensión de programación de exportación de conjuntos de datos**
>
>Si su organización tiene flujos de datos de exportación de conjuntos de datos creados antes de noviembre de 2024, estos dejarán de funcionar el **1 de septiembre de 2025**. Si necesita que los flujos de datos sigan exportando datos después del 1 de septiembre de 2025, debe ampliar sus programaciones para cada destino al que exporte conjuntos de datos, siguiendo los pasos de [esta guía](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Se requiere la actualización de la lista de IP permitidas para destinos basados en API**
>
>Debido a las actualizaciones en el motor de exportación de destinos de streaming, las organizaciones que usan [listas de IP permitidas](../../destinations/catalog/streaming/ip-address-allow-list.md) para destinos basados en API deben añadir las siguientes direcciones IP a sus listas **antes del 15 de septiembre de 2025**:
>
>**Direcciones IP obligatorias:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Este cambio se aplica a los siguientes tipos de destino:**
>
>- [Destinos de exportación de audiencias de streaming](../../destinations/destination-types.md#streaming-destinations) ([Audiencia en tiempo real de Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), integraciones basadas en API con [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) y [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinos públicos o privados creados mediante [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Acción necesaria:** si ha trabajado con Adobe para incluir en la lista de permitidos alguna dirección IP en destinos de streaming basados en API, debe añadir las direcciones IP anteriores a la lista para garantizar flujos de datos ininterrumpidos en sus destinos basados en API.

**Nuevos destinos**

| Destino | Descripción |
| --- | --- |
| Destino [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Use el destino [!DNL Acxiom Real ID Audience Connection] para mejorar las audiencias con la tecnología [Real ID](https://www.acxiom.com/real-id/real-id/) de [!DNL Acxiom's] y activar audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más. |

**Destinos actualizados**

| Destino | Descripción |
| --- | --- |
| Actualización interna de [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | A partir del 11 de agosto de 2025, es posible que haya visto dos tarjetas de **[!DNL Microsoft Bing]** en paralelo en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino **[!DNL Microsoft Bing]** existente a **[!UICONTROL Microsoft Bing (obsoleto)]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Microsoft Bing]**. <br>La actualización se completó y la tarjeta obsoleta se eliminó del catálogo de destino. Use la nueva conexión **[!UICONTROL Microsoft Bing]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL Microsoft Bing (obsoleto)]**, se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br><br>Si está creando flujos de datos a través de la [API del servicio de flujo](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar su [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores:<ul><li>ID de especificación de flujo: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de especificación de conexión: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Después de esta actualización, es posible que experimente una **caída en el número de perfiles activados** en sus flujos de datos a [!DNL Microsoft Bing]. Esta caída se debe a la introducción del **requisito de asignación ECID** para todas las activaciones en esta plataforma de destino. |
| Detalles de caducidad de autenticación de [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) y destinos de [audiencias coincidentes de LinkedIn](../../destinations/catalog/social/linkedin-b2b.md) | La información de caducidad de autenticación de los destinos de [!DNL LinkedIn] ahora es visible directamente en la interfaz de Experience Platform, por lo que puede ver cuándo caducará la autenticación y renovarla antes de que cause interrupciones en los flujos de datos. Puede monitorizar las fechas de caducidad de los tókenes desde la columna **[!UICONTROL Fecha de caducidad de la cuenta]** en las pestañas **[[!UICONTROL Cuentas]](../../destinations/ui/destinations-workspace.md#accounts)** o **[[!UICONTROL Examinar]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Funciones mejoradas de búsqueda, filtrado y etiquetado para destinos | Mejore su flujo de trabajo de administración de destinos con capacidades mejoradas de búsqueda, filtrado y etiquetado en las pestañas [Examinar](../../destinations/ui/destinations-workspace.md#browse) y [Cuentas](../../destinations/ui/destinations-workspace.md#accounts). <br>Ahora puede buscar flujos de datos y cuentas específicos por nombre, filtrar por varios criterios (incluidos la plataforma de destino, el estado y las fechas) y crear etiquetas personalizadas para organizar los destinos. La ordenación de columnas también está disponible para campos clave como el último tiempo de ejecución del flujo de datos, lo que facilita la identificación y administración de las conexiones de destino. <br> ![Demostración animada de la búsqueda de un flujo de datos de destino en la pestaña Examinar](../../destinations/assets/ui/workspace/search.gif) |


## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Esquemas basados en modelos | Simplifique el modelado de datos con esquemas basados en modelos. Ahora puede crear esquemas más fácilmente con ejemplos explicativos y directrices completos. En la actualidad, esta función está disponible para los titulares de licencias de Orquestación de campañas y se ampliará a los clientes de Data Distiller en GA, lo que hace que el modelado de datos sea más accesible y eficiente. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

<!--

## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Zonas protegidas {#sandboxes}

Experience Platform está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Deduplicación de objetos de dependencia en el flujo de trabajo de importación | Ahora, las herramientas de zona protegida siempre reutilizarán los objetos existentes si se detectan objetos con el mismo nombre para evitar la proliferación de objetos. Este cambio se aplica a los siguientes objetos: <ul><li>Esquema</li><li>Grupo de campo</li><li>Público</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Para obtener más información, lea la [guía de objetos admitidos para las herramientas de zonas protegidas](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Compatibilidad total con la zona protegida para el uso compartido de paquetes entre organizaciones | La herramienta de zona protegida ahora admite el tipo **Zona protegida completa** en el uso compartido de paquetes entre organizaciones. Ahora puede compartir paquetes de zona protegida completa y de varios objetos entre organizaciones. Para obtener más información, lea la [guía de objetos admitidos en las herramientas de zonas protegidas](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Estimaciones de audiencia | Las estimaciones de audiencia ahora se muestran como **rango**, que se basa en el intervalo de confianza de los datos de muestreo. Para obtener más información acerca de las estimaciones, lea la [guía del Generador de segmentos](/help/segmentation/ui/segment-builder.md#audience-properties). |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Autenticación mejorada para [!DNL Azure Blob Storage] | Ahora puede usar la autenticación basada en principal de servicio para conectar su fuente de [!DNL Azure Blob Storage] a Experience Platform. Utilice la autenticación basada en principal de servicio para mejorar la seguridad, facilitar la rotación de credenciales y conseguir un control de acceso más granular para su cuenta. Para obtener más información, lea la [[!DNL Azure Blob Storage] información general](../../sources/connectors/cloud-storage/blob.md). |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

<!---

| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|

-->

