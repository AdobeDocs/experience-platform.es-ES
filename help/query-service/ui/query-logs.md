---
title: Registros de consultas
description: Los registros de consultas se generan automáticamente cada vez que se ejecuta una consulta y están disponibles a través de la interfaz de usuario para ayudar a solucionar problemas. Este documento describe cómo utilizar y navegar por la sección Registros del servicio de consulta de la interfaz de usuario.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Registros de consultas

>[!IMPORTANT]
>
>Ciertas funciones de registros de consultas están actualmente en una versión limitada y no están disponibles para todos los clientes. La interfaz de usuario puede aparecer de forma ligeramente diferente sin un icono de edición. Además, es posible que el proceso de seleccionar un nombre de consulta requiera navegar al Editor de consultas en lugar de a la vista [!UICONTROL Detalles del registro de consultas].

Adobe Experience Platform mantiene un registro de todos los eventos de consulta que se producen a través de la API y la interfaz de usuario. Esta información está disponible en la interfaz de usuario del servicio de consultas de la ficha [!UICONTROL Registros].

Los archivos de registro se generan automáticamente mediante cualquier evento de consulta y contienen información como el SQL utilizado, el estado de la consulta, cuánto tiempo tardó y el último tiempo de ejecución. Puede utilizar los datos de registro de consultas como una herramienta potente para solucionar consultas ineficientes o problemáticas. Se guarda información de registro más completa como parte de la función de registro de auditoría y se puede encontrar en la [documentación del registro de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Comprobar registros de consultas {#check-query-logs}

Para comprobar los registros de consultas, seleccione [!UICONTROL Consultas] para ir al área de trabajo del servicio de consultas y seleccione [!UICONTROL Registro] de las opciones disponibles.

>[!NOTE]
>
>Tanto las consultas del sistema como las consultas del panel se excluyen de forma predeterminada. Consulte la sección [filtros](#filter-logs) para obtener información sobre cómo restringir los registros mostrados en función de su configuración.

![Interfaz de usuario de Platform con consultas y registro resaltados.](../images/ui/query-log/logs.png)

## Personalizar y buscar {#customize-and-search}

Los registros del servicio de consultas se presentan en un formato de tabla personalizable. Para personalizar las columnas de la tabla, seleccione el icono de configuración (![A icono de configuración.](../images/ui/query-log/settings-icon.png)) a la derecha de la pantalla. Aparece un cuadro de diálogo [!UICONTROL Personalizar tabla] en el que se puede anular la selección de cada columna.

También puede buscar registros relacionados con plantillas de consulta específicas escribiendo el nombre de la plantilla en el campo de búsqueda.

![Se ha resaltado el área de trabajo Registro de consultas con la barra de búsqueda y la lista desplegable Administrar tabla de columnas.](../images/ui/query-log/customize-logs.png)

Se puede encontrar una [descripción para cada una de las columnas de la tabla de registro](./overview.md#log) en la sección Registro de la descripción general del servicio de consultas.

## Detectar datos de registro

Cada fila representa los datos de registro de una ejecución de consulta asociada a una plantilla de consulta. Seleccione cualquier fila de la tabla para rellenar la barra lateral derecha con los datos de registro de esa ejecución.

![El área de trabajo Registro de consultas con una fila seleccionada y los datos de registro resaltados en la barra lateral derecha.](../images/ui/query-log/log-details.png)

En el panel de detalles del registro, puede realizar diversas acciones. Puede ejecutar la consulta como CTAS, que crea un nuevo conjunto de datos de salida, ver o copiar la consulta SQL completa que se utilizó en la ejecución o eliminar la consulta.

>[!NOTE]
>
>La opción [!UICONTROL Ejecutar como CTAS] solo está disponible para una consulta SELECT.

![El área de trabajo del registro de consultas con una fila seleccionada, Ejecutar como CTAS, Eliminar consulta y el icono de copiar SQL resaltado.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Ciertas funciones de registros de consultas están actualmente en una versión limitada y no están disponibles para todos los clientes.

También puede seleccionar un nombre de plantilla de consulta de la columna [!UICONTROL Nombre] para navegar directamente a la vista [!UICONTROL Detalles del registro de consultas].

>[!NOTE]
>
>Si la consulta se creó con la API y no se proporcionó ningún nombre de plantilla durante la inicialización, se muestran las primeras docenas de caracteres de la consulta SQL en su lugar.

![Vista de detalles del registro de consultas.](../images/ui/query-log/query-log-details.png)

## Editar registros {#edit-logs}

Junto al nombre de plantilla o al fragmento SQL de cada fila hay un icono de lápiz (![Un icono de lápiz.](../images/ui/query-log/edit-icon.png)) que puede utilizar para desplazarse hasta el Editor de consultas. A continuación, la consulta se rellena previamente en el editor para su edición.

![Área de trabajo del registro de consultas con un icono de lápiz resaltado.](../images/ui/query-log/edit-query.png)

## Filtrar registros {#filter-logs}

Puede filtrar la lista de registros de consultas en función de diferentes configuraciones. Seleccione el icono de filtro (![El icono de filtro.](../images/ui/query-log/filter-icon.png)) en la parte superior izquierda del espacio de trabajo para abrir un conjunto de opciones de filtro en el carril izquierdo.

![Área de trabajo del registro de consultas con el icono de filtro resaltado.](../images/ui/query-log/log-filter.png)

Se muestra la lista de filtros disponibles.

![Área de trabajo del registro de consultas con las opciones de filtro mostradas y resaltadas.](../images/ui/query-log/log-filter-settings.png)

En la tabla siguiente se proporciona una descripción de cada filtro.

| Filtro | Descripción |
| ------ | ----------- |
| [!UICONTROL Excluir consultas de panel] | Esta casilla de verificación está activada de forma predeterminada y excluye los registros generados por las consultas utilizadas para generar perspectivas. Estas consultas son generadas por el sistema y oscurecen los registros generados por el usuario necesarios para monitorizar, administrar y solucionar problemas. Para ver los registros generados por el sistema, desactive la casilla de verificación. |
| [!UICONTROL Excluir consultas del sistema] | Esta casilla de verificación está activada de forma predeterminada y excluye los registros generados por el sistema. Las consultas generadas por el sistema suelen incluir tareas en segundo plano u operaciones de mantenimiento que pueden no ser relevantes para la supervisión del usuario, la administración o la resolución de problemas. Si necesita inspeccionar los registros generados por el sistema, anule la selección de esta casilla de verificación para incluirlos en la vista de registro. |
| [!UICONTROL Fecha de inicio] | Para filtrar los registros de las consultas creadas durante un período específico, establezca las fechas de [!UICONTROL Inicio] y [!UICONTROL Finalización] en la sección [!UICONTROL Fecha de inicio]. |
| [!UICONTROL Fecha de finalización] | Para filtrar los registros de las consultas que se completaron durante un período específico, establezca las fechas de [!UICONTROL Inicio] y [!UICONTROL Finalización] en la sección [!UICONTROL Fecha de finalización]. |
| [!UICONTROL Estado] | Para filtrar registros basados en el [!UICONTROL Estado] de la consulta, seleccione el botón de opción apropiado. Las opciones disponibles incluyen [!UICONTROL Enviado], [!UICONTROL En curso], [!UICONTROL Correcto] y [!UICONTROL Error]. Solo puede filtrar registros en función de una condición de estado a la vez. |
| [!UICONTROL Cliente] | Para filtrar registros basados en la consulta que utilizó el cliente, escriba uno de los siguientes valores aceptados en el campo de texto libre: `API`, `Adobe Query Service UI` o `QsAccel`. |
| [!UICONTROL Mis consultas] | Utilice la opción [!UICONTROL Mis consultas] para filtrar los registros de las consultas que ejecuta. |
| [!UICONTROL id. de registro de consulta] | Para filtrar según el ID de registro único de una consulta, introduzca el ID de registro en el campo de texto libre. Esta información se encuentra en [!UICONTROL Detalles de registro]. |

Todos los filtros aplicados se muestran encima de los resultados del registro filtrado.

![Pestaña Registro del área de trabajo Consultas, con la lista de filtros aplicados resaltada.](../images/ui/query-log/applied-log-filters.png)

## Pasos siguientes

Al leer este documento, ahora comprende mejor cómo se accede a los registros de consulta y cómo se utilizan en la interfaz de usuario del servicio de consultas.

Consulte la [descripción general de la interfaz de usuario](./overview.md) o la [guía de la API del servicio de consultas](../api/getting-started.md) para obtener más información acerca de las funcionalidades del servicio de consultas.

Consulte el documento [supervisar consultas](./monitor-queries.md) para obtener información sobre cómo el servicio de consultas mejora la visibilidad de las ejecuciones de consultas programadas.
