---
title: Información general sobre registros de auditoría
description: Descubra cómo los registros de auditoría le permiten ver quién realizó qué acciones en Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: cd7ce8c107769a77373f328d9aa84c982be0d8ee
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 14%

---

# Registros de auditoría

Para aumentar la transparencia y visibilidad de las actividades realizadas en el sistema, Adobe Experience Platform permite auditar la actividad de los usuarios para diversos servicios y capacidades en forma de &quot;registros de auditoría&quot;. Estos registros forman una pista de auditoría que puede ayudar a solucionar problemas en Platform y ayudar a su empresa a cumplir de manera eficaz con las políticas de administración de datos corporativos y los requisitos regulatorios.

En un sentido básico, un registro de auditoría informa **who** performed **what** acción y **when**. Cada acción registrada en un registro contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y atributos adicionales relevantes para el tipo de acción.

Este documento cubre los registros de auditoría en Platform, incluido cómo verlos y administrarlos en la interfaz de usuario o la API.

## Tipos de eventos capturados por los registros de auditoría {#category}

La siguiente tabla indica qué acciones sobre qué recursos de se registran en los registros de auditoría:

| Recurso | Acciones |
| --- | --- |
| [Política de control de acceso (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Cuenta (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Registros de auditoría](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportar</li></ul> |
| [Clase](../../../xdm/schema/composition.md#class) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Atributo calculado](../../../profile/computed-attributes/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Conjunto de datos](../../../catalog/datasets/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para [Perfil del cliente en tiempo real](../../../profile/home.md)</li><li>Deshabilitar para perfil</li><li>Adición de datos</li><li>Eliminar lote</li></ul> |
| [Tipos de datos](../../../xdm/schema/composition.md#data-type) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Deshabilitar</li><li>Activar conjunto de datos</li><li>Eliminación de conjunto de datos</li><li>Activar perfil</li><li>Eliminación de perfil</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Gráfico de identidad](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Ver</li></ul> |
| [Área de nombres de identidad](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Crear</li><li>Actualización</li></ul> |
| [Combinar directiva](../../../profile/merge-policies/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Perfil del producto](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Consulta](../../../query-service/ui/overview.md) | <ul><li>Ejecutar</li></ul> |
| [Plantilla de consulta](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Función (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Adición del usuario</li><li>Eliminar usuario</li></ul> |
| [Zona protegida](../../../sandboxes/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Restablecer</li><li>Eliminar</li></ul> |
| [Consulta programada](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para perfil</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Crear</li><li>Eliminar</li><li>Activar segmento</li><li>Eliminación de segmentos</li></ul> |
| [Flujo de datos de origen](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Deshabilitar</li><li>Activación de conjunto de datos</li><li>Eliminación de conjunto de datos</li><li>Activate de perfil</li><li>Eliminación de perfil</li></ul> |
| [Orden de trabajo](../../../hygiene/home.md) | <ul><li>Crear</li></ul> |

## Acceso a registros de auditoría

Cuando la función está habilitada para su organización, los registros de auditoría se recopilan automáticamente a medida que se produce la actividad. No es necesario habilitar manualmente la recopilación de registros.

Para ver y exportar los registros de auditoría, debe tener la variable **[!UICONTROL Ver registro de actividades del usuario]** permiso de control de acceso concedido (encontrado en la sección [!UICONTROL Administración de datos] ). Para obtener información sobre cómo administrar permisos individuales para las funciones de Platform, consulte la [documentación de control de acceso](../../../access-control/home.md).

## Administración de registros de auditoría en la interfaz de usuario

Puede ver los registros de auditoría de las distintas funciones del Experience Platform en el **[!UICONTROL Auditorías]** en la interfaz de usuario de Platform. El espacio de trabajo muestra una lista de registros registrados, ordenados de forma predeterminada de los más recientes a los menos recientes.

![Panel de registros de auditoría](../../images/audit-logs/audits.png)

Los registros de auditoría se conservan durante 365 días después de los cuales se eliminarán del sistema. Por lo tanto, solo puede volver durante un periodo máximo de 365 días. Si necesita datos de más de 365 días, debe exportar los registros en una cadencia normal para satisfacer los requisitos de políticas internas.

Seleccione un evento de la lista para ver sus detalles en el carril derecho.

![Detalles del evento](../../images/audit-logs/select-event.png)

### Filtrar registros de auditoría

>[!NOTE]
>
>Dado que se trata de una función nueva, los datos mostrados solo se remontan a marzo de 2022. Según el recurso seleccionado, es posible que los datos anteriores estén disponibles a partir de enero de 2022.


Seleccione el icono de canal (![Icono de filtro](../../images/audit-logs/icon.png)) para mostrar una lista de controles de filtro para ayudar a reducir los resultados. Solo se muestran los últimos 1000 registros independientemente de los distintos filtros seleccionados.

![Filtros](../../images/audit-logs/filters.png)

Los siguientes filtros están disponibles para eventos de auditoría en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Categoría] | Utilice el menú desplegable para filtrar los resultados mostrados por [categoría](#category). |
| [!UICONTROL Acción] | Filtrar por acción. Actualmente solo [!UICONTROL Crear] y [!UICONTROL Eliminar] las acciones se pueden filtrar. |
| [!UICONTROL Usuario] | Introduzca el ID de usuario completo (por ejemplo, `johndoe@acme.com`) para filtrar por usuario. |
| [!UICONTROL Estado] | Filtrar por si la acción fue permitida (completada) o denegada debido a la falta de [control de acceso](../../../access-control/home.md) permisos. |
| [!UICONTROL Fecha] | Seleccione una fecha de inicio o una fecha de finalización para definir un intervalo de fechas por el que filtrar los resultados. Los datos se pueden exportar con un periodo retrospectivo de 90 días (por ejemplo, 2021-12-15 a 2022-03-15). Esto puede variar según el tipo de evento. |

Para quitar un filtro, seleccione la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o seleccione **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![Borrar filtros](../../images/audit-logs/clear-filters.png)

### Exportar registros de auditoría

Para exportar la lista actual de registros de auditoría, seleccione **[!UICONTROL Descargar registro]**.

![Descargar registro](../../images/audit-logs/download.png)

En el cuadro de diálogo que aparece, seleccione el formato que desee (ya sea **[!UICONTROL CSV]** o **[!UICONTROL JSON]**) y, a continuación, seleccione **[!UICONTROL Descargar]**. El explorador descarga el archivo generado y lo guarda en el equipo.

![Seleccionar formato de descarga](../../images/audit-logs/select-download-format.png)

## Administración de registros de auditoría en la API

Todas las acciones que puede realizar en la interfaz de usuario también se pueden realizar mediante llamadas a la API . Consulte la [Documento de referencia de API](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obtener más información.

## Administración de registros de auditoría para Adobe Admin Console

Para obtener información sobre cómo administrar los registros de auditoría de actividades en Adobe Admin Console, consulte lo siguiente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Pasos siguientes y recursos adicionales

Esta guía abarcaba cómo administrar los registros de auditoría en Experience Platform. Para obtener más información sobre cómo monitorizar las actividades de Platform, consulte la documentación de [Perspectivas de la capacidad de observación](../../../observability/home.md) y [monitorización de la ingesta de datos](../../../ingestion/quality/monitor-data-ingestion.md).

Para comprender mejor los registros de auditoría en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
