---
keywords: Experience Platform;inicio;temas populares;conector de comercio electrónico;eCommerce
solution: Experience Platform
title: Crear un flujo de datos con un origen de comercio electrónico en la interfaz de usuario
type: Tutorial
description: Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Platform. Este tutorial proporciona pasos sobre cómo crear un flujo de datos para una fuente de comercio electrónico mediante la interfaz de usuario de Platform.
exl-id: ee1382c5-78ac-4765-8883-0a922772bb20
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# Crear un flujo de datos mediante una fuente de comercio electrónico en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos en Adobe Experience Platform. Este tutorial proporciona pasos sobre cómo crear un flujo de datos para un origen de comercio electrónico mediante la interfaz de usuario de Platform.

>[!NOTE]
>
>Para crear un flujo de datos, ya debe tener una cuenta autenticada con un origen de comercio electrónico. Puede encontrar una lista de tutoriales para crear distintas cuentas de origen de comercio electrónico en la interfaz de usuario en la [información general sobre fuentes](../../../home.md#ecommerce).

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

## Adición de datos

Después de crear su cuenta de origen de comercio electrónico, la variable **[!UICONTROL Añadir datos]** aparece, proporcionando una interfaz para explorar la jerarquía de tablas de la cuenta de origen de comercio electrónico.

* La mitad izquierda de la interfaz es un explorador que muestra una lista de tablas de datos incluidas en la cuenta. La interfaz también incluye una opción de búsqueda que permite identificar rápidamente los datos de origen que desea utilizar.
* La mitad derecha de la interfaz es un panel de vista previa, que le permite obtener una vista previa de hasta 100 filas de datos.

>[!NOTE]
>
>La opción de fuente de datos de búsqueda está disponible para todas las fuentes basadas en tablas, excluyendo Adobe Analytics. [!DNL Amazon Kinesis]y [!DNL Azure Event Hubs].

Una vez que encuentre los datos de origen, seleccione la tabla y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Proporcionar detalles de flujo de datos

La variable [!UICONTROL Detalles de flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o un nuevo conjunto de datos. Durante este proceso, también puede configurar las opciones de [!UICONTROL Conjunto de datos del perfil], [!UICONTROL Diagnóstico de errores], [!UICONTROL Ingesta parcial]y [!UICONTROL Alertas].

![dataflow-detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Usar un conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable. Una vez que haya seleccionado un conjunto de datos, proporcione un nombre y una descripción para el flujo de datos.

![conjunto de datos existente](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Usar un nuevo conjunto de datos

Para introducir en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre de conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema para asignarlo mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez que haya seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

![conjunto de datos nuevo](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Habilitar [!DNL Profile] y diagnóstico de errores

A continuación, seleccione la **[!UICONTROL Conjunto de datos del perfil]** alternar para habilitar su conjunto de datos para [!DNL Profile]. Esto le permite crear una vista holística de los atributos y comportamientos de una entidad. Datos de todos [!DNL Profile]Los conjuntos de datos habilitados para se incluirán en [!DNL Profile] Los cambios y se aplican cuando guarda el flujo de datos.

[!UICONTROL Diagnóstico de errores] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] le permite introducir datos que contengan errores, hasta un umbral determinado que defina manualmente. Consulte la [información general sobre la ingesta parcial de lotes](../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

![profile-and-errors](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Habilitar alertas

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la interfaz de usuario](../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![alertas](../../../images/tutorials/dataflow/table-based/alerts.png)

## Asignación de campos de datos a un esquema XDM

La variable [!UICONTROL Asignación] aparece, proporcionando una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](../../../../data-prep/ui/mapping.md).

Una vez asignados correctamente los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![asignación](../../../images/tutorials/dataflow/table-based/mapping.png)

## Programar ejecuciones de ingesta

La variable [!UICONTROL Programación] , lo que le permite configurar una programación de ingesta para que ingrese automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. De forma predeterminada, la programación está configurada en `Once`. Para ajustar la frecuencia de ingesta, seleccione **[!UICONTROL Frecuencia]** y, a continuación, seleccione una opción en el menú desplegable.

>[!TIP]
>
>El intervalo y el relleno no son visibles durante una ingesta única.

![programación](../../../images/tutorials/dataflow/table-based/scheduling.png)

Si establece la frecuencia de ingesta en `Minute`, `Hour`, `Day`o `Week`, debe configurar un intervalo para establecer un intervalo de tiempo definido entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para la ingesta de datos cada 15 días.

Durante este paso, también puede activar **relleno** y defina una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar nuevos datos de los datos existentes.

Consulte la siguiente tabla para obtener más información sobre las configuraciones de programación.

| Campo | Descripción |
| --- | --- |
| Frecuencia | Frecuencia con la que se produce una ingesta. Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`y `Week`. |
| Intervalo | Un entero que define el intervalo para la frecuencia seleccionada. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15. |
| Hora de inicio | Marca de tiempo UTC que indica cuándo se configura la primera ingesta. La hora de inicio debe ser buena o igual a la hora UTC actual. |
| Relleno | Un valor booleano que determina qué datos se introducen inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se incorporarán durante la primera ingesta programada. Si el relleno está desactivado, solo se incorporarán los archivos que se cargan entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |
| Cargar datos incrementales por | Una opción con un conjunto filtrado de campos de esquema de origen de tipo, fecha u hora. Este campo se utiliza para diferenciar entre datos nuevos y existentes. Los datos incrementales se incorporarán en función de la marca de tiempo de la columna seleccionada. |

![relleno](../../../images/tutorials/dataflow/table-based/backfill.png)

## Revise el flujo de datos

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el período, la frecuencia y el intervalo activos del programa de ingesta.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![review](../../../images/tutorials/dataflow/table-based/review.png)

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se incorporan a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar el flujo de datos, consulte el tutorial en [supervisión de cuentas y flujos de datos en la interfaz de usuario](../monitor.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente empleando la función **[!UICONTROL Eliminar]** en la función **[!UICONTROL Flujos de datos]** espacio de trabajo. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminación de flujos de datos en la interfaz de usuario](../delete.md).

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para traer los datos de su fuente de comercio electrónico a Platform. Los datos entrantes ahora se pueden usar en el flujo descendente [!DNL Platform] servicios como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](../../../../profile/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> La interfaz de usuario de Platform que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)

