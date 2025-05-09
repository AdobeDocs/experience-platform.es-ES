---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2022'
description: Las notas de la versión de marzo de 2022 de Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 20%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 30 de marzo de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Registros de auditoría](#audit-logs)
- [Cuentas relacionadas en Real-Time CDP B2B edition](#related-accounts)

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Recopilación de datos](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Fuentes](#sources)

## Registros de auditoría {#audit-logs}

Experience Platform le permite auditar la actividad del usuario para varios servicios y funcionalidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Registros de auditoría para conjunto de datos, esquema, clase, grupo de campos, tipo de datos, zona protegida, destino, segmento, política de combinación, atributo calculado, perfil de producto y cuenta (Adobe) | Estos son los recursos que se registran en los registros de auditoría. Si la función está habilitada, los registros de auditoría se recopilarán automáticamente a medida que se produzca la actividad. No es necesario habilitar manualmente la recopilación de registros. |
| Exportar registros de auditoría | Los registros de auditoría se pueden descargar como un archivo de `CSV` o `JSON`. Los archivos generados se guardan directamente en el equipo. |

{style="table-layout:auto"}

Para obtener más información sobre los registros de auditoría en Experience Platform, consulte la [descripción general de los registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Cuentas relacionadas en Real-Time CDP B2B edition {#related-accounts}

>[!NOTE]
>
>La función Cuentas relacionadas solo está disponible para clientes de B2B edition de Real-Time CDP.

Las empresas B2B a menudo almacenan la información de sus clientes en varios sistemas, cada uno de los cuales incluye solo datos parciales o incluso en conflicto para la misma entidad comercial del mundo real. Esto crea un desafío masivo de llegar a una vista precisa de sus clientes, reduciendo así la eficiencia y eficacia de sus esfuerzos de marketing y ventas B2B. Con el lanzamiento de las cuentas relacionadas, [!DNL Real-Time CDP B2B] ahora muestra una lista de cuentas similares a la cuenta que está explorando. Puede incluir las cuentas relacionadas en sus definiciones de segmentos para ampliar su alcance o aplicar criterios más amplios en sus segmentos.

Obtenga más información sobre la función en las siguientes páginas de documentación:

- [Información general sobre cuentas relacionadas en Real-Time CDP B2B edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Pestaña Cuentas relacionadas en la guía de la IU del perfil de cuenta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Uso de cuentas relacionadas en definiciones de segmentos](../../rtcdp/segmentation/b2b.md#related-accounts)

Para obtener más información acerca de Real-Time CDP B2B edition, consulte la [descripción general](../../rtcdp/overview.md).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a diferentes reglas de alertas a través de la pestaña [!UICONTROL Alertas] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o a través de notificaciones por correo electrónico.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas reglas de alerta | Ahora hay dos nuevas reglas de alerta disponibles para las fuentes relacionadas con la ingesta de datos. Consulte la descripción general de [reglas de alerta](../../observability/alerts/rules.md) para ver la lista actualizada de tipos de alerta. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas en Experience Platform, consulte la [descripción general de las alertas](../../observability/alerts/overview.md).

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios(as) [!DNL dashboards] a través de los cuales puede ver información importante acerca de los datos de su organización, según se capturan durante las instantáneas diarias.

### Paneles de perfil

El panel Perfiles muestra una instantánea de los datos de atributo (registro) que su organización tiene en el almacén de perfiles en Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de perfiles no segmentados | El widget proporciona el número total de todos los perfiles no adjuntos a ningún segmento. El número generado es preciso desde la última instantánea y representa la oportunidad de activación de perfiles en toda la organización. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| Widget de tendencias de perfiles no segmentados | Este widget proporciona una ilustración gráfica de líneas del número de perfiles que no están adjuntos a ningún segmento durante un período de tiempo determinado. La tendencia se puede visualizar en períodos de 30 días, 90 días y 12 meses. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| Perfiles no segmentados por widget de identidad | Este widget categoriza el número total de perfiles no segmentados por su identificador único. Los datos se visualizan en un gráfico de barras. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| Widget de perfiles de identidad única | Este widget proporciona un recuento de los perfiles de su organización que solo tienen un tipo de ID que crea su identidad, ya sea un correo electrónico o un ECID. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre paneles de perfiles, consulte la [Información general sobre paneles de perfiles](../../dashboards/guides/profiles.md).

### Paneles de destinos

El panel Destinos muestra una instantánea de los destinos que su organización ha activado en Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de recuento de destinos | El widget proporciona el número total de puntos de conexión disponibles en los que se puede activar y enviar una audiencia dentro del sistema. Este número incluye destinos activos e inactivos. Consulte la [documentación del widget estándar de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre paneles de destinos en Experience Platform, consulte la [descripción general de paneles de destinos](../../dashboards/guides/destinations.md).

## Recopilación de datos {#data-collection}

Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Configuración global de flujo de datos | Ahora puede configurar varias opciones globales nuevas al configurar un conjunto de datos: ubicación geográfica, cookie de ID de origen y sincronización de ID de terceros. Consulte la sección sobre [configuración de una secuencia de datos](../../datastreams/overview.md#create) en la guía de IU de secuencias de datos para obtener más información. |
| [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/getting-started/) | La API de Edge Network permite que los clientes interactúen con el Edge Network de Experience Platform mediante un extremo nuevo y autenticado, para impulsar una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing. |

Para obtener más información sobre la recopilación de datos en Experience Platform, consulte [descripción general de la recopilación de datos](../../collection/home.md).

## Servicio de consultas {#query-service}

[!DNL Query Service] le permite usar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| `table_exists` | El comando de la nueva función se utiliza para confirmar si existe o no una tabla en el sistema. El comando devuelve un valor booleano: `true` si la tabla **existe**, y `false` si la tabla existe **no**. Consulte la [documentación de sintaxis SQL](../../query-service/sql/syntax.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las características disponibles, consulte [Introducción al servicio de consultas](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar la ingesta de datos en todo.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Hay nuevas fuentes disponibles para el uso B2B | Ahora puede utilizar todas las fuentes disponibles en Experience Platform para casos de uso B2B. Consulte el [catálogo de fuentes](../../sources/home.md) para obtener una lista completa de las fuentes disponibles. |
| Disponibilidad general del nuevo origen [!DNL Oracle Eloqua] | Ahora puede usar el origen [!DNL Oracle Eloqua] para ingerir sin problemas datos de su instancia [!DNL Oracle Eloqua] (cuenta, campaña, contactos) en Experience Platform. Consulte la documentación sobre [creación de una [!DNL Oracle Eloqua] conexión de origen](../../sources/connectors/marketing-automation/oracle-eloqua.md) para obtener más información. |
| Mejoras de API para [!DNL Data Landing Zone] | El origen [!DNL Data Landing Zone] ahora admite la detección automática de propiedades de archivo al usar la API [!DNL Flow Service]. Consulte la documentación sobre [creación de una [!DNL Data Landing Zone] conexión de origen](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
