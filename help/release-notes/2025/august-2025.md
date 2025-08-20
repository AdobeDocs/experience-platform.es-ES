---
title: Notas de la versión de Adobe Experience Platform, agosto de 2025
description: Las notas de la versión de agosto de 2025 de Adobe Experience Platform.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 6672ed3fd4ee4f48952dcf5ffb6561de026fe55b
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 39%

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

**Fecha de lanzamiento: miércoles, 19 de agosto de 2025**


Estas son las nuevas funciones y actualizaciones de las existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [Servicio de catálogo](#catalog-service)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Alertas de capacidad de rendimiento de streaming | Tres nuevas alertas permiten a los usuarios suscribirse y configurar alertas para administrar y supervisar de forma proactiva el rendimiento de la capacidad de rendimiento de flujo continuo. Las nuevas alertas incluyen casos en los que el rendimiento de streaming alcanzó el 80 %, el 90 % o supera los límites de capacidad. Para obtener más información, lea la guía [reglas de alerta de capacidad](../../observability/alerts/rules.md#capacity). |

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Servicio de catálogo {#catalog-service}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Retención de datos para el perfil del cliente en tiempo real | Solo puede **actualizar** el período de retención de datos del perfil del cliente en tiempo real una vez cada 30 días. |

Para obtener más información sobre el servicio de catálogo, lea la [descripción general del servicio de catálogo](../../catalog/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

>[!IMPORTANT]
>
>**Extensión de programación de exportación de conjuntos de datos**
>
>Si su organización tiene flujos de datos de exportación de conjuntos de datos creados antes de noviembre de 2024, estos dejarán de funcionar el **1 de septiembre de 2025**. Si necesita que los flujos de datos sigan exportando datos después del 1 de septiembre de 2025, debe ampliar sus programaciones para cada destino al que esté exportando conjuntos de datos, siguiendo los pasos de [esta guía](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>Se requiere **actualización de lista de permitidos IP para destinos basados en API**
>
>Debido a las actualizaciones en el motor de exportación de destinos de streaming, las organizaciones que usan [listas de permitidos IP](../../destinations/catalog/streaming/ip-address-allow-list.md) para destinos basados en API deben agregar las siguientes direcciones IP a sus listas de permitidos **antes del 15 de septiembre de 2025**:
>
>**Direcciones IP requeridas:**
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
>- [Destinos de exportación de audiencias de streaming](../../destinations/destination-types.md#streaming-destinations) ([Audiencia en tiempo real Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), integraciones basadas en API con [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) y [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinos públicos o privados creados mediante [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Acción necesaria:** Si ha trabajado con Adobe para realizar la lista de permitidos de direcciones IP en destinos de flujo basados en API, debe agregar las direcciones IP anteriores a su lista de permitidos para garantizar flujos de datos ininterrumpidos en sus destinos basados en API.

**Nuevos destinos**

| Destino | Descripción |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) destino | Use el destino [!DNL Acxiom Real ID Audience Connection] para mejorar audiencias con la tecnología [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) y activar audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más. |

**Destinos actualizados**

| Destino | Descripción |
| --- | --- |
| Actualización interna de [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | Desde el martes, 11 de agosto de 2025, puede ver dos tarjetas **[!DNL Microsoft Bing]** una al lado de la otra en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino **[!DNL Microsoft Bing]** existente a **[!UICONTROL (obsoleto) Microsoft Bing]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Microsoft Bing]**. Use la nueva conexión **[!UICONTROL Microsoft Bing]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL (obsoleto) de Microsoft Bing]**, se actualizarán automáticamente, por lo que no es necesario que realice ninguna acción. <br><br>Si está creando flujos de datos a través de la [API del servicio de flujo](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar su [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores:<ul><li>ID de especificación de flujo: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de especificación de conexión: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Después de esta actualización, es posible que experimente una **caída en el número de perfiles activados** en sus flujos de datos a [!DNL Microsoft Bing]. Esta caída se debe a la introducción del **requisito de asignación ECID** para todas las activaciones en esta plataforma de destino. |


**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Funciones mejoradas de búsqueda, filtrado y etiquetado para destinos | Mejore su flujo de trabajo de administración de destinos con capacidades mejoradas de búsqueda, filtrado y etiquetado en las pestañas [Examinar](../../destinations/ui/destinations-workspace.md#browse) y [Cuentas](../../destinations/ui/destinations-workspace.md#accounts). <br>: ahora puede buscar flujos de datos y cuentas específicos por nombre, filtrar por varios criterios, incluida la plataforma de destino, el estado y las fechas, y crear etiquetas personalizadas para organizar sus destinos. La ordenación de columnas también está disponible para campos clave como el último tiempo de ejecución del flujo de datos, lo que facilita la identificación y administración de las conexiones de destino. <br> ![Demostración animada de la búsqueda de un flujo de datos de destino en la ficha Examinar](../../destinations/assets/ui/workspace/search.gif) |

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Esquemas basados en modelos | Simplifique el modelado de datos con esquemas basados en modelos. Ahora puede crear esquemas más fácilmente con ejemplos explicativos y directrices completas. Actualmente, esta función está disponible para los titulares de licencias de Campaign Orchestration y se ampliará a los clientes de Data Distiller en GA, lo que hace que el modelado de datos sea más accesible y eficiente. |

Para obtener más información, lea la [descripción general de XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

El Perfil del cliente en tiempo real proporciona una vista unificada y procesable de cada cliente mediante la consolidación de datos de todos los canales en un único perfil.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Funcionalidad de búsqueda mejorada en la API de entidades | La API de entidades ahora es compatible con lo siguiente: <ul><li>Persona (perfil)</li><li>Eventos de experiencia</li><li>Cuenta</li><li>Oportunidad</li></ul> Esta actualización simplifica el uso de la API y ayuda a garantizar un rendimiento y una fiabilidad óptimos. Si anteriormente ha utilizado búsquedas para otros tipos de entidades, incluidas tablas de unión y tipos de varias entidades personalizados, ahora es una buena oportunidad para revisar el uso de la API y aprovechar la experiencia mejorada. Para obtener más información, lea la [Guía de actualización de la arquitectura de Real-Time CDB B2B edition](../../rtcdp/b2b-architecture-upgrade.md). |

Para obtener más información sobre el perfil del cliente en tiempo real, lea [Descripción general del perfil](../../profile/home.md).

## Zonas protegidas {#sandboxes}

Experience Platform está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Deduplicación de objetos de dependencia en el flujo de trabajo de importación | Ahora, las herramientas de espacio aislado siempre reutilizan los objetos existentes si se detectan objetos con el mismo nombre, para evitar la proliferación de objetos. Este cambio se aplica a los siguientes objetos: <ul><li>Esquema</li><li>Grupo de campo</li><li>Público</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Para obtener más información, lea la [guía de objetos admitidos para las herramientas de zonas protegidas](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Compatibilidad total con la zona protegida para el uso compartido de paquetes entre organizaciones | La herramienta de espacio aislado ahora admite el tipo **Espacio aislado completo** en el uso compartido de paquetes entre organizaciones. Ahora puede compartir paquetes de zona protegida completos y de varios objetos entre organizaciones. Para obtener más información, lea la [guía de objetos admitidos en las herramientas de zonas protegidas](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Estimaciones de audiencia | Las estimaciones de audiencia ahora se generan automáticamente en el Generador de segmentos. Este valor se actualiza siempre que se modifica la audiencia y siempre refleja las reglas de audiencia más recientes. Además, la estimación ahora se mostrará como **rango**, que se basa en el intervalo de confianza de los datos de muestreo. |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Compatibilidad con [!BADGE Beta]{type=Informative} para [!DNL Azure Private Links] en la interfaz de usuario | Ahora puede usar [!DNL Azure Private Links] para un grupo selecto de orígenes en la interfaz de usuario. Utilice esta función para crear un extremo privado al que se pueda conectar el origen. Con los extremos privados, puede configurar conexiones y flujos de datos que omiten la Internet pública, lo que le ofrece una seguridad mejorada y un aislamiento de red para sus datos confidenciales. La compatibilidad con [!DNL Azure Private Links] está disponible para los siguientes orígenes: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> Para obtener más información, lea la guía de [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |
| Autenticación mejorada para [!DNL Azure Blob Storage] | Ahora puede usar la autenticación basada en la entidad de seguridad de servicio para conectar su origen de [!DNL Azure Blob Storage] a Experience Platform. Utilice la autenticación basada en la entidad de seguridad de servicio para mejorar la seguridad, facilitar la rotación de credenciales y un control de acceso más granular para su cuenta. Para obtener más información, lea la [[!DNL Azure Blob Storage] información general](../../sources/connectors/cloud-storage/blob.md). |

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
-->
