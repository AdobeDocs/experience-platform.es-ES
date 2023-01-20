---
title: Integración del registro de auditoría del servicio de consultas
description: Los registros de auditoría del servicio de consulta mantienen registros de diversas acciones del usuario para formar una pista de auditoría para solucionar problemas o cumplir con las políticas y los requisitos regulatorios de administración de datos corporativos. Este tutorial proporciona información general sobre las funciones del registro de auditoría específicas del servicio de consulta.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] integración del registro de auditoría

Adobe Experience Platform [!DNL Query Service] la integración del registro de auditoría proporciona registros de las acciones del usuario relacionadas con la consulta. Los registros de auditoría son una herramienta esencial para solucionar problemas y cumplir con las políticas de administración de datos corporativos y los requisitos regulatorios. La funcionalidad permite devolver un registro de acción para muchos tipos de eventos y filtrar y exportar los registros. Se puede acceder a los registros a través de la interfaz de usuario de Platform o a través de la [API de consulta de auditoría](https://www.adobe.io/experience-platform-apis/references/audit-query/) y descargado en los formatos de archivo CSV o JSON.

Para obtener más información sobre la interfaz de usuario de registros de auditoría, consulte la [documento de información general sobre registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md). Para obtener más información sobre cómo realizar llamadas a las API de plataforma, consulte la [guía de API de registros de auditoría](../../landing/api-guide.md).

## Requisitos previos

Debe tener la variable [!DNL Data Governance] [!UICONTROL Ver registro de actividades del usuario] permiso habilitado para ver el panel de registro de auditoría en la interfaz de usuario de Platform. El permiso se habilita a través del Adobe [Admin Console](https://adminconsole.adobe.com/). Póngase en contacto con el administrador de su organización si no tiene privilegios de administrador para habilitar este permiso. Consulte la documentación de control de acceso para [instrucciones completas para añadir permisos mediante Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorías del registro de auditoría {#audit-log-categories}

Las categorías del registro de auditoría proporcionadas por [!DNL Query Service] son los siguientes:

| Categoría | Descripción |
|---|---|
| [!UICONTROL Consulta] | Esta categoría permite auditar las ejecuciones de consultas. |
| [!UICONTROL Plantilla de consulta] | Esta categoría permite auditar las distintas acciones (crear, actualizar y eliminar) realizadas en una plantilla de consulta. |
| [!UICONTROL Consulta programada] | Esta categoría le permite auditar las programaciones que se han creado, actualizado o eliminado en [!DNL Query Service]. |

## Realizar una [!DNL Query Service] registro de auditoría {#perform-an-audit-log}

Para realizar una auditoría de [!DNL Query Service] actividades, seleccionar **[!UICONTROL Auditorías]** desde la navegación de la izquierda, seguido del icono de canal (![Un icono de filtro.](../images/audit-log/filter.png)) para mostrar una lista de controles de filtro para ayudar a reducir los resultados.

![El tablero de registro de auditoría de la interfaz de usuario de la plataforma con &quot;Audits&quot; en el panel de navegación izquierdo y controles de filtro resaltados.](../images/audit-log/filter-controls.png)

En el [!UICONTROL Auditorías] tablero [!UICONTROL Registro de actividades] , puede filtrar todas las acciones de Platform registradas por cualquiera de las [!DNL Query Service] categorías. Los resultados de registro se pueden filtrar aún más en función del período de tiempo en el que se ejecutaron, la acción o función realizada o el usuario que ha realizado la consulta. Consulte la documentación del registro de auditoría para [instrucciones completas sobre cómo filtrar los registros en función de categoría, acción, usuario y estado](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Los datos de registro de auditoría devueltos contienen la siguiente información sobre todas las consultas que cumplen los criterios de filtro seleccionados.

| El nombre de la columna | Descripción |
|---|---|
| [!UICONTROL Marca de tiempo] | La fecha y hora exactas de la acción realizada en un `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nombre del recurso] | El valor de la variable [!UICONTROL Nombre del recurso] depende de la categoría elegida como filtro. Al usar la variable [!UICONTROL Consulta programada] categoría que es la **nombre de la programación**. Al usar la variable [!UICONTROL Plantilla de consulta] , esta es la categoría **nombre de plantilla**. Al usar la variable [!UICONTROL Consulta] , esta es la categoría **session ID** |
| [!UICONTROL Categoría] | Este campo coincide con la categoría seleccionada en la lista desplegable de filtros. |
| [!UICONTROL Acción] | Puede crear, eliminar, actualizar o ejecutar. Las acciones disponibles dependen de la categoría elegida como filtro. |
| [!UICONTROL Usuario] | Este campo proporciona el ID de usuario que ejecutó la consulta. |

![El tablero Audits con el registro de actividad filtrado resaltado.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Para obtener más detalles de la consulta, descargue los resultados de registro en los formatos de archivo CSV o JSON, de los que se muestran de forma predeterminada en el panel de registro de auditoría.

## Panel Detalles

Seleccione cualquier fila de resultados del registro de auditoría para abrir un panel de detalles a la derecha de la pantalla.

![Audita la pestaña Registro de actividades del tablero con el panel de detalles resaltado.](../images/audit-log/details-panel.png)

El panel de detalles se puede usar para encontrar la variable [!UICONTROL ID del recurso] y [!UICONTROL Estado del evento].

El valor de la variable [!UICONTROL ID del recurso] cambia según la categoría utilizada en la auditoría.

* Al usar la variable [!UICONTROL Consulta] categoría, [!UICONTROL ID del recurso] es la variable  **session ID**.
* Al usar la variable [!UICONTROL Plantilla de consulta] categoría, [!UICONTROL ID del recurso] es la variable **ID de plantilla** con el prefijo `[!UICONTROL templateID:]`.
* Al usar la variable [!UICONTROL Consulta programada] categoría, [!UICONTROL ID del recurso] es la variable  **ID de programación** con el prefijo `[!UICONTROL scheduleID:]`.

El valor de la variable [!UICONTROL Estado del evento] cambia según la categoría utilizada en la auditoría.

* Al usar la variable [!UICONTROL Consulta] categoría, [!UICONTROL Estado del evento] proporciona una lista de todos los **ID de consulta** ejecutado por el usuario en esa sesión.
* Al usar la variable [!UICONTROL Plantilla de consulta] categoría, [!UICONTROL Estado del evento] proporciona la variable **nombre de plantilla** como prefijo del estado del evento.
* Al usar la variable [!UICONTROL Programación de consultas] categoría, [!UICONTROL Estado del evento] proporciona la variable **nombre de la programación** como prefijo del estado del evento.

## Filtros disponibles para [!DNL Query Service] categorías del registro de auditoría {#available-filters}

Los filtros disponibles varían en función de la categoría seleccionada en la lista desplegable. La siguiente tabla detalla los filtros disponibles para [[!DNL Query Service] categorías del registro de auditoría](#audit-log-categories).

| Filtro | Descripción |
|---|---|
| Categoría | Consulte la [[!DNL Query Service] categorías del registro de auditoría](#audit-log-categories) para obtener una lista completa de las categorías disponibles. |
| Acción | Al hacer referencia a [!DNL Query Service] categorías de auditoría, actualización es un **modificación del formulario existente**, la eliminación es la **eliminación de la programación o plantilla**, crear es **creación de una nueva programación o plantilla** y ejecutar es **ejecución de una consulta**. |
| Usuario | Introduzca el ID de usuario completo (por ejemplo, johndoe@acme.com) para filtrar por usuario. |
| Estado | La variable [!UICONTROL Permitir], [!UICONTROL Correcto]y [!UICONTROL Fallo] las opciones filtran los registros en función del &quot;estado&quot; o el &quot;estado del evento&quot;, mientras que la variable [!UICONTROL Denegar] se filtrará **all** registros. |
| Fecha | Seleccione una fecha de inicio o una fecha de finalización para definir un intervalo de fechas por el que filtrar los resultados. |

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión del [!DNL Query Service] registro de auditoría y cómo se puede usar para filtrar su [!DNL Query Service] acciones del usuario.

Si está utilizando la variable [!DNL Query Service] registro de auditoría para solucionar problemas, se recomienda leer el [guía de solución de problemas](../troubleshooting-guide.md).
