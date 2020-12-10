---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para ver flujos de datos existentes desde el espacio de trabajo Fuentes.
solution: Experience Platform
title: Monitoreo de flujos de datos
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4d99526a592e173e3b46e1fa2a3f869b1fe5d4f2
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 1%

---


# Monitorear flujos de datos para orígenes en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para ver flujos de datos existentes desde el espacio de trabajo [!UICONTROL Fuentes] .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../sources/home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Simuladores](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitoreo de flujos de datos

Inicie sesión en la interfaz de usuario [del](https://platform.adobe.com) Experience Platform y, a continuación, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Fuentes] . Seleccione **[!UICONTROL Flujos]** de datos del encabezado superior para vista de flujos de datos existentes.

![catalog-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

Aparece una lista de flujos de datos existentes. En esta página hay una lista de flujos de datos visualizables, incluida información sobre su origen, nombre de usuario, número de flujos de datos y estado.

Consulte la siguiente tabla para obtener más información sobre los estados:

| Estado | Descripción |
| ------ | ----------- |
| Habilitado | El `Enabled` estado indica que un flujo de datos está activo y que está invirtiendo datos según la programación que se proporcionó. |
| Desactivado | El estado `Disabled` indica que un flujo de datos está inactivo y no está invirtiendo ningún dato. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos. |
| Error | El `Error` estado indica que se ha interrumpido el proceso de activación de un flujo de datos. |

Seleccione el icono del canal en la parte superior izquierda para ordenar.

![lista de flujos de datos](../assets/ui/monitor-sources/dataflows-list.png)

Aparece el panel de ordenación. Seleccione el origen al que desea acceder desde el menú de desplazamiento y seleccione el flujo de datos desde la lista de la derecha. También puede seleccionar el botón de elipses (`...`) para que aparezcan más opciones disponibles para el flujo de datos seleccionado.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

La página **[!UICONTROL actividad]** de flujo de datos contiene detalles sobre el número de registros ingestados y de registros fallidos, así como información sobre el estado de flujo de datos y el tiempo de procesamiento. Seleccione el icono de calendario que hay encima del flujo de datos para ajustar el intervalo de tiempo de los registros de ingestión.

![datflow-actividad](../assets/ui/monitor-sources/dataflow-activity.png)

El calendario permite la vista de los distintos intervalos de tiempo para los registros ingestados. Puede elegir seleccionar una de las dos opciones predefinidas &quot;[!UICONTROL Últimos 7 días]&quot; o &quot;[!UICONTROL Últimos 30 días]&quot;. También puede establecer un intervalo de tiempo personalizado mediante el calendario. Seleccione el intervalo de tiempo que desee y seleccione **[!UICONTROL Aplicar]** para continuar.

![flow-calendar](../assets/ui/monitor-sources/flow-calendar.png)

De forma predeterminada, la actividad **** Flujo de datos muestra el panel **[!UICONTROL Propiedades]** asociado al flujo de datos. Seleccione el flujo ejecutado desde la lista para ver sus metadatos asociados, incluida la información sobre su ID de ejecución única.

Seleccione **[!UICONTROL inicio]** de ejecución de flujo de datos para acceder a la información general **[!UICONTROL de ejecución de flujo de]** datos.

![corre](../assets/ui/monitor-sources/run-metadata.png)

La **[!UICONTROL información general]** de ejecución de flujo de datos muestra información sobre el flujo de datos, incluidos sus metadatos, el estado de ingestión parcial y el umbral de error asignado. El encabezado superior también incluye un resumen de errores. El resumen **[!UICONTROL de]** errores contiene el error específico de nivel superior que muestra en qué paso el proceso de ingestión encontró un error.

![dataflow run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

Consulte la siguiente tabla para ver los errores que se pueden ver en el resumen **[!UICONTROL de]** errores.

| Error | Descripción |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Error al copiar datos de un origen. |
| `CONNECTOR-2001-500` | Error al procesar los datos copiados en [!DNL Platform]. Este error puede deberse a analizar, validar o transformar. |

La mitad inferior de la pantalla contiene información sobre los errores **[!UICONTROL de ejecución de]** Dataflow. Desde aquí, también puede realizar vistas de los archivos ingestados, realizar previsualizaciones y descargar diagnósticos de error o descargar el manifiesto de archivo.

La sección Errores **[!UICONTROL de ejecución de flujo de]** datos muestra el código de error, el número de registros en los que se ha producido un error y la información que describe el error.

Seleccione los diagnósticos **[!UICONTROL de error de]** Previsualización para ver más información sobre el error de inserción.

![Errores de ejecución de flujo de datos](../assets/ui/monitor-sources/dataflow-run-errors.png)

Aparece el panel previsualización **[!UICONTROL de diagnóstico de]** errores. Esta pantalla muestra información específica sobre el error de inserción, incluido el nombre del archivo, el código de error, el nombre de la columna en la que se produjo el error y una descripción del error.

Esta sección también incluye una previsualización de la columna que contiene el error.

>[!IMPORTANT]
>
>Para habilitar la previsualización **[!UICONTROL de diagnósticos de]** error, debe activar los diagnósticos de ingestión **** parcial y **[!UICONTROL error al configurar un flujo de datos]** . Al hacerlo, el sistema podrá analizar todos los registros ingestados durante la ejecución del flujo.

![Previsualización-error-diagnósticos](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Después de obtener una vista previa de los errores, puede seleccionar **[!UICONTROL Descargar]** desde el panel de información general **** de las ejecuciones de flujo de datos para acceder a los diagnósticos de error completos y descargar el manifiesto del archivo. Consulte los documentos sobre diagnóstico [de](../../ingestion/batch-ingestion/partial.md#retrieve-errors) errores y [descarga de metadatos](../../ingestion/batch-ingestion/partial.md#download-metadata) para obtener más información.

![Previsualización-error-diagnósticos](../assets/ui/monitor-sources/download.png)

Para obtener más información sobre la supervisión de flujos de datos y la ingestión, consulte el tutorial sobre la [supervisión de flujos de datos](../../ingestion/quality/monitor-data-ingestion.md)de flujo continuo.

## Pasos siguientes

Siguiendo este tutorial, se ha accedido correctamente a las cuentas y flujos de datos existentes desde el espacio de trabajo **[!UICONTROL Fuentes]** . Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../data-science-workspace/home.md)
