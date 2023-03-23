---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para monitorizar los flujos de datos de flujo continuo desde el espacio de trabajo de fuentes.
title: Monitorizar flujos de datos para fuentes de transmisión en la interfaz de usuario
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Monitorizar flujos de datos para fuentes de transmisión en la interfaz de usuario

Este tutorial trata los pasos para monitorizar los flujos de datos para fuentes de flujo continuo mediante el [!UICONTROL Fuentes] espacio de trabajo.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Flujos de datos](../../../dataflows/home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile]y [!DNL Destinations].
   * [Ejecuciones de flujo de datos](../../notifications.md): Las ejecuciones de flujo de datos son los trabajos programados recurrentes basados en la configuración de frecuencia de los flujos de datos seleccionados.
* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitorización de flujos de datos para fuentes de flujo continuo

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Para ver los flujos de datos existentes de las fuentes de flujo continuo, seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior.

![catálogo](../../images/tutorials/monitor-streaming/catalog.png)

La variable [!UICONTROL Flujos de datos] contiene una lista de todos los flujos de datos existentes en su organización, incluida la información sobre sus datos de origen, el nombre de cuenta y el estado de ejecución del flujo de datos.

Seleccione el nombre del flujo de datos que desea ver.

![flujos de datos](../../images/tutorials/monitor-streaming/dataflows.png)

La siguiente tabla contiene más información sobre los estados de ejecución de flujo de datos:

| Estado | Descripción |
| ------ | ----------- |
| Completado | La variable `Completed` indica que todos los registros de la ejecución de flujo de datos correspondiente se procesaron dentro del período de una hora. A `Completed` El estado de aún puede contener errores en las ejecuciones de flujo de datos. |
| Correcto | La variable `Success` indica que todos los registros de la ejecución de flujo de datos correspondiente se procesaron dentro del período de una hora y que no se encontraron errores durante el curso de la ejecución del flujo de datos. |
| Procesamiento | La variable `Processing` indica que un flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos. |
| Error | La variable `Error` indica que se ha interrumpido el proceso de activación de un flujo de datos. |
| Sin ejecuciones | La variable `No runs` estado indica que se creó el flujo de datos, pero que no se iniciaron ejecuciones de flujo de datos. |

La variable [!UICONTROL Actividad de flujo de datos] muestra información específica sobre el flujo de datos de flujo continuo. El banner superior contiene el número acumulado de registros ingestados y los registros fallidos para todas las ejecuciones de flujo de datos de flujo continuo en el intervalo de fechas seleccionado.

![actividad de flujo de datos](../../images/tutorials/monitor-streaming/dataflow-activity.png)

De forma predeterminada, los datos mostrados contienen tasas de ingesta de los últimos siete días. Select **[!UICONTROL Últimos 7 días]** para ajustar el lapso de tiempo de los registros mostrados.

Aparece una ventana emergente de calendario que proporciona opciones para intervalos de tiempo de ingesta alternativos. Puede configurar el intervalo de tiempo de ejecución del flujo de datos para ver las ejecuciones de flujo de los últimos siete días o de los últimos 30 días. Como alternativa, puede configurar el calendario interactivo para establecer un intervalo de tiempo personalizado de su elección. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![calendario](../../images/tutorials/monitor-streaming/calendar.png)

La mitad inferior de la página muestra información sobre el número de registros recibidos, anidados y fallidos por ejecución de flujo. Cada ejecución de flujo se registra dentro de una ventana por hora.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Métricas de ejecución de flujo de datos {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Registros recibidos"
>abstract="La métrica Registros recibidos indica el recuento total de registros recibidos en el flujo de datos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Registros ingestados"
>abstract="La métrica Registros ingestados indica el recuento total de registros ingeridos en el lago de datos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Error de registros"
>abstract="La métrica Registros fallidos indica el recuento total de registros que no se incorporaron al lago de datos debido a errores en los datos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Registros con advertencias"
>abstract="Los registros con advertencias indican el recuento total de registros ingeridos con advertencias de transformación del asignador. Todos los errores de transformación del asignador se notifican como advertencias y las filas parcialmente incorporadas se consideran correctas con una advertencia"
>text="Learn more in documentation"

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

* **[!UICONTROL Inicio de la ejecución del flujo de datos]**: Hora a la que comenzó la ejecución del flujo de datos.
* **[!UICONTROL Tiempo de procesamiento]**: Cantidad de tiempo que tardó el flujo de datos en procesarse.
* **[!UICONTROL Registros recibidos]**: Número total de registros recibidos en el flujo de datos desde un conector de origen.
* **[!UICONTROL Registros ingestados]**: El recuento total de registros ingestados en [!DNL Data Lake].
* **[!UICONTROL Registros con advertencias]**: Recuento total de registros con advertencias que se incorporaron. Todos los errores de transformación del asignador se notifican como advertencias y las filas que se incorporan parcialmente se etiquetan como `success` con una advertencia. **Nota**: La compatibilidad con la ingesta de registros con advertencias solo está disponible para fuentes de flujo continuo.
* **[!UICONTROL Registros fallidos]**: El número de registros que no se incorporaron en [!DNL Data Lake] debido a errores en los datos.
* **[!UICONTROL Tasa de ingesta]**: La tasa de éxito de los registros introducidos en [!DNL Data Lake]. Esta métrica es aplicable cuando [!UICONTROL Ingesta parcial] está activada.
* **[!UICONTROL Estado]**: Representa el estado en el que se encuentra el flujo de datos: o [!UICONTROL Completado] o [!UICONTROL Procesamiento]. [!UICONTROL Completado] significa que todos los registros de la ejecución del flujo de datos correspondiente se procesaron dentro del período de una hora. [!UICONTROL Procesamiento] significa que la ejecución del flujo de datos aún no ha finalizado.

La variable [!UICONTROL Resumen de ejecución de flujo de datos] contiene información adicional sobre el flujo de datos, como su ID de ejecución de flujo de datos correspondiente, el conjunto de datos de destino y el ID de organización.

Un flujo ejecutado con errores también contiene la variable [!UICONTROL Errores de ejecución del flujo de datos] , que muestra el error en particular que provocó el fallo de la ejecución, así como el recuento total de registros que fallaron.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Ver registros con advertencias {#warnings}

[!UICONTROL Registros con advertencias] muestra una lista de advertencias de transformación del asignador que se produjeron durante la ejecución del flujo. Las filas parcialmente ingeridas se consideran correctas y se añaden con advertencias si se encuentran errores de transformación del asignador.

De forma predeterminada, todos los errores de transformación del asignador se consideran advertencias, excepto si son cualquiera de los siguientes:

* Errores de sintaxis
* Referencias a atributos que no existen
* Discordancia entre los tipos de datos XDM

Para ver los diagnósticos de error, seleccione **[!UICONTROL Previsualizar diagnósticos de error]**.

![registros con advertencias](../../images/tutorials/monitor-streaming/records-with-warnings.png)

La variable [!UICONTROL Vista previa del diagnóstico de errores] permite obtener una vista previa de hasta 100 errores o advertencias relacionados con la ejecución del flujo de datos. Desde aquí también puede descargar el manifiesto de error de ingesta para obtener más información, utilizando la variable [!DNL Data Access] API.

![diagnóstico](../../images/tutorials/monitor-streaming/diagnostics.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!UICONTROL Fuentes] espacio de trabajo para controlar los flujos de datos de flujo continuo e identificar los errores que han producido cualquier flujo de datos fallido. Consulte los siguientes documentos para obtener más información:

* [Resumen de fuentes](../../home.md)
* [Información general de flujos de datos](../../../dataflows/home.md)
