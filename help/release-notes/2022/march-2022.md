---
title: Notas de la versión de Adobe Experience Platform, marzo de 2022
description: Notas de la versión de marzo de 2022 para Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 30 de marzo de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Registros de auditoría](#audit-logs)
- [Cuentas relacionadas en Real-Time CDP B2B Edition](#related-accounts)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Recopilación de datos](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Fuentes](#sources)

## Registros de auditoría {#audit-logs}

Experience Platform le permite auditar la actividad de los usuarios en relación con diversos servicios y funcionalidades. Los registros de auditoría proporcionan información sobre quién hizo qué y cuándo.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Registros de auditoría para conjunto de datos, esquema, clase, grupo de campos, tipo de datos, entorno limitado, destino, segmento, política de combinación, atributo calculado, perfil de producto y cuenta (Adobe) | Estos son los recursos que se registran en los registros de auditoría. Si la función está habilitada, los registros de auditoría se recopilarán automáticamente a medida que se produzca la actividad. No es necesario habilitar manualmente la recopilación de registros. |
| Exportar registros de auditoría | Los registros de auditoría se pueden descargar como un `CSV` o `JSON` archivo. Los archivos generados se guardan directamente en el equipo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los registros de auditoría en Platform, consulte la [información general sobre registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Cuentas relacionadas en Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La función Cuentas relacionadas solo está disponible para clientes de Real-Time CDP B2B Edition.

A menudo, las empresas B2B tienen la información de sus clientes almacenada en múltiples sistemas, cada uno de los cuales incluye solamente datos parciales o incluso contradictorios para la misma entidad comercial del mundo real. Esto crea un enorme desafío de llegar a una visión precisa de sus clientes, reduciendo así la eficiencia y eficacia de sus esfuerzos de ventas y marketing B2B. Con el lanzamiento de cuentas relacionadas, [!DNL Real-Time CDP B2B] ahora muestra una lista de cuentas similares a la cuenta que está explorando. Puede incluir las cuentas relacionadas en las definiciones de segmentos para ampliar su alcance o aplicar criterios más amplios en sus segmentos.

Obtenga más información sobre la función en las siguientes páginas de documentación:

- [Resumen de cuentas relacionadas en Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Ficha Cuentas relacionadas en la guía de la interfaz de usuario del perfil de la cuenta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Cómo utilizar cuentas relacionadas en definiciones de segmentos](../../rtcdp/segmentation/b2b.md#related-accounts)

Para obtener más información sobre Real-Time CDP B2B Edition, consulte la [información general](../../rtcdp/overview.md).

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a distintas reglas de alerta a través de la [!UICONTROL Alertas] en la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas reglas de alerta | Ya hay disponibles dos nuevas reglas de alerta para las fuentes relacionadas con la ingesta de datos. Consulte la descripción general sobre [reglas de alerta](../../observability/alerts/rules.md) para la lista actualizada de tipos de alertas. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las alertas en Platform, consulte la [información general sobre alertas](../../observability/alerts/overview.md).

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través de la cual puede ver información importante sobre los datos de su organización, tal como se captura durante las instantáneas diarias.

### Tableros de perfil

El panel Perfiles muestra una instantánea de los datos de atributo (registro) que su organización tiene en el Experience Platform Almacenamiento de perfiles .

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget Perfiles sin segmentar | La utilidad proporciona el número total de perfiles que no están adjuntos a ningún segmento. El número generado es preciso a partir de la última instantánea y representa la oportunidad de activar perfiles en toda la organización. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| Widget de tendencias de perfiles sin segmentar | Esta utilidad proporciona una ilustración gráfica de líneas del número de perfiles que no están adjuntos a ningún segmento durante un período de tiempo determinado. La tendencia se puede visualizar en periodos de 30 días, 90 días y 12 meses. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| Perfiles sin segmentar por utilidad de identidad | Esta utilidad categoriza el número total de perfiles sin segmentar por su identificador único. Los datos se visualizan en un gráfico de barras. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |
| utilidad de perfiles de identidad única | Esta utilidad proporciona un recuento de los perfiles de su organización que solo tienen un tipo de ID que crea su identidad, ya sea un correo electrónico o un ECID. Consulte la [documentación de widgets estándar de perfiles](../../dashboards/guides/profiles.md#standard-widgets) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los paneles Perfiles, consulte la [Información general sobre los paneles de perfiles](../../dashboards/guides/profiles.md).

### Tableros de destinos

El panel Destinos muestra una instantánea de los destinos que su organización ha habilitado en el Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de recuento de destinos | La utilidad proporciona el número total de extremos disponibles en los que se puede activar y enviar una audiencia dentro del sistema. Este número incluye destinos tanto activos como inactivos. Consulte la [documentación de utilidades estándar de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre los paneles Destinos en Platform, consulte la [Información general sobre los paneles Destinos](../../dashboards/guides/destinations.md).

## Recopilación de datos {#data-collection}

Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Configuración del conjunto de datos global | Ahora puede configurar varias nuevas configuraciones globales al configurar un conjunto de datos: ubicación geográfica, cookie de ID de origen y sincronización de ID de terceros. Consulte la sección sobre [configuración de un conjunto de datos](../../edge/datastreams/overview.md#create) en la guía de interfaz de usuario de Datastreams para obtener más información. |
| [API del servidor de red perimetral](../../server-api/overview.md) | La API de servidor permite a los clientes interactuar con la red perimetral del Experience Platform mediante un nuevo punto final autenticado para potenciar una variedad de casos de uso de recopilación, personalización, publicidad y marketing. |

Para obtener más información sobre la recopilación de datos en Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

## Servicio de consultas {#query-service}

[!DNL Query Service] permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| `table_exists` | El nuevo comando de funciones se utiliza para confirmar si existe o no una tabla en el sistema. El comando devuelve un valor booleano: `true` si la tabla **does** existe, y `false` si la tabla lo hace **not** existe. Consulte la [Documentación de sintaxis SQL](../../query-service/sql/syntax.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las funciones disponibles, consulte la [Información general del servicio de consultas](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar la ingesta de datos en todo.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Ya hay nuevas fuentes disponibles para el uso de B2B | Ahora puede usar todas las fuentes disponibles en Platform para casos de uso B2B. Consulte la [catálogo de fuentes](../../sources/home.md) para obtener una lista completa de las fuentes disponibles. |
| Disponibilidad general del nuevo [!DNL Oracle Eloqua] source | Ahora puede usar la variable [!DNL Oracle Eloqua] de origen a la ingesta perfecta de datos de su [!DNL Oracle Eloqua] instancia (cuenta, campaña, contactos) a Platform. Consulte la documentación sobre [creación de [!DNL Oracle Eloqua] conexión de origen](../../sources/connectors/marketing-automation/oracle-eloqua.md) para obtener más información. |
| Mejoras de API para [!DNL Data Landing Zone] | La variable [!DNL Data Landing Zone] el origen ahora es compatible con la detección automática de las propiedades de los archivos al usar la variable [!DNL Flow Service] API. Consulte la documentación sobre [crear un [!DNL Data Landing Zone] conexión de origen](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
