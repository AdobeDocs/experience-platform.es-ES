---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para monitorizar los flujos de datos de flujo continuo desde el espacio de trabajo de fuentes.
solution: Experience Platform
title: Monitorizar flujos de datos para fuentes de transmisión en la interfaz de usuario
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---


# Monitorizar flujos de datos para fuentes de transmisión en la interfaz de usuario

Este tutorial trata los pasos para monitorizar los flujos de datos para fuentes de flujo continuo mediante el espacio de trabajo [!UICONTROL Sources].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../../../dataflows/home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
   * [Se ejecuta](../../notifications.md) el flujo de datos: Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitorización de flujos de datos para fuentes de flujo continuo

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Para ver los flujos de datos existentes para las fuentes de flujo continuo, seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior.

![catálogo](../../images/tutorials/monitor-streaming/catalog.png)

La página [!UICONTROL Flujos de datos] contiene una lista de todos los flujos de datos existentes en su organización, incluida información sobre sus datos de origen, nombre de cuenta y estado de ejecución del flujo de datos.

Seleccione el nombre del flujo de datos que desea ver.

![flujos de datos](../../images/tutorials/monitor-streaming/dataflows.png)

La siguiente tabla contiene más información sobre los estados de ejecución de flujo de datos:

| Estado | Descripción |
| ------ | ----------- |
| Completado | El estado `Completed` indica que todos los registros de la ejecución de flujo de datos correspondiente se procesaron dentro del período de una hora. Un estado `Completed` aún puede contener errores en las ejecuciones de flujo de datos. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos. |
| Error | El estado `Error` indica que se ha interrumpido el proceso de activación de un flujo de datos. |

La página [!UICONTROL Actividad de flujo de datos] muestra información específica sobre el flujo de datos de flujo continuo. El banner superior contiene el número acumulado de registros ingestados y los registros fallidos para todas las ejecuciones de flujo de datos de flujo continuo en el intervalo de fechas seleccionado.

La mitad inferior de la página muestra información sobre el número de registros recibidos, anidados y fallidos por ejecución de flujo. Cada ejecución de flujo se registra dentro de una ventana por hora.

![actividad de flujo de datos](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

* **[!UICONTROL Inicio]** de la ejecución del flujo de datos: Hora a la que comenzó la ejecución del flujo de datos.
* **[!UICONTROL Tiempo]** de procesamiento: Cantidad de tiempo que tardó el flujo de datos en procesarse.
* **[!UICONTROL Registros recibidos]**: Número total de registros recibidos en el flujo de datos desde un conector de origen.
* **[!UICONTROL Registros ingestados]**: Recuento total de registros introducidos en  [!DNL Data Lake].
* **[!UICONTROL Registros fallidos]**: Número de registros que no se incorporaron en  [!DNL Data Lake] debido a errores en los datos.
* **[!UICONTROL Tasa de ingesta]**: La tasa de éxito de los registros introducidos en  [!DNL Data Lake]. Esta métrica se aplica cuando [!UICONTROL Ingesta parcial] está habilitada.
* **[!UICONTROL Estado]**: Representa el estado en el que se encuentra el flujo de datos:   Completada o  [!UICONTROL Procesamiento].  Completado significa que todos los registros de la ejecución de flujo de datos correspondiente se procesaron dentro del período de una hora.  Procesamiento significa que la ejecución del flujo de datos aún no ha finalizado.

De forma predeterminada, los datos mostrados contienen tasas de ingesta de los últimos siete días. Seleccione **[!UICONTROL Last 7 days]** para ajustar el lapso de tiempo de los registros mostrados.

![cambio de hora](../../images/tutorials/monitor-streaming/change-time.png)

Aparece una ventana emergente de calendario que proporciona opciones para intervalos de tiempo de ingesta alternativos. Seleccione **[!UICONTROL Últimos 30 días]** y, a continuación, seleccione **[!UICONTROL Aplicar]**.

![calendario](../../images/tutorials/monitor-streaming/calendar.png)

Para ver los detalles de una ejecución de flujo de datos específica, incluidos sus errores, seleccione la hora de inicio de la ejecución en la lista.

![select-failed](../../images/tutorials/monitor-streaming/select-fail.png)

La página [!UICONTROL Información general de la ejecución del flujo de datos] contiene información adicional sobre el flujo de datos, como su ID de ejecución del flujo de datos correspondiente, el conjunto de datos de destino y el ID de organización de IMS.

Un flujo ejecutado con errores también contiene el panel [!UICONTROL Dataflow run errors], que muestra el error en particular que provocó el fallo de la ejecución, así como el recuento total de registros que fallaron.

![error](../../images/tutorials/monitor-streaming/failure.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para supervisar los flujos de datos de flujo continuo e identificar los errores que han producido cualquier flujo de datos fallido. Consulte los siguientes documentos para obtener más información:

* [Resumen de fuentes](../../home.md)
* [Información general de flujos de datos](../../../dataflows/home.md)