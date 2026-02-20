---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2026'
description: Las notas de la versión de febrero de 2026 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 05c9a99132d1385f9ec043bb667a72304b17a9b5
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 48%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: miércoles, 17 de febrero de 2026**

Estas son las nuevas funciones y actualizaciones en Adobe Experience Platform:

- [Alertas](#alerts)
- [Destinos](#destinations)
- [Servicio de segmentación](#segmentation-service)
- [Fuentes](#sources)
- [Modelo de datos de experiencia (XDM)](#xdm)

## Alertas {#alerts}

Experience Platform le permite suscribirse a alertas basadas en eventos para diversas actividades de Experience Platform. Puede suscribirse a distintas reglas de alerta a través de la ficha [!UICONTROL Alerts] de la interfaz de usuario de Experience Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o mediante notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Integración de [!DNL Slack] para alertas de cara al cliente | Ahora puede enviar alertas de cara al cliente a [!DNL Slack]. Siga el [tutorial paso a paso](../../observability/alerts/slack-integration.md) para configurar la integración de [!DNL Slack] y recibir notificaciones de alerta directamente en el área de trabajo de [!DNL Slack]. |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Observability Insights] información general](../../observability/home.md).

## Destinos {#destinations}

Los [!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados**

| Destino | Descripción |
| --- | --- |
| [[!DNL Snowflake] Lote](../../destinations/catalog/warehouses/snowflake-batch.md) disponible en general | El destino del lote [!DNL Snowflake] ya está disponible de forma general. Los clientes de Real-Time CDP de todo el mundo ahora pueden utilizar este conector para activar datos en sus cuentas de Snowflake sin necesidad de copiar físicamente los datos. Se han eliminado todas las limitaciones de la versión limitada (disponibilidad para clientes solo de EE. UU., compatibilidad con audiencias que pertenecen únicamente a la política de combinación predeterminada). |

{style="table-layout:auto"}

**Correcciones y mejoras**

| Se ha corregido un problema que hacía que se mostrara | Descripción |
| --- | --- |
| Alerta Tasa de activaciones fallidas superadas | La alerta de destino Tasa de activaciones fallidas superadas ahora utiliza correctamente el umbral configurado al evaluar y enviar la alerta. Anteriormente, la alerta se activaba con una tasa de error del 1 % independientemente del porcentaje que configurara. Consulte [reglas de alerta estándar](../../observability/alerts/rules.md#destinations) para obtener más información sobre esta alerta. |
| Informes de identidades excluidas de Customer Match de Google | Se ha corregido un error en la lógica de recuento de registros omitidos que provocaba que se mostraran recuentos inflados de perfiles excluidos para los destinos de Customer Match de Google. El comportamiento de activación y exportación no se vio afectado; solo las cifras notificadas eran incorrectas. |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Servicio de segmentación {#segmentation-service}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de serie temporal que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Audiencias de API editables | Ahora puede editar audiencias creadas mediante la API del servicio de segmentación o Audience Agent en el Generador de segmentos. **Nota:** Las audiencias que contienen datos de series temporales **no se pueden** editar en este momento mediante el Generador de segmentos. |
| Actualización de caducidad de datos de audiencia externa | Puede utilizar la API del servicio de segmentación para ampliar la caducidad de los datos de sus audiencias externas. Para obtener más información, lea la [guía de API para audiencias externas](/help/segmentation/api/external-audiences.md#extend-data-expiration). |

Para obtener más información, lea la [[!DNL Segmentation Service] información general](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Fuentes nuevas o actualizadas**

| Fuente | Descripción |
| --- | --- |
| Compatibilidad con el catálogo Unity en el conector de origen [!DNL Databricks] | El conector de origen [!DNL Databricks] ahora es compatible con Unity Catalog. Lea la documentación actualizada de [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) para aprender a utilizar el catálogo Unity al configurar la conexión de origen. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

| Función | Descripción |
| --- | --- |
| Edición restringida para esquemas con conjuntos de datos | Las operaciones de edición que resultan en cambios importantes ahora están restringidas una vez que existe un conjunto de datos para un esquema. Cuando se asocia un conjunto de datos, ya no puede cambiar el nombre ni eliminar campos, cambiar los tipos de datos o formatos de los campos, modificar los descriptores de identidad, administrar campos relacionados para eliminar campos existentes o cambiar la clase asignada; los cambios aditivos y la obsolescencia de los campos siguen siendo compatibles. |

Para obtener más información, lea la [información general sobre XDM](../../xdm/home.md).

