---
title: Asignación de un archivo CSV a un esquema XDM mediante Recommendations generado por IA (Beta)
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante recomendaciones generadas por AI.
source-git-commit: d6f858af8bc44be74b1aaf12b973fb6818c1b2a5
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 1%

---

# Asignación de un archivo CSV a un esquema XDM mediante recomendaciones generadas por AI (Beta)

>[!IMPORTANT]
>
>Esta función está actualmente en fase beta y es posible que su organización no tenga acceso a ella aún. La documentación y la funcionalidad están sujetas a cambios.
>
>Para obtener información sobre las funciones de asignación de CSV disponibles de forma general en Platform, consulte el documento sobre [asignación de un archivo CSV a un esquema existente](./existing-schema.md).

Para introducir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a un [!DNL Experience Data Model] (XDM). Puede elegir asignar a [un esquema existente](./existing-schema.md), pero si no sabe exactamente qué esquema utilizar o cómo debe estructurarse, puede utilizar recomendaciones dinámicas basadas en modelos de aprendizaje automático (ML) en la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
   * Como mínimo, debe comprender el concepto de [comportamientos en XDM](../../../xdm/home.md#data-behaviors), para que pueda decidir si asigna los datos a un [!UICONTROL Perfil] Clase (comportamiento de registro) o [!UICONTROL ExperienceEvent] (comportamiento de serie temporal).
* [Ingesta por lotes](../../batch-ingestion/overview.md): El método mediante el cual [!DNL Platform] Ingesta datos de archivos de datos suministrados por el usuario.
* [Preparación de datos de Adobe Experience Platform](../../batch-ingestion/overview.md): Conjunto de funciones que le permiten asignar y transformar datos ingestados para ajustarse a esquemas XDM. La documentación de [Funciones de preparación de datos](../../../data-prep/functions.md) es especialmente relevante para la asignación de esquemas.

## Proporcionar detalles de flujo de datos

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , vaya a la **[!UICONTROL Sistema local]** categoría. En **[!UICONTROL Carga de archivo local]**, seleccione **[!UICONTROL Añadir datos]**.

![La variable [!UICONTROL Fuentes] en la interfaz de usuario de Platform, con [!UICONTROL Añadir datos] under [!UICONTROL Carga de archivo local] seleccionado](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

La variable **[!UICONTROL Asignar esquema XDM CSV]** aparece el flujo de trabajo, empezando por el **[!UICONTROL Detalles de flujo de datos]** paso a paso.

Select **[!UICONTROL Crear un nuevo esquema con recomendaciones ML]**, lo que hace que aparezcan nuevos controles. Elija la clase adecuada para los datos CSV que desea asignar ([!UICONTROL Perfil] o [!UICONTROL ExperienceEvent]). Si lo desea, puede utilizar el menú desplegable para seleccionar el sector correspondiente para su empresa o dejarlo en blanco si las categorías proporcionadas no se aplican a usted. Si su organización opera bajo un [de empresa a empresa (B2B)](../../../xdm/tutorials/relationship-b2b.md) modelo, seleccione el **[!UICONTROL Datos B2B]** casilla de verificación.

![La variable [!UICONTROL Detalles de flujo de datos] paso con la opción de recomendación ML seleccionada. [!UICONTROL Perfil] está seleccionado para la clase y [!UICONTROL Telecomunicaciones] seleccionados para el sector](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

A partir de aquí, proporcione un nombre para el esquema que se creará a partir de los datos CSV y un nombre para el conjunto de datos de salida que contendrá los datos ingestados en ese esquema.

Opcionalmente, puede configurar las siguientes funciones adicionales para el flujo de datos antes de continuar:

| Nombre de entrada | Descripción |
| --- | --- |
| [!UICONTROL Descripción] | Descripción del flujo de datos. |
| [!UICONTROL Diagnóstico de errores] | Cuando está habilitado, se generan mensajes de error para lotes recién ingestados, que se pueden ver al recuperar el lote correspondiente en la variable [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Ingesta parcial] | Cuando se habilita, los registros válidos para los nuevos datos de lote se incorporarán dentro de un umbral de error especificado. Este umbral le permite configurar el porcentaje de errores aceptables antes de que falle todo el lote. |
| [!UICONTROL Detalles del flujo de datos] | Proporcione un nombre y una descripción opcional para el flujo de datos que llevará los datos CSV a Platform. Al iniciar este flujo de trabajo, se asigna automáticamente un nombre predeterminado al flujo de datos. Cambiar el nombre es opcional. |
| [!UICONTROL Alertas] | Seleccione de una lista de [alertas en el producto](../../../observability/alerts/overview.md) que desea recibir con respecto al estado del flujo de datos una vez que se ha iniciado. |

{style=&quot;table-layout:auto&quot;}

Cuando haya terminado de configurar el flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![La variable [!UICONTROL Detalles de flujo de datos] sección completada](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selección de datos

En el **[!UICONTROL Seleccionar datos]** , utilice la columna izquierda para cargar el archivo CSV. Puede seleccionar **[!UICONTROL Elegir archivos]** para abrir un cuadro de diálogo del explorador de archivos para seleccionar el archivo o puede arrastrar y soltar el archivo directamente en la columna.

![La variable [!UICONTROL Elegir archivos] y área de arrastrar y soltar resaltada dentro del [!UICONTROL Seleccionar datos] step](../../images/tutorials/map-csv-recommendations/upload-files.png)

Después de cargar el archivo, aparece una sección de datos de ejemplo que muestra las diez primeras filas de los datos recibidos para que pueda verificar que se han cargado correctamente. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![Las filas de datos de ejemplo se rellenan en el espacio de trabajo](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configuración de asignaciones de esquema

Los modelos ML se ejecutan para generar un nuevo esquema basado en la configuración del flujo de datos y el archivo CSV cargado. Cuando se completa el proceso, la variable [!UICONTROL Asignación] el paso se rellena para mostrar las asignaciones para cada campo individual junto con la vista completamente navegable de la estructura de esquema generada.

![La variable [!UICONTROL Asignación] en la interfaz de usuario, que muestra todos los campos CSV asignados y la estructura de esquema resultante](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Desde aquí, puede [editar las asignaciones de campos](#edit-mappings) o [modificar los grupos de campos a los que están asociados](#edit-schema) según sus necesidades. Cuando esté satisfecho, seleccione **[!UICONTROL Finalizar]** para completar la asignación e iniciar el flujo de datos configurado anteriormente. Los datos CSV se incorporan al sistema y rellenan un conjunto de datos basado en la estructura de esquema generada, listo para ser consumido por los servicios de Platform descendentes.

![La variable [!UICONTROL Finalizar] botón seleccionado, completando el proceso de asignación de CSV](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Editar asignaciones de campos {#edit-mappings}

Utilice la vista previa de asignación de campos para editar las asignaciones existentes o eliminarlas por completo. Para obtener más información sobre cómo administrar un conjunto de asignaciones en la interfaz de usuario, consulte la [Guía de la interfaz de usuario para la asignación de preparación de datos](../../../data-prep/ui/mapping.md#mapping-interface).

### Editar grupos de campos {#edit-field-groups}

Los campos CSV se asignan automáticamente a grupos de campos XDM existentes mediante modelos ML. Si desea cambiar el grupo de campos de cualquier campo CSV en particular, seleccione **[!UICONTROL Editar]** junto al árbol de esquemas.

![La variable [!UICONTROL Editar] botón seleccionado junto al árbol de esquemas](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Aparece un cuadro de diálogo que le permite editar el nombre para mostrar, el tipo de datos y el grupo de campos de cualquier campo de la asignación. Seleccione el icono de edición (![Icono Editar](../../images/tutorials/map-csv-recommendations/edit-icon.png)) junto a un campo de origen para editar sus detalles en la columna derecha antes de seleccionar **[!UICONTROL Aplicar]**.

![Grupo de campos recomendado para un campo de origen que se está cambiando](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Cuando haya terminado de ajustar las recomendaciones de esquema para los campos de origen, seleccione **[!UICONTROL Guardar]** para aplicar los cambios.

## Pasos siguientes

En esta guía se explica cómo asignar un archivo CSV a un esquema XDM mediante recomendaciones generadas por AI, lo que permite introducir esos datos en Platform mediante la ingesta por lotes.

Para ver los pasos sobre la asignación de un archivo CSV a un esquema existente, consulte [flujo de trabajo de asignación de esquema existente](./existing-schema.md). Para obtener información sobre la transmisión de datos a Platform en tiempo real a través de conexiones de origen precompiladas, consulte la [información general sobre fuentes](../../../sources/home.md).
