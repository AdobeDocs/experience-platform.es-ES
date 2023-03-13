---
title: Integración del registro de auditoría del servicio de consultas
description: Los registros de auditoría del servicio de consultas mantienen registros de diversas acciones del usuario para formar una pista de auditoría para la resolución de problemas o el cumplimiento de las políticas de administración de datos corporativos y los requisitos regulatorios. Este tutorial proporciona información general sobre las funciones del registro de auditoría específicas del servicio de consultas.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] integración del registro de auditoría

El Adobe Experience Platform [!DNL Query Service] la integración del registro de auditoría proporciona registros de las acciones de usuario relacionadas con las consultas. Los registros de auditoría son una herramienta esencial para solucionar problemas y cumplir con las políticas de administración de datos corporativos y los requisitos regulatorios. La capacidad permite devolver un registro de acciones para muchos tipos de eventos y filtrar y exportar los registros. Se puede acceder a los registros a través de la interfaz de usuario de Platform o de [API de consulta de auditoría](https://www.adobe.io/experience-platform-apis/references/audit-query/) y descargado en formato de archivo CSV o JSON.

Para obtener más información sobre la interfaz de usuario de registros de auditoría, consulte la [documento de información general de registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md). Para obtener más información sobre cómo realizar llamadas a las API de Platform, consulte la [guía de API de registros de auditoría](../../landing/api-guide.md).

## Requisitos previos

Debe tener el [!DNL Data Governance] [!UICONTROL Ver registro de actividades de usuario] permiso habilitado para ver el tablero de registro de auditoría en la interfaz de usuario de Platform. El permiso se habilita mediante el Adobe [Admin Console](https://adminconsole.adobe.com/). Póngase en contacto con el administrador de su organización si no tiene privilegios de administrador para habilitar este permiso. Consulte la documentación de control de acceso para [instrucciones completas para agregar permisos mediante Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorías de registro de auditoría {#audit-log-categories}

Las categorías de registro de auditoría proporcionadas por [!DNL Query Service] son los siguientes.

| Categoría | Descripción |
|---|---|
| [!UICONTROL Consulta] | Esta categoría le permite auditar las ejecuciones de consultas. |
| [!UICONTROL Plantilla de consulta] | Esta categoría le permite auditar las distintas acciones (crear, actualizar y eliminar) realizadas en una plantilla de consulta. |
| [!UICONTROL Consulta programada] | Esta categoría le permite auditar las programaciones que se han creado, actualizado o eliminado en [!DNL Query Service]. |

## Realice una [!DNL Query Service] registro de auditoría {#perform-an-audit-log}

Para realizar una auditoría para [!DNL Query Service] actividades, seleccione **[!UICONTROL Auditorías]** desde la navegación izquierda, seguido del icono de canal (![Un icono de filtro.](../images/audit-log/filter.png)) para mostrar una lista de controles de filtro y ayudar a reducir los resultados.

![El panel de registro de auditoría de la IU de Platform con &quot;Auditorías&quot; en los controles de navegación y filtro izquierdos resaltados.](../images/audit-log/filter-controls.png)

Desde el [!UICONTROL Auditorías] tablero [!UICONTROL Registro de actividades] , puede filtrar todas las acciones de Platform registradas por cualquiera de las [!DNL Query Service] categorías. Los resultados del registro se pueden filtrar aún más en función del período de tiempo en que se ejecutaron, la acción/función realizada o el usuario que implementó la consulta. Consulte la documentación del registro de auditoría para [instrucciones completas sobre cómo filtrar los registros en función de la categoría, acción, usuario y estado](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Los datos de registro de auditoría devueltos contienen la siguiente información sobre todas las consultas que cumplen los criterios de filtro seleccionados.

| El nombre de la columna | Descripción |
|---|---|
| [!UICONTROL Marca de tiempo] | La fecha y hora exactas de la acción realizada en un `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nombre de recurso] | El valor de [!UICONTROL Nombre de recurso] El campo depende de la categoría elegida como filtro. Al usar el [!UICONTROL Consulta programada] categoría esta es la **nombre de programación**. Al usar el [!UICONTROL Plantilla de consulta] categoría, esta es la **nombre de plantilla**. Al usar el [!UICONTROL Consulta] categoría, esta es la **session ID** |
| [!UICONTROL Categoría] | Este campo coincide con la categoría seleccionada por usted en la lista desplegable de filtros. |
| [!UICONTROL Acción] | Esto puede ser crear, eliminar, actualizar o ejecutar. Las acciones disponibles dependen de la categoría elegida como filtro. |
| [!UICONTROL Usuario] | Este campo proporciona el ID de usuario que ejecutó la consulta. |

![El panel Auditorías con el registro de actividad filtrado resaltado.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>La descarga de los resultados del registro en los formatos de archivo CSV o JSON proporciona más detalles de consulta que los mostrados de forma predeterminada en el panel de registro de auditoría.

## Panel Detalles

Seleccione cualquier fila de resultados de registro de auditoría para abrir un panel de detalles a la derecha de la pantalla.

![Pestaña Registro de actividades del panel Auditorías con el panel de detalles resaltado.](../images/audit-log/details-panel.png)

El panel de detalles se puede utilizar para encontrar la variable [!UICONTROL ID de recurso] y el [!UICONTROL Estado del evento].

El valor del [!UICONTROL ID de recurso] cambia según la categoría utilizada en la auditoría.

* Al usar el [!UICONTROL Consulta] categoría, la [!UICONTROL ID de recurso] es el  **session ID**.
* Al usar el [!UICONTROL Plantilla de consulta] categoría, la [!UICONTROL ID de recurso] es el **ID de plantilla** y con el prefijo `[!UICONTROL templateID:]`.
* Al usar el [!UICONTROL Consulta programada] categoría, la [!UICONTROL ID de recurso] es el  **ID de programación** y con el prefijo `[!UICONTROL scheduleID:]`.

El valor del [!UICONTROL Estado del evento] cambia según la categoría utilizada en la auditoría.

* Al usar el [!UICONTROL Consulta] categoría, la [!UICONTROL Estado del evento] proporciona una lista de todos los **ID de consulta** ejecutado por el usuario dentro de esa sesión.
* Al usar el [!UICONTROL Plantilla de consulta] categoría, la [!UICONTROL Estado del evento] El campo proporciona el **nombre de plantilla** como prefijo del estado del evento.
* Al usar el [!UICONTROL Programación de consultas] categoría, la [!UICONTROL Estado del evento] El campo proporciona el **nombre de programación** como prefijo del estado del evento.

## Filtros disponibles para [!DNL Query Service] categorías de registro de auditoría {#available-filters}

Los filtros disponibles varían según la categoría seleccionada en la lista desplegable. La siguiente tabla detalla los filtros disponibles para [[!DNL Query Service] categorías de registro de auditoría](#audit-log-categories).

| Filtro | Descripción |
|---|---|
| Categoría | Consulte la [[!DNL Query Service] categorías de registro de auditoría](#audit-log-categories) para obtener una lista completa de las categorías disponibles. |
| Acción | Al hacer referencia a [!DNL Query Service] categorías de auditoría, la actualización es una **modificación del formulario existente**, delete es el **eliminación de la programación o plantilla**, crear es **creación de una nueva programación o plantilla**, y ejecutar es **ejecución de una consulta**. |
| Usuario | Introduzca el ID de usuario completo (por ejemplo, johndoe@acme.com) para filtrar por usuario. |
| Estado | El [!UICONTROL Permitir], [!UICONTROL Correcto], y [!UICONTROL Error] Las opciones de filtran los registros en función del &quot;Estado&quot; o del &quot;Estado del evento&quot;, mientras que las opciones de [!UICONTROL Denegar] opción filtrará hacia fuera **todo** registros. |
| Fecha | Seleccione una fecha de inicio o de finalización para definir un intervalo de fechas en el que filtrar los resultados. |

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión del [!DNL Query Service] función de registro de auditoría y cómo se puede utilizar para filtrar su [!DNL Query Service] acciones del usuario.

Si utiliza el complemento [!DNL Query Service] función de registro de auditoría para solucionar problemas, se recomienda leer el [guía de solución de problemas](../troubleshooting-guide.md).
