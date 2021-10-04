---
title: Información general sobre registros de auditoría
description: Descubra cómo los registros de auditoría le permiten ver quién realizó qué acciones en Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d4beb7691c8fb38359425509a40572ea9b09fd26
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 5%

---

# Registros de auditoría (Beta)

>[!IMPORTANT]
>
>La función de registros de auditoría de Adobe Experience Platform se encuentra actualmente en fase beta y es posible que su organización no tenga acceso a ella aún. La funcionalidad descrita en esta documentación está sujeta a cambios.

Para aumentar la transparencia y visibilidad de las actividades realizadas en el sistema, Adobe Experience Platform permite auditar la actividad de los usuarios para diversos servicios y capacidades en forma de &quot;registros de auditoría&quot;. Estos registros forman una pista de auditoría que puede ayudar a solucionar problemas en Platform y ayudar a su empresa a cumplir de manera eficaz con las políticas de administración de datos corporativos y los requisitos regulatorios.

En un sentido básico, un registro de auditoría indica a **quién** realizó **qué** acción y **cuándo**. Cada acción registrada en un registro contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y atributos adicionales relevantes para el tipo de acción.

Este documento cubre los registros de auditoría en Platform, incluido cómo verlos y administrarlos en la interfaz de usuario o la API.

## Tipos de eventos capturados por los registros de auditoría {#category}

En la tabla siguiente se describen las acciones en las que los registros de auditoría registran los recursos:

| Recurso | Acciones |
| --- | --- |
| [Conjunto de datos](../../../catalog/datasets/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para [Perfil del cliente en tiempo real](../../../profile/home.md)</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Clase](../../../xdm/schema/composition.md#class) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Tipo de datos](../../../xdm/schema/composition.md#data-type) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Entorno de pruebas](../../../sandboxes/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Restablecer</li><li>Eliminar</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Activar</li></ul> |

## Acceso a registros de auditoría

Cuando la función está habilitada para su organización, los registros de auditoría se recopilan automáticamente a medida que se produce la actividad. No es necesario habilitar manualmente la recopilación de registros.

Para ver y exportar los registros de auditoría, debe tener el permiso de control de acceso &quot;Ver registros de auditoría&quot; concedido (que se encuentra en la categoría &quot;Control de datos&quot;). Para obtener información sobre cómo administrar permisos individuales para funciones de Platform, consulte la [documentación de control de acceso](../../../access-control/home.md).

## Administración de registros de auditoría en la interfaz de usuario

Puede ver los registros de auditoría de distintas funciones de Experience Platform en el espacio de trabajo **[!UICONTROL Audits]** de la interfaz de usuario de Platform. El espacio de trabajo muestra una lista de registros registrados, ordenados de forma predeterminada de los más recientes a los menos recientes.

![Panel de registros de auditoría](../../images/audit-logs/audits.png)

El sistema solo muestra los registros de auditoría del último año. Todos los registros que superen este límite se eliminarán automáticamente del sistema.

Seleccione un evento de la lista para ver sus detalles en el carril derecho.

![Detalles del evento](../../images/audit-logs/select-event.png)

Seleccione el icono de canal (![Filtro icono](../../images/audit-logs/icon.png)) para mostrar una lista de controles de filtro para ayudar a reducir los resultados.

![Filtros](../../images/audit-logs/filters.png)

Los siguientes filtros están disponibles para eventos de auditoría en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Categoría] | Utilice el menú desplegable para filtrar los resultados mostrados por [categoría](#category). |
| [!UICONTROL Acción] | Filtrar por acción. Actualmente solo se pueden filtrar las acciones [!UICONTROL Create] y [!UICONTROL Delete]. |
| [!UICONTROL Estado de control de acceso] | Filtre por si la acción fue permitida (completada) o denegada debido a la falta de permisos de [control de acceso](../../../access-control/home.md). |
| [!UICONTROL Fecha] | Seleccione una fecha de inicio o una fecha de finalización para definir un intervalo de fechas por el que filtrar los resultados. |

Para quitar un filtro, seleccione la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o seleccione **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![Borrar filtros](../../images/audit-logs/clear-filters.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Administración de registros de auditoría en la API

Todas las acciones que puede realizar en la interfaz de usuario también se pueden realizar mediante llamadas a la API . Consulte el [documento de referencia de API](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obtener más información.

## Administración de registros de auditoría para Adobe Admin Console

Para aprender a administrar los registros de auditoría de las actividades en Adobe Admin Console, consulte el siguiente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Pasos siguientes

Esta guía abarcaba cómo administrar los registros de auditoría en Experience Platform. Para obtener más información sobre cómo monitorizar las actividades de Platform, consulte la documentación sobre [Observability Insights](../../../observability/home.md) y [monitorización de la incorporación de datos](../../../ingestion/quality/monitor-data-ingestion.md).
