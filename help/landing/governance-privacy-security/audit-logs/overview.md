---
title: Resumen de registros de auditoría
description: Descubra cómo los registros de auditoría le permiten ver quién realizó qué acciones en Adobe Experience Platform.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: acbd46b5810a491d838f1c4c3366d19c91c15d51
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 32%

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

En un sentido básico, un registro de auditoría indica a **quién** realizó **qué** acción y **cuándo**. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

>[!NOTE]
>
> Los metadatos de las acciones **Agregar usuario** y **Quitar usuario** dentro del recurso **Rol** no contendrán el ID de correo electrónico del usuario que realizó la acción. En su lugar, los registros mostrarán el ID de correo electrónico generado por el sistema (system@adobe.com).

Este documento cubre los registros de auditoría en Platform, incluido cómo verlos y administrarlos en la interfaz de usuario o la API.

## Tipos de eventos capturados por los registros de auditoría {#category}

La siguiente tabla indica qué acciones sobre qué recursos se registran en los registros de auditoría:

| Recurso | Acciones |
| --- | --- |
| [Directiva de control de acceso (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Cuenta (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Instancia de inteligencia artificial aplicada a la atribución](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar</li><li>Deshabilitar</li></ul> |
| [Registros de auditoría](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportar</li></ul> |
| [Clase](../../../xdm/schema/composition.md#class) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| Atributo calculado | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Instancia de inteligencia artificial aplicada al cliente](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar</li><li>Deshabilitar</li></ul> |
| [Conjunto de datos](../../../catalog/datasets/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para [Perfil del cliente en tiempo real](../../../profile/home.md)</li><li>Deshabilitar para el perfil</li><li>Adición de datos</li><li>Eliminar lote</li></ul> |
| [Flujo de datos](../../../datastreams/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar</li><li>Deshabilitar</li><li>[Editar asignación](../../../datastreams/data-prep.md)</li></ul> |
| [Tipos de datos](../../../xdm/schema/composition.md#data-type) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Destino](../../../destinations/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar</li><li>Deshabilitar</li><li>Activación de conjunto de datos</li><li>Eliminación de conjunto de datos</li><li>Activación de perfil</li><li>Eliminación de perfil</li></ul> |
| [Grupo de campos](../../../xdm/schema/composition.md#field-group) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Gráfico de identidad](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Ver</li></ul> |
| [Área de nombres de identidad](../../../identity-service/features/namespaces.md) | <ul><li>Crear</li><li>Actualización</li></ul> |
| [Política de combinación](../../../profile/merge-policies/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Perfil del producto](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Consulta](../../../query-service/ui/overview.md) | <ul><li>Ejecutar</li></ul> |
| [Plantilla de consulta](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Rol (control de acceso basado en atributos)](../../../access-control/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Adición de usuario</li><li>Quitar usuario</li></ul> |
| [espacio aislado](../../../sandboxes/home.md) | <ul><li>Crear</li><li>Actualización</li><li>Restablecer</li><li>Eliminar</li></ul> |
| [Consulta programada](../../../query-service/ui/overview.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li></ul> |
| [Esquema](../../../xdm/schema/composition.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar para el perfil</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Crear</li><li>Eliminar</li><li>Activación de segmentos</li><li>Eliminar segmento</li></ul> |
| [Flujo de datos de Source](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crear</li><li>Actualización</li><li>Eliminar</li><li>Habilitar</li><li>Deshabilitar</li><li>Activación de conjunto de datos</li><li>Eliminación de conjunto de datos</li><li>Activar perfil</li><li>Eliminación de perfil</li></ul> |
| [Orden de trabajo](../../../hygiene/home.md) | <ul><li>Crear</li></ul> |

## Acceso a los registros de auditoría

Cuando la función está habilitada para su organización, los registros de auditoría se recopilan automáticamente a medida que se produce la actividad. No es necesario habilitar manualmente la recopilación de registros.

Para ver y exportar los registros de auditoría, debe contar con el permiso de control de acceso **[!UICONTROL Ver registro de actividad de usuario]** concedido (que se encuentra en la categoría [!UICONTROL Control de datos]). Para obtener información sobre cómo administrar permisos individuales para las características de Platform, consulte la [documentación de control de acceso](../../../access-control/home.md).

## Administración de registros de auditoría en la interfaz de usuario {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <b>Auditorías</b> en la navegación izquierda. El espacio de trabajo Auditorías muestra una lista de los registros grabados, ordenados por defecto del más al menos reciente.</li>   <li> NOTA: Los registros de auditoría se conservan durante 365 días, después de los cuales se eliminarán del sistema. Por lo tanto, solo podrá retroceder un máximo de 365 días. Si necesita consultar datos con más de 365 días de antigüedad, deberá exportar los registros con regularidad para cumplir los requisitos de su directiva interna. </li><li>Seleccione un evento de la lista para ver los detalles en el carril derecho. </li><li>Seleccione el icono de canal para mostrar una lista de controles de filtro y ayudar a reducir los resultados. Solo se muestran los últimos 1000 registros, independientemente de los filtros seleccionados. </li><li>Para exportar la lista actual de registros de auditoría, seleccione **Descargar registro**.</li><li>Para obtener más ayuda sobre esta función, consulte la <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=es">información general sobre registros de auditoría</a> en Experience League.</li></ul>"

Puede ver los registros de auditoría de distintas características de Experience Platform en el espacio de trabajo **[!UICONTROL Auditorías]** de la interfaz de usuario de Platform. El espacio de trabajo muestra una lista de registros registrados, ordenados de forma predeterminada de más reciente a menos reciente.

![El panel Auditorías resalta las Auditorías en el menú de la izquierda.](../../images/audit-logs/audits.png)

Los registros de auditoría se conservan durante 365 días, después de los cuales se eliminan del sistema. Si necesita datos de más de 365 días, debe exportar los registros a una cadencia regular para satisfacer los requisitos de directivas internas.

El método que utiliza para solicitar los registros de auditoría cambia el período de tiempo permitido y el número de registros a los que tendrá acceso. [Exportar registros](#export-audit-logs) le permite retroceder 365 días (en intervalos de 90 días) a un máximo de 1000 registros, mientras que la [interfaz de usuario del registro de actividad](#filter-audit-logs) en Experience Platform muestra los últimos 90 días a un máximo de 1000 registros.

Seleccione un evento de la lista para ver los detalles en el carril derecho.

![Pestaña Registro de actividades del panel de auditorías con el panel de detalles del evento resaltado.](../../images/audit-logs/select-event.png)

### Filtrar registros de auditoría

Seleccione el icono de canal (![Icono de filtro](/help/images/icons/filter.png)) para mostrar una lista de controles de filtro y ayudar a reducir los resultados.

>[!NOTE]
>
>La interfaz de usuario de Experience Platform solo muestra los últimos 90 días hasta un máximo de 1000 registros, independientemente de los filtros aplicados. Si necesita registrar más allá de eso (hasta un máximo de 365 días), necesitará [exportar los registros de auditoría](#export-audit-logs).

![Panel de auditorías con el registro de actividad filtrado resaltado.](../../images/audit-logs/filters.png)

Los siguientes filtros están disponibles para eventos de auditoría en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Categoría] | Utilice el menú desplegable para filtrar los resultados mostrados por [categoría](#category). |
| [!UICONTROL Acción] | Filtrar por acción. Las acciones disponibles para cada servicio se pueden ver en la tabla de recursos anterior. |
| [!UICONTROL Usuario] | Escriba el identificador de usuario completo (por ejemplo, `johndoe@acme.com`) para filtrar por usuario. |
| [!UICONTROL Estado] | Filtre por si la acción se permitió (completó) o se denegó debido a la falta de [permisos de control de acceso](../../../access-control/home.md). |
| [!UICONTROL Fecha] | Seleccione una fecha de inicio o de finalización para definir un intervalo de fechas en el que filtrar los resultados. Los datos se pueden exportar con un periodo retrospectivo de 90 días (por ejemplo, del 15-12-2021 al 15-03-2022). Esto puede variar según el tipo de evento. |

Para quitar un filtro, selecciona la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o selecciona **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![Se resaltó el panel Auditorías con el filtro sin cifrar.](../../images/audit-logs/clear-filters.png)

Los datos de registro de auditoría devueltos contienen la siguiente información sobre todas las consultas que cumplen los criterios de filtro seleccionados.

| Nombre de columna | Descripción |
|---|---|
| [!UICONTROL Marca de tiempo] | La fecha y hora exactas de la acción realizada en formato `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Nombre de recurso] | El valor del campo [!UICONTROL Nombre del recurso] depende de la categoría elegida como filtro. |
| [!UICONTROL Categoría] | Este campo coincide con la categoría seleccionada en la lista desplegable de filtros. |
| [!UICONTROL Acción] | Las acciones disponibles dependen de la categoría elegida como filtro. |
| [!UICONTROL Usuario] | Este campo proporciona el ID de usuario que ejecutó la consulta. |

![Panel de auditorías con el registro de actividad filtrado resaltado.](../../images/audit-logs/filtered.png)

### Exportar registros de auditoría {#export-audit-logs}

Para exportar la lista actual de registros de auditoría, seleccione **[!UICONTROL Descargar registro]**.

>[!NOTE]
>
>Los registros se pueden solicitar en intervalos de 90 días hasta 365 días antes. Sin embargo, la cantidad máxima de registros que se pueden devolver durante una sola exportación es de 10 000.

![Se ha resaltado el panel Auditorías con el [!UICONTROL registro de descargas].](../../images/audit-logs/download.png)

En el cuadro de diálogo que aparece, seleccione el formato que prefiera (**[!UICONTROL CSV]** o **[!UICONTROL JSON]**) y, a continuación, seleccione **[!UICONTROL Descargar]**. El explorador descarga el archivo generado y lo guarda en el equipo.

![Se resaltó el cuadro de diálogo de selección de formato de archivo con [!UICONTROL Descargar].](../../images/audit-logs/select-download-format.png)

## Habilitar alertas {#enable-alerts}

Puede activar alertas de auditoría para recibir notificaciones para las siguientes reglas:

* Creación de público
* Actualización de público
* Eliminación de público
* Creación de conjunto de datos
* Actualización de conjunto de datos
* Eliminación de conjunto de datos
* Creación de esquema
* Actualización de esquema
* Eliminación de esquema

Seleccione la alerta que desee en la lista para suscribirse y recibir notificaciones. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas mediante la interfaz de usuario](../../../observability/alerts/ui.md).

## Administración de registros de auditoría en la API

Todas las acciones que puede realizar en la interfaz de usuario también se pueden realizar mediante llamadas a la API. Consulte el [documento de referencia de API](https://www.adobe.io/experience-platform-apis/references/audit-query/) para obtener más información.

## Administración de registros de auditoría para Adobe Admin Console

Para obtener información sobre cómo administrar los registros de auditoría para las actividades en Adobe Admin Console, consulte el siguiente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Pasos siguientes y recursos adicionales

En esta guía se explica cómo administrar los registros de auditoría en Experience Platform. Para obtener más información sobre cómo monitorizar las actividades de Platform, consulte la documentación sobre [Observability Insights](../../../observability/home.md) y [supervisión de la ingesta de datos](../../../ingestion/quality/monitor-data-ingestion.md).

Para comprender mejor los registros de auditoría en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
