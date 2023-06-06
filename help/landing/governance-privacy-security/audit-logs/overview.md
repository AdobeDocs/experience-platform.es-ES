---
title: Resumen de registros de auditoría
description: Descubra cómo los registros de auditoría le permiten ver quién realizó qué acciones en Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 7bb81a103c6b2a7d0baec22c927f575764bc3730
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 45%

---

# Registros de auditoría {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Acciones principales"
>abstract="Este widget muestra los principales tipos de acciones que se han realizado en Experience Platform dentro del periodo de tiempo seleccionado. Para ver la lista completa de acciones registradas en Platform, seleccione **Auditorías** en el panel de navegación situado a la izquierda."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Usuarios principales"
>abstract="Este widget muestra los usuarios que ejecutaron la mayoría de las acciones en Experience Platform dentro del periodo de tiempo seleccionado. Para ver la lista completa de acciones registradas en Platform, seleccione **Auditorías** en el panel de navegación situado a la izquierda."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Monitorización de actividades de usuarios en Platform"
>abstract="<h2>Descripción</h2><p>Puede monitorizar la actividad de los usuarios para los distintos servicios y capacidades de Platform en forma de registros de auditoría. Estos registros forman una pista de auditoría que registra <b>quién</b> realizó <b>qué</b> acción y <b>cuándo</b>. Los registros de auditoría pueden ayudar a solucionar problemas en Platform y a que su empresa cumpla de manera eficaz con las políticas corporativas de administración de datos y los requisitos regulatorios.</p>"

Para aumentar la transparencia y la visibilidad de las actividades realizadas en el sistema, Adobe Experience Platform le permite auditar la actividad del usuario para varios servicios y funcionalidades en forma de &quot;registros de auditoría&quot;. Estos registros forman una pista de auditoría que puede ayudar a solucionar problemas en Platform y ayudar a su empresa a cumplir de forma eficaz con las políticas de administración de datos corporativos y los requisitos regulatorios.

En un sentido estricto, un registro de auditoría informa de **quién** realizó **qué** acción y **cuándo** lo hizo. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

Este documento cubre los registros de auditoría en Platform, incluido cómo verlos y administrarlos en la interfaz de usuario o la API.

## Tipos de eventos capturados por los registros de auditoría {#category}

La siguiente tabla indica qué acciones sobre qué recursos de se registran en los registros de auditoría:

