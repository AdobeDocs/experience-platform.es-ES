---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 37d073266bf9293ad3a9e85c193acd1e2e47fa2a
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 25 de mayo de 2022**

<!-- New features in Adobe Experience Platform: -->

<!-- - [Attribute-based access control](#abac) -->
<!-- - [Data hygiene](#hygiene) -->

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Registros de auditoría](#audit-logs)
- [Tableros](#dashbaords)
- [Recopilación de datos](#data-collection)

<!-- - [Data Governance](#data-governance) -->
- [Preparación de datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Fuentes](#sources)

<!-- ## Attribute-based access control {#abac}

>[!IMPORTANT]
>
>Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.

Attribute-based access control is a capability of Adobe Experience Platform that enables administrators to control access to specific objects and/or capabilities based on attributes. Attributes can be metadata added to an object, such as a label added to a schema field or segment. An administrator defines access policies that include attributes to manage user access permissions.

Through attribute-based access control, administrators of your organization can control users’ access to both sensitive personal data (SPD) and personally identifiable information (PII) across all Platform workflows and resources. Administrators can define user roles that have access only to specific fields and data that correspond to those fields.

| Feature | Description |
| --- | --- |
| Attribute-based access control | Attribute-based access control allows you to label Experience Data Model (XDM) schema fields with labels that define organizational or data usage scopes. In parallel, administrators can use the user and role administration interface to define access policies covering XDM schema fields and better manage the access given to users or groups of users (internal, external, or third-party users). Additionally, attribute-based access control allows administrators to manage access to specific segments. |
| Permissions | Permissions is the area of Experience Cloud where administrators can define user roles and access policies to manage access permissions for features and objects within a product application. Through Permissions, you can create and manage roles, as well as assign the desired resource permissions for these roles. Permissions also allow you to manage the labels, sandboxes, and users associated with a specific role. For more information, see the [Permissions UI guide](../../access-control/abac/ui/browse.md). |

For more information on attribute-based access control, see the [attribute-based access control overview](../../access-control/abac/overview.md). -->

<!-- ## Data hygiene {#hygiene}

Experience Platform provides a suite of data hygiene capabilities that allow you manage your stored data through programmatic deletions of consumer records and datasets. Using either the [!UICONTROL Data Hygiene] workspace in the UI or through calls to the Data Hygiene API, you can manage your data stores to ensure that information is used as expected, is updated when incorrect data needs fixing, and is deleted when organizational policies deem it necessary.

>[!IMPORTANT]
>
>Data hygiene capabilities are currently only available for organizations that have purchased the Adobe Shield for Healthcare add-on offering.

**New features**

| Feature | Description |
| --- | --- |
| Consumer deletion | [Delete consumer records](../../hygiene/ui/delete-consumer.md) from the data lake and Profile store based on primary identity data. |
| Time to live (TTL) for datasets | [Schedule TTLs](../../hygiene/ui/ttl.md) for Platform datasets.  |

For more information on audit logs in Platform, refer to the [data hygiene overview](../../hygiene/home.md). -->

## Registros de auditoría {#audit-logs}

Experience Platform le permite auditar la actividad de los usuarios en relación con diversos servicios y funcionalidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Funciones actualizadas**

| Función | Nombre | Descripción | | — | — | — | | Recursos añadidos | <ul><li> Política de control de acceso </li><li> Función </li><li> Registros de auditoría </li><li> Orden de trabajo </li><li> Área de nombres de identidad </li><li> Gráfico de identidad </li><li> Consulta </li><li> Conjunto de datos </li><li> Flujo de datos de origen </li></ul> | Los recursos del registro de auditoría se registran automáticamente a medida que se produce la actividad. Si la función está habilitada, no es necesario habilitar manualmente la recopilación de registros. |



Para obtener más información sobre los registros de auditoría en Platform, consulte la [información general sobre registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver información importante sobre los datos de su organización, tal como se captura durante las instantáneas diarias.

### Tableros de perfiles

El panel de perfiles muestra una instantánea de los datos de atributo (registro) que su organización tiene en el Almacenamiento de perfiles en el Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Superposición de audiencias por el widget de directiva de combinación | Esta utilidad muestra la transición visual de las definiciones de segmentos y le permite optimizar la estrategia de segmentación mediante el estudio de las similitudes entre las definiciones de segmentos. |
| El recuento de perfiles cambia la tendencia por el widget de identidad | Esta utilidad le ayuda a administrar sus necesidades de activación de destino demostrando el patrón de crecimiento de perfiles filtrados por la identidad requerida. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los perfiles, consulte la [documentación del panel de perfiles](../../dashboards/guides/profiles.md).

### Tableros de destinos

El panel de destinos muestra una instantánea de los destinos que su organización ha habilitado en Experience Platform.

| Función | Descripción |
| --- | --- |
| Audiencias activadas por widget de destino | Esta utilidad le ayuda a comprender de un vistazo el valor de sus destinos en función del número de audiencias activadas. También proporciona acceso fácil a información más detallada sobre los segmentos que se han asignado al destino. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los destinos, consulte la [documentación del panel de destinos](../../dashboards/guides/destinations.md).

### Tableros de segmentos

El tablero de segmentos proporciona una interfaz de usuario a través de la cual puede ver información importante sobre sus segmentos, tal como se captura durante una instantánea diaria.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de superposición de audiencia | Esta utilidad le permite optimizar su estrategia de segmentación mediante la visualización de las similitudes en los resultados de sus definiciones de segmento. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los segmentos, consulte la [documentación del tablero de segmentos](../../dashboards/guides/segments.md).

## Recopilación de datos {#data-collection}

Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Copiar conjuntos de datos | [Crear una copia de un conjunto de datos existente](../../edge/datastreams/overview.md#copy) y ajuste su configuración según sea necesario, evitando la necesidad de comenzar desde cero. |
| Importar reglas de asignación de conjuntos de datos | Al configurar la preparación de datos para la recopilación de datos, puede [importar las reglas de asignación de un conjunto de datos existente](../../edge/datastreams/data-prep.md#import-mapping) en lugar de configurar cada asignación de campo manualmente. |
| Compatibilidad con la asignación de conjuntos de datos para SDK móvil | Ahora puede configurar la preparación de datos para la recopilación de datos en conjuntos de datos que se van a usar con el SDK móvil de Experience Platform. |
| Compatibilidad con la asignación de conjuntos de datos para objetos XDM | Asignar objetos XDM además de objetos de capa de datos al [configuración de la preparación de datos para la recopilación de datos](../../edge/datastreams/data-prep.md#select-data). |

Para obtener más información sobre la recopilación de datos en Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

<!-- ## Data Governance {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature | Description | 
| ------- | ----------- |
| Consent policy enforcement (limited availability) | If your organization has purchased the Adobe Shield for Healthcare add-on offering, you can now [create consent policies](../../data-governance/policies/user-guide.md#consent-policy) to automatically [enforce customer consents and preferences in segment participation](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style="table-layout:auto"}

See the [Data Governance overview](../../data-governance/home.md) for more information on the service. -->

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Errores de datos localizados | [!DNL Data Prep] ahora localiza todos los errores de transformación al nivel de atributo (anteriormente al nivel de fila). Los flujos de datos ahora incorporarán filas parciales rellenas de columnas que no tengan errores de transformación, en lugar de ignorar las filas completas. |
| Transmitir de subida a [!DNL Profile Service] | Transfiera las fuentes con [!DNL Data Prep] para enviar actualizaciones de fila parciales al servicio de perfil mediante la función [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)o [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) fuente. Consulte la guía de [streaming upserts](../../data-prep/upserts.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in [!DNL Data Prep] | You will now only be able to map attributes that you have access to. Attributes that you do not have access to can not be used in pass-through mappings and calculated fields. For more information, see [attribute-based access control in [!DNL Data Prep]](../../data-prep/home.md). **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released. | -->

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Exportar las últimas cualificaciones de perfil [después de la evaluación diaria de segmentos](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Ahora puede programar una exportación completa de archivos, una vez o a diario, con las últimas cualificaciones de perfil, una vez completada la evaluación diaria de segmentos. |
| ID de almacén de datos opcional para [Destinos de Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Para habilitar la personalización de Adobe Target para los usuarios que no puedan implementar el SDK web del Experience Platform, la selección del ID del conjunto de datos es ahora opcional al configurar destinos de Adobe Target. Cuando no utilice un conjunto de datos, los segmentos exportados de Experience Platform a Target solo admitirán la personalización de la siguiente sesión, mientras que la segmentación perimetral estará deshabilitada, junto con todas las [casos de uso](../../destinations/ui/configure-personalization-destinations.md) que dependen de la segmentación de Edge. |

{style=&quot;table-layout:auto&quot;}

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Conjunto de cambios]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | Captura los cambios en el nivel de fila de los conjuntos de datos. Este grupo de campos se puede utilizar en cualquier clase. |
| Grupo de campos | [[!UICONTROL Claves de referencia]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | Captura claves de referencia para esquemas de ExperienceEvent, lo que permite crear relaciones con esquemas basados en otras clases. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Comportamiento | [[!UICONTROL Esquema de series temporales]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | Actualizado `eventType` para incluir varios tipos de eventos nuevos relacionados con los medios y un caso de uso entrante de canal web para Adobe Journey Optimizer. |
| Esquema global | [[!UICONTROL Destino]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | Se han eliminado los valores de enumeración de `xdm:destinationCategory`. |
| Grupo de campos | [[!UICONTROL Estado de registro]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | Se ha actualizado el estado del grupo de campos de `experimental` a `stable`. |
| Grupo de campos | (Varios) | Se han actualizado varios grupos de campos B2B para que ciertos campos de ID queden obsoletos en favor de los campos de tipo clave que utilizan la variable [[!UICONTROL Fuente B2B]](../../xdm/data-types/b2b-source.md) tipo de datos. Los campos de ID anteriores quedarán obsoletos en una actualización futura. Consulte lo siguiente [solicitud de extracción](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1) para obtener una lista completa de los cambios realizados en los grupos de campos afectados. |
| Tipo de datos | [[!UICONTROL Detalles del explorador]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | Se ha añadido un nuevo campo `xdm:userAgentClientHints` que captura información contextual sobre el agente de usuario que interactúa con el explorador. |
| Tipo de datos | [[!UICONTROL Información multimedia]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | Se ha añadido un `xdm:playhead` para capturar el tiempo del cabezal de reproducción de un fragmento de contenido multimedia. Se ha corregido la validación de patrones para `xdm:videoSegment`. |
| Tipo de datos | [[!UICONTROL Clasificación]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` ya no es un campo obligatorio. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL data lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL data lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Integración del registro de auditoría del servicio de consultas | La integración del registro de auditoría del servicio de consulta proporciona registros de las acciones de usuario relacionadas con la consulta con el fin de solucionar problemas o cumplir con las políticas y los requisitos regulatorios de administración de datos corporativos. Consulte la [documentación de integración del registro de auditoría](../../query-service/data-governance/audit-log-guide.md) para información completa |
| CONSTRUCCIÓN SQL ALTER TABLE | Utilice SQL para establecer identidades principales en un conjunto de datos ad hoc. El servicio de consulta le permite marcar las columnas del conjunto de datos como identidades principales o secundarias directamente a través de SQL mediante el uso de `ALTER TABLE` comando. |

{style=&quot;table-layout:auto&quot;}

<!-- For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md). -->

Para obtener más información sobre las capacidades del servicio de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Lanzamiento beta de [!DNL Zendesk] source | Utilice la variable [!DNL Zendesk] fuente para introducir datos de usuario, agente y organización de su [!DNL Zendesk] instancia para [!DNL Profile] enriquecimiento. Consulte la [[!DNL Zendesk] información general de la fuente](../../sources/connectors/customer-success/zendesk.md) para obtener más información. |
| Compatibilidad con la recopilación de datos de Adobe | Utilice el catálogo de fuentes para acceder a los datos de la recopilación de datos de Experience Edge, incluida la preparación de datos para la recopilación de datos y la compatibilidad mejorada con las advertencias de datos de la preparación de datos. Consulte la [Resumen de la fuente de recopilación de datos de Adobe](../../sources/connectors/adobe-applications/data-collection.md) para obtener más información. |
| Compatibilidad con la ingesta de archivos con `ISO-8859-1` encoding | Utilice la variable `encoding` parámetro a ingesta `ISO-8859-1` archivos codificados con una fuente de almacenamiento en la nube para Platform con el [!DNL Flow Service] API. Consulte la guía de [creación de una conexión de origen de almacenamiento en la nube](../../sources/tutorials/api/collect/cloud-storage.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in sources | You can now manage and control access to individual source fields and attributes during ingestion. **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.  | -->

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
