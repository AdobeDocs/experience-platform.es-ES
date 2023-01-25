---
title: Registros de consultas
description: Los registros de consulta se generan automáticamente cada vez que se ejecuta una consulta y están disponibles a través de la interfaz de usuario para ayudarle a solucionar el problema. Este documento describe cómo utilizar y desplazarse por la sección Registros del servicio de consulta de la interfaz de usuario.
source-git-commit: 22deca5f9bcf6bcf97cca01b97fce9d22800b767
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Registros de consultas

Adobe Experience Platform mantiene un registro de todos los eventos de consulta que se producen a través de la API y la IU. Esta información está disponible en la interfaz de usuario del servicio de consultas desde el [!UICONTROL Registros] pestaña .

Los archivos de registro se generan automáticamente por cualquier evento de consulta y contienen información, incluido el SQL utilizado, el estado de la consulta, cuánto tiempo tardó y el último tiempo de ejecución. Los datos de registro de consultas se pueden usar como herramienta potente para solucionar problemas o consultas ineficientes. La información de registro más completa se conserva como parte de la función de registro de auditoría y se puede encontrar en la [documentación del registro de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md).

## Comprobar registros de consultas

Para comprobar los registros de consulta, seleccione [!UICONTROL Consultas] para desplazarse al espacio de trabajo del servicio de consulta y seleccione [!UICONTROL Registro] de las opciones disponibles.

![Interfaz de usuario de Platform con Consultas y Registro resaltados.](../images/ui/query-log/logs.png)

## Personalizar y buscar {#customize-and-search}

Los registros del servicio de consulta se presentan en un formato de tabla personalizable. Para personalizar las columnas de la tabla, seleccione el icono de configuración (![Un icono de configuración.](../images/ui/query-log/settings-icon.png)) a la derecha de la pantalla. A [!UICONTROL Personalizar tabla] aparece el cuadro de diálogo donde se puede anular la selección de cada columna.

También puede buscar registros relacionados con plantillas de consulta específicas escribiendo el nombre de la plantilla en el campo de búsqueda.

![El espacio de trabajo Registro de consultas con la barra de búsqueda y la lista desplegable administrar tabla de columnas resaltadas.](../images/ui/query-log/customize-logs.png)

A [descripción de cada una de las columnas de la tabla de registro](./overview.md#log) se encuentra en la sección Registro de la descripción general del servicio de consulta.

## Datos de registro de Discover

Cada fila representa los datos de registro de una ejecución de consulta asociada a una plantilla de consulta. Seleccione cualquier fila de la tabla para rellenar la barra lateral derecha con los datos de registro para esa ejecución.

![El espacio de trabajo Registro de consultas con una fila seleccionada y los datos de registro en la barra lateral derecha resaltados.](../images/ui/query-log/log-details.png)

En el panel de detalles del registro, puede seleccionar un nuevo conjunto de datos de salida y ver o copiar la consulta SQL completa que se utilizó en la ejecución.

![El espacio de trabajo Registro de consultas con una fila seleccionada y el conjunto de datos de salida y la consulta SQL resaltados.](../images/ui/query-log/edit-output-dataset.png)

También puede seleccionar un nombre de plantilla de consulta en la [!UICONTROL Nombre] para navegar directamente a la [!UICONTROL Detalles del registro de consultas] vista.

>[!NOTE]
>
>Si la consulta se creó con la API y no se proporcionó ningún nombre de plantilla durante la inicialización, se muestran las primeras decenas de caracteres de la consulta SQL.

![La vista Detalles del registro de consultas .](../images/ui/query-log/query-log-details.png)

Al lado del nombre de plantilla de cada fila o del fragmento SQL hay un icono de lápiz (![Un icono de lápiz.](../images/ui/query-log/edit-icon.png)) que puede utilizar para ir al Editor de consultas. A continuación, la consulta se rellena previamente en el editor para su edición.

![El espacio de trabajo Registro de consultas con un icono de lápiz resaltado.](../images/ui/query-log/edit-query.png)

## Pasos siguientes

Al leer este documento, ahora tiene una mejor comprensión de cómo se accede y utiliza a los registros de consulta en la interfaz de usuario del servicio de consultas.

Consulte la [Información general sobre la IU](./overview.md)o [Guía de API del servicio de consulta](../api/getting-started.md) para obtener más información sobre las funcionalidades del servicio de consulta.

Consulte la [documento de consultas de monitor](./monitor-queries.md) para conocer cómo el servicio de consulta mejora la visibilidad de las ejecuciones de consultas programadas.