| Recurso | Acciones |
| --- | --- |
| [Política de control de acceso (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Cuenta (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [instancia de Attribution AI](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Disable</li></ul> |
| [Registros de auditoría](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportar</li></ul> |
| [Clase](../../../xdm/schema/composition.md#class) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| Atributo calculado | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Instancia de Customer AI](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Disable</li></ul> |
| [Conjunto de datos](../../../catalog/datasets/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para [Perfil del cliente en tiempo real](../../../profile/home.md)</li><li>Deshabilitar para el perfil</li><li>Adición de datos</li><li>Eliminar lote</li></ul> |
| [Datastream](../../../edge/datastreams/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Disable</li><li>[Editar asignación](../../../edge/datastreams/data-prep.md)</li></ul> |
| [Tipos de datos](../../../xdm/schema/composition.md#data-type) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Disable</li><li>Activar conjunto de datos</li><li>Eliminar conjunto de datos</li><li>Activar perfil</li><li>Eliminación de perfil</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Gráfico de identidad](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Ver</li></ul> |
| [Área de nombres de identidad](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Crear</li><li>Actualización</li></ul> |
| [Política de combinación](../../../profile/merge-policies/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Perfil del producto](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Consulta](../../../query-service/ui/overview.md) | <ul><li>Ejecutar</li></ul> |
| [Plantilla de consulta](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Rol (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Adición del usuario</li><li>Quitar usuario</li></ul> |
| [Zona protegida](../../../sandboxes/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Restablecer</li><li>Eliminar</li></ul> |
| [Consulta programada](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para Perfil</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Crear</li><li>Eliminar</li><li>Activar segmento</li><li>Eliminar segmento</li></ul> |
| [Flujo de datos de origen](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Activar</li><li>Disable</li><li>Activación de conjunto de datos</li><li>Eliminar conjunto de datos</li><li>Activar perfil</li><li>Eliminar perfil</li></ul> |
| [Orden de trabajo](../../../hygiene/home.md) | <ul><li>Crear</li></ul> |

## Acceso a los registros de auditoría

Cuando la función está habilitada para su organización, los registros de auditoría se recopilan automáticamente a medida que se produce la actividad. No es necesario habilitar manualmente la recopilación de registros.

Para ver y exportar los registros de auditoría, debe tener **[!UICONTROL Ver registro de actividades de usuario]** permiso de control de acceso concedido (se encuentra en la sección [!UICONTROL Gobernanza de datos] categoría). Para obtener información sobre cómo administrar permisos individuales para funciones de Platform, consulte la [documentación de control de acceso](../../../access-control/home.md).

## Administración de registros de auditoría en la IU {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <b>Auditorías</b> en la navegación izquierda. El espacio de trabajo Auditorías muestra una lista de los registros grabados, ordenados por defecto del más al menos reciente.</li>   <li> NOTA: Los registros de auditoría se conservan durante 365 días, después de los cuales se eliminarán del sistema. Por lo tanto, solo podrá retroceder un máximo de 365 días. Si necesita consultar datos con más de 365 días de antigüedad, deberá exportar los registros con regularidad para cumplir los requisitos de su directiva interna. </li><li>Seleccione un evento de la lista para ver los detalles en el carril derecho. </li><li>Seleccione el icono de canal para mostrar una lista de controles de filtro y ayudar a reducir los resultados. Solo se muestran los últimos 1000 registros, independientemente de los filtros seleccionados. </li><li>Para exportar la lista actual de registros de auditoría, seleccione **Descargar registro**.</li><li>Para obtener más ayuda sobre esta función, consulte la <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=es">información general sobre registros de auditoría</a> en Experience League.</li></ul>"

Puede ver registros de auditoría para diferentes funciones de Experience Platform dentro de la **[!UICONTROL Auditorías]** Workspace en la IU de Platform. El espacio de trabajo muestra una lista de registros registrados, ordenados de forma predeterminada de más reciente a menos reciente.

![El panel Auditorías resalta las Auditorías en el menú de la izquierda.](../../images/audit-logs/audits.png)

Los registros de auditoría se conservan durante 365 días, después de los cuales se eliminan del sistema. Por lo tanto, solo podrá retroceder un máximo de 365 días. Si necesita datos de más de 365 días, debe exportar los registros a una cadencia regular para satisfacer los requisitos de directivas internas.

Seleccione un evento de la lista para ver los detalles en el carril derecho.

![Pestaña Registro de actividades del panel Auditorías con el panel de detalles del evento resaltado.](../../images/audit-logs/select-event.png)

### Filtrar registros de auditoría

>[!NOTE]
Como es una función nueva, los datos mostrados solo se remontan a marzo de 2022. Según el recurso seleccionado, los datos anteriores podrían estar disponibles a partir de enero de 2022.


Seleccione el icono de canal (![Icono de filtro](../../images/audit-logs/icon.png)) para mostrar una lista de controles de filtro y ayudar a reducir los resultados. Solo se muestran los últimos 1000 registros, independientemente de los distintos filtros seleccionados.

![El panel Auditorías con el registro de actividad filtrado resaltado.](../../images/audit-logs/filters.png)

Los siguientes filtros están disponibles para eventos de auditoría en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Categoría] | Utilice el menú desplegable para filtrar los resultados mostrados por [categoría](#category). |
| [!UICONTROL Acción] | Filtrar por acción. Las acciones disponibles para cada servicio se pueden ver en la tabla de recursos anterior. |
| [!UICONTROL Usuario] | Introduzca el ID de usuario completo (por ejemplo, `johndoe@acme.com`) para filtrar por usuario. |
| [!UICONTROL Estado] | Filtre por si la acción se permitió (completó) o se denegó debido a la falta de [control de acceso](../../../access-control/home.md) permisos. |
| [!UICONTROL Fecha] | Seleccione una fecha de inicio o de finalización para definir un intervalo de fechas en el que filtrar los resultados. Los datos se pueden exportar con un periodo retrospectivo de 90 días (por ejemplo, del 15-12-2021 al 15-03-2022). Esto puede variar según el tipo de evento. |

Para eliminar un filtro, seleccione la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o seleccione **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![El panel Auditorías con el filtro claro resaltado.](../../images/audit-logs/clear-filters.png)

Los datos de registro de auditoría devueltos contienen la siguiente información sobre todas las consultas que cumplen los criterios de filtro seleccionados.

| El nombre de la columna | Descripción |
|---|---|
| [!UICONTROL Marca de tiempo] | La fecha y hora exactas de la acción realizada en un `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nombre de recurso] | El valor de [!UICONTROL Nombre de recurso] El campo depende de la categoría elegida como filtro. |
| [!UICONTROL Categoría] | Este campo coincide con la categoría seleccionada en la lista desplegable de filtros. |
| [!UICONTROL Acción] | Las acciones disponibles dependen de la categoría elegida como filtro. |
| [!UICONTROL Usuario] | Este campo proporciona el ID de usuario que ejecutó la consulta. |

![El panel Auditorías con el registro de actividad filtrado resaltado.](../../images/audit-logs/filtered.png)

### Exportar registros de auditoría

Para exportar la lista actual de registros de auditoría, seleccione **[!UICONTROL Descargar registro]**.

![El panel Auditorías con [!UICONTROL Descargar registro] resaltado.](../../images/audit-logs/download.png)

En el cuadro de diálogo que aparece, seleccione el formato preferido (o bien **[!UICONTROL CSV]** o **[!UICONTROL JSON]**) y seleccione **[!UICONTROL Descargar]**. El explorador descarga el archivo generado y lo guarda en el equipo.

![El cuadro de diálogo de selección de formato de archivo con [!UICONTROL Descargar] resaltado.](../../images/audit-logs/select-download-format.png)

## Administración de registros de auditoría en la API

Todas las acciones que puede realizar en la interfaz de usuario también se pueden realizar mediante llamadas a la API. Para obtener más información, consulte el [documento de la API de ](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Administración de registros de auditoría para Adobe Admin Console

Para obtener información sobre cómo administrar los registros de auditoría para las actividades en Adobe Admin Console, consulte lo siguiente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Pasos siguientes y recursos adicionales

En esta guía se explica cómo administrar los registros de auditoría en Experience Platform. Para obtener más información sobre cómo monitorizar las actividades de Platform, consulte la documentación sobre [Observability Insights](../../../observability/home.md) y [monitorización de la ingesta de datos](../../../ingestion/quality/monitor-data-ingestion.md).

Para comprender mejor los registros de auditoría en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
