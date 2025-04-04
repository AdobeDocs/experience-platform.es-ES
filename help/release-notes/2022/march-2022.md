---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2022'
description: Las notas de la versión de marzo de 2022 de Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 16%

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

Experience Platform le permite auditar usuario actividad para distintos servicios y capacidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Registros de auditoría para conjunto de datos, esquema, clase, grupo de campo, tipo de datos, zona de pruebas, destino, segmento, directiva de combinación, atributo calculado, perfil de producto y cuenta (Adobe Systems) | Estos son los recursos registrados por los registros de auditoría. Si la característica está habilitada, los registros de auditoría se recopilarán automáticamente a medida actividad ocurra. No es necesario habilitar manualmente el colección de registro. |
| Exportar registros de auditoría | Los registros de auditoría se pueden descargar como un `CSV` archivo O `JSON` . Los archivos generados se guardan directamente en el equipo. |

{style="table-layout:auto"}

Para obtener más información sobre los registros de auditoría en Experience Platform, consulte la [descripción general de los registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Cuentas relacionadas en Real-Time CDP B2B edition {#related-accounts}

>[!NOTE]
>
>La función Cuentas relacionadas solo está disponible para los clientes de Real-Time CDP B2B Edition.

B2B empresas a menudo tienen la información de sus clientes almacenada en múltiples sistemas, cada uno de los cuales incluye solo datos parciales o igualado conflictivos para la misma entidad comercial del mundo real. Esto crea un desafío masivo de llegar a una vista precisa de sus clientes, lo que reduce la eficiencia y efectividad de sus B2B marketing y esfuerzos de ventas. Con el lanzamiento de cuentas relacionadas, [!DNL Real-Time CDP B2B] ahora le muestra un lista de cuentas que son similares a la cuenta está explorando. Puede incluir las cuentas relacionadas en sus definiciones de segmentos para ampliar su alcance o aplicar criterios más amplios en sus segmentos.

Obtenga más información sobre la función en las siguientes páginas de documentación:

- [Información general sobre cuentas relacionadas en Real-Time CDP B2B edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Pestaña Cuentas relacionadas en la guía de la IU del perfil de cuenta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Uso de cuentas relacionadas en definiciones de segmentos](../../rtcdp/segmentation/b2b.md#related-accounts)

Para obtener más información acerca de Real-Time CDP B2B edition, consulte la [descripción general](../../rtcdp/overview.md).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en evento para varias actividades Experience Platform. Puede suscribirse a diferentes reglas de alerta a través del [!UICONTROL pestaña de] alertas de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia IU o mediante notificaciones correo electrónico.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo reglas alerta | Ahora hay dos nuevas reglas de alerta disponibles para las fuentes relacionadas con la ingesta de datos. Consulte la información general sobre [alerta reglas](../../observability/alerts/rules.md) para conocer las lista actualizadas de alerta tipos. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas en Experience Platform, consulte la [información general](../../observability/alerts/overview.md) de alertas.

## Paneles {#dashboards}

Adobe Experience Platform proporciona múltiples [!DNL dashboards] a través de los cuales puede vista información importante sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

### Paneles de perfil

El panel Perfiles muestra una instantánea de los datos de atributo (registro) que su organización tiene dentro del tienda de perfiles de Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de perfiles no segmentados | La utilidad proporciona el número total de todos los perfiles no asociados a ninguna segmento. El número generado es exacto a partir de la última instantánea y representa el oportunidad de perfil activación en su organización. Consulte la documentación](../../dashboards/guides/profiles.md#standard-widgets) de las [utilidades estándar de perfiles para obtener más información. |
| Widget de tendencias de perfiles no segmentados | Este widget proporciona una ilustración gráfica de líneas del número de perfiles que no están adjuntos a ningún segmento durante un período de tiempo determinado. La tendencia se puede visualizar en períodos de 30 días, 90 días y 12 meses. Consulte la documentación](../../dashboards/guides/profiles.md#standard-widgets) de las [utilidades estándar de perfiles para obtener más información. |
| Widget Perfiles no segmentados por identidad | Esta utilidad categoriza el número total de perfiles no segmentados por su identificador único. Los datos se visualizan en un gráfico de barras. Consulte la documentación](../../dashboards/guides/profiles.md#standard-widgets) de las [utilidades estándar de perfiles para obtener más información. |
| Widget de perfiles de identidad única | Este widget proporciona un recuento de los perfiles de su organización que solo tienen un tipo de tipo de ID que crea su identidad, ya sea un correo electrónico o ECID. Consulte la documentación](../../dashboards/guides/profiles.md#standard-widgets) de las [utilidades estándar de perfiles para obtener más información. |

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

Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos lado del cliente experiencia del cliente y enviarlos a la red de Adobe Experience Platform Edge, donde se pueden enriquecer, transformar y distribuir a destinos Adobe Systems o no Adobe Systems.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Configuración global del flujo de datos | Ahora puede configurar varios ajustes globales nuevos al configurar un flujo de datos: ubicación geográfica, cookie de ID de origen y sincronizar de ID de terceros. Consulte la sección sobre [configuración de un flujo](../../datastreams/overview.md#create) de datos en la guía de IU flujos de datos para obtener más información. |
| [API del servidor de red perimetral](../../server-api/overview.md) | La API del servidor permite a los clientes interactuar con la red perimetral de Experience Platform mediante un nuevo punto final autenticado, para impulsar una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing. |

Para obtener más información sobre recopilación de datos en Experience Platform, consulte la descripción general](../../collection/home.md) recopilación de datos[.

## Servicio de consultas {#query-service}

[!DNL Query Service] le permite usar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unir cualquier conjunto de datos del [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su ingesta en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| `table_exists` | El comando nueva función se utiliza para confirmar si existe o no una tabla en el sistema. El comando devuelve un valor booleano: `true` si la tabla **existe** y `false` si la tabla **no** existe. Consulte la [documentación de sintaxis SQL](../../query-service/sql/syntax.md) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las características disponibles, consulte [Introducción al servicio de consultas](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar la ingesta de datos en todo.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo fuentes ahora disponibles para uso B2B | Ahora puede utilizar todas las fuentes disponibles en Experience Platform para casos de uso B2B. Consulte el [catálogo](../../sources/home.md) de fuentes para obtener una lista completa de las fuentes disponibles. |
| Disponibilidad general de la nueva [!DNL Oracle Eloqua] fuente | Ahora puede usar el origen [!DNL Oracle Eloqua] para ingerir sin problemas datos de su instancia [!DNL Oracle Eloqua] (cuenta, campaña, contactos) en Experience Platform. Consulte la documentación sobre [la creación de una [!DNL Oracle Eloqua] conexión](../../sources/connectors/marketing-automation/oracle-eloqua.md) de origen para obtener más información. |
| Mejoras de API para [!DNL Data Landing Zone] | El [!DNL Data Landing Zone] origen ahora admite la detección automática de propiedades de archivo cuando se utiliza la [!DNL Flow Service] API. Consulte la documentación sobre [la creación de una [!DNL Data Landing Zone] conexión](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) de origen para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, consulte la descripción general](../../sources/home.md) de las [fuentes.
