---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
source-git-commit: 04d35137a301492794ab8c0c67183cf5c76f2105
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 30 de marzo de 2022**

Nuevas funciones de Adobe Experience Platform:

- [Registros de auditoría](#audit-logs)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Alertas](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Modelo de datos de experiencia (XDM)](#xdm)
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

Para obtener más información sobre los paneles Perfiles, consulte la [Información general sobre los paneles de perfiles](../../dashboards/guides/profiles.md).

### Tableros de destinos

El panel Destinos muestra una instantánea de los destinos que su organización ha habilitado en el Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de recuento de destinos | La utilidad proporciona el número total de extremos disponibles en los que se puede activar y enviar una audiencia dentro del sistema. Este número incluye destinos tanto activos como inactivos. Consulte la [documentación de utilidades estándar de destinos](../../dashboards/guides/destinations.md#standard-widgets) para obtener más información. |

Para obtener más información sobre los paneles Destinos en Platform, consulte la [Información general sobre los paneles Destinos](../../dashboards/guides/destinations.md).

## Modelo de datos de experiencia (XDM) {#xdm}

Experience Data Model (XDM) es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

| Función | Descripción |
| --- | --- |
| Adición o eliminación de campos estándar individuales para un esquema | La interfaz de usuario del Editor de esquemas ahora le permite añadir partes de grupos de campos estándar a sus esquemas, lo que proporciona más flexibilidad para los campos que elija incluir sin necesidad de crear recursos personalizados desde cero.<br><br>Ahora también puede definir campos personalizados específicos directamente dentro de la estructura de esquema y asignarlos a un grupo de campos personalizados nuevo o existente sin necesidad de crear o editar el grupo de campos de antemano.<br><br>Consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../xdm/ui/resources/schemas.md) para obtener más información sobre estos nuevos flujos de trabajo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

[!DNL Query Service] permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos desde la [!DNL Data Lake] y capturan los resultados de la consulta como un nuevo conjunto de datos para su uso en informes, Data Science Workspace o para su incorporación al perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| `table_exists` | El nuevo comando de funciones se utiliza para confirmar si existe o no una tabla en el sistema. El comando devuelve un valor booleano: `true` si la tabla **does** existe, y `false` si la tabla lo hace **not** existe. Consulte la [Documentación de sintaxis SQL](../../query-service/sql/syntax.md) para obtener más información. |

Para obtener más información sobre las funciones disponibles, consulte la [Información general del servicio de consultas](../../query-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar la ingesta de datos en todo.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Ya hay nuevas fuentes disponibles para el uso de B2B | Ahora puede usar todas las fuentes disponibles en Platform para casos de uso B2B. Consulte la [catálogo de fuentes](../../sources/home.md) para obtener una lista completa de las fuentes disponibles. |
| Disponibilidad general del nuevo [!DNL Oracle Eloqua] source | Ahora puede usar la variable [!DNL Oracle Eloqua] de origen a la ingesta perfecta de datos de su [!DNL Oracle Eloqua] instancia (cuenta, campaña, contactos) a Platform. Consulte la documentación sobre [creación de [!DNL Oracle Eloqua] conexión de origen](../../sources/connectors/oracle-eloqua.md) para obtener más información. |
| Mejoras de API para [!DNL Data Landing Zone] | La variable [!DNL Data Landing Zone] el origen ahora es compatible con la detección automática de las propiedades de los archivos al usar la variable [!DNL Flow Service] API. Consulte la documentación sobre [crear un [!DNL Data Landing Zone] conexión de origen](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
