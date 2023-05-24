---
title: Asignar un archivo CSV a un esquema XDM mediante Recommendations generado por IA
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante recomendaciones generadas por IA.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Asignar un archivo CSV a un esquema XDM mediante recomendaciones generadas por IA

>[!NOTE]
>
>Para obtener información sobre las funciones de asignación de CSV generalmente disponibles en Platform, consulte el documento sobre [asignación de un archivo CSV a un esquema existente](./existing-schema.md).

Para introducir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a una [!DNL Experience Data Model] Esquema (XDM). Puede elegir asignar a [un esquema existente](./existing-schema.md), pero si no sabe exactamente qué esquema utilizar o cómo debe estructurarse, puede utilizar recomendaciones dinámicas basadas en modelos de aprendizaje automático (ML) dentro de la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.
   * Como mínimo, debe comprender el concepto de [comportamientos en XDM](../../../xdm/home.md#data-behaviors), para que pueda decidir si desea asignar los datos a una [!UICONTROL Perfil] (comportamiento de registro) o [!UICONTROL ExperienceEvent] (comportamiento de la serie temporal).
* [Ingesta por lotes](../../batch-ingestion/overview.md): método mediante el cual [!DNL Platform] incorpora datos de archivos de datos proporcionados por el usuario.
* [Preparación de datos de Adobe Experience Platform](../../batch-ingestion/overview.md): conjunto de funciones que le permiten asignar y transformar datos ingeridos para que se ajusten a esquemas XDM. La documentación sobre [Funciones de preparación de datos](../../../data-prep/functions.md) es específicamente relevante para la asignación de esquemas.

## Proporcionar detalles del flujo de datos

En la IU del Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** vista, vaya a la **[!UICONTROL Sistema local]** categoría. En **[!UICONTROL Carga de archivo local]**, seleccione **[!UICONTROL Añadir datos]**.

![El [!UICONTROL Fuentes] en la interfaz de usuario de Platform, con [!UICONTROL Añadir datos] bajo [!UICONTROL Carga de archivo local] que se está seleccionando.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

El **[!UICONTROL Asignar esquema XDM de CSV]** flujo de trabajo aparece, empezando por **[!UICONTROL Detalles del flujo de datos]** paso.

Seleccionar **[!UICONTROL Crear un nuevo esquema con recomendaciones XML]**, lo que provoca la aparición de nuevos controles. Elija la clase adecuada para los datos CSV que desea asignar ([!UICONTROL Perfil] o [!UICONTROL ExperienceEvent]). Si lo desea, puede utilizar el menú desplegable para seleccionar el sector relevante para su negocio o dejarlo en blanco si no le corresponden las categorías proporcionadas. Si su organización funciona con un [de empresa a empresa (B2B)](../../../xdm/tutorials/relationship-b2b.md) modelo, seleccione el **[!UICONTROL Datos B2B]** casilla de verificación

![El [!UICONTROL Detalles del flujo de datos] paso con la opción de recomendación ML seleccionada. [!UICONTROL Perfil] está seleccionado para la clase y [!UICONTROL Telecomunicaciones] seleccionados para la industria](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Desde aquí, proporcione un nombre para el esquema que se creará a partir de los datos CSV y un nombre para el conjunto de datos de salida que contendrá los datos introducidos en ese esquema.

Opcionalmente, puede configurar las siguientes funciones adicionales para el flujo de datos antes de continuar:

| Nombre de entrada | Descripción |
| --- | --- |
| [!UICONTROL Descripción] | Descripción del flujo de datos. |
| [!UICONTROL Diagnósticos de error] | Cuando se habilita, se generan mensajes de error para los lotes recién ingeridos, que se pueden ver al recuperar el lote correspondiente en la [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Ingesta parcial] | Cuando se habilita, se incorporan registros válidos para nuevos datos por lotes dentro de un umbral de error especificado. Este umbral le permite configurar el porcentaje de errores aceptables antes de que falle todo el lote. |
| [!UICONTROL Detalles del flujo de datos] | Proporcione un nombre y una descripción opcional para el flujo de datos que llevará los datos CSV a Platform. Al iniciar este flujo de trabajo, se asigna automáticamente un nombre predeterminado al flujo de datos. Cambiar el nombre es opcional. |
| [!UICONTROL Alertas] | Seleccione de una lista de [alertas en el producto](../../../observability/alerts/overview.md) que desee recibir con respecto al estado del flujo de datos una vez que se haya iniciado. |

{style="table-layout:auto"}

Cuando haya terminado de configurar el flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![El [!UICONTROL Detalles del flujo de datos] se ha completado la sección.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Seleccionar datos

En el **[!UICONTROL Seleccionar datos]** , utilice la columna de la izquierda para cargar el archivo CSV. Puede seleccionar **[!UICONTROL Elegir archivos]** para abrir un cuadro de diálogo del explorador de archivos desde el que seleccionar el archivo, o bien puede arrastrar y soltar el archivo directamente en la columna.

![El [!UICONTROL Elegir archivos] y área de arrastrar y soltar resaltada dentro de la etiqueta [!UICONTROL Seleccionar datos] paso.](../../images/tutorials/map-csv-recommendations/upload-files.png)

Después de cargar el archivo, aparece una sección de datos de ejemplo que muestra las primeras diez filas de los datos recibidos para que pueda comprobar que se han cargado correctamente. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![Las filas de datos de ejemplo se rellenan en el espacio de trabajo](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurar asignaciones de esquema

Los modelos XML se ejecutan para generar un nuevo esquema basado en la configuración del flujo de datos y en el archivo CSV cargado. Una vez completado el proceso, la variable [!UICONTROL Asignación] Este paso se rellena para mostrar las asignaciones de cada campo individual junto con la vista totalmente navegable de la estructura de esquema generada.

![El [!UICONTROL Asignación] paso en la interfaz de usuario, que muestra todos los campos CSV asignados y la estructura de esquema resultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Desde aquí, puede hacer lo siguiente [editar las asignaciones de campos](#edit-mappings) o [modificar los grupos de campo a los que están asociados](#edit-schema) según sus necesidades. Cuando esté satisfecho, seleccione **[!UICONTROL Finalizar]** para completar la asignación e iniciar el flujo de datos configurado anteriormente. Los datos CSV se incorporan al sistema y rellenan un conjunto de datos basado en la estructura de esquema generada, listo para ser consumido por los servicios de Platform secundarios.

![El [!UICONTROL Finalizar] que se está seleccionando, completando el proceso de asignación de CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Editar asignaciones de campo {#edit-mappings}

Utilice la vista previa de asignación de campos para editar asignaciones existentes o eliminarlas por completo. Para obtener más información sobre cómo administrar un conjunto de asignaciones en la interfaz de usuario, consulte [Guía de interfaz de usuario para asignación de preparación de datos](../../../data-prep/ui/mapping.md#mapping-interface).

### Editar grupos de campos {#edit-field-groups}

Los campos CSV se asignan automáticamente a grupos de campos XDM existentes mediante modelos XML. Si desea cambiar el grupo de campos de cualquier campo CSV en particular, seleccione **[!UICONTROL Editar]** junto al árbol de esquemas.

![El [!UICONTROL Editar] botón que se está seleccionando junto al árbol de esquemas.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Aparece un cuadro de diálogo que le permite editar el nombre para mostrar, el tipo de datos y el grupo de campos de cualquier campo de la asignación. Seleccione el icono de edición (![Icono Editar](../../images/tutorials/map-csv-recommendations/edit-icon.png)) junto a un campo de origen para editar sus detalles en la columna derecha antes de seleccionar **[!UICONTROL Aplicar]**.

![El grupo de campos recomendado para un campo de origen que se está cambiando.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Cuando haya terminado de ajustar las recomendaciones del esquema para los campos de origen, seleccione **[!UICONTROL Guardar]** para aplicar los cambios.

## Pasos siguientes

En esta guía se explica cómo asignar un archivo CSV a un esquema XDM mediante recomendaciones generadas por IA, lo que le permite introducir esos datos en Platform mediante la ingesta por lotes.

Para ver los pasos de asignación de un archivo CSV a un esquema existente, consulte la [flujo de trabajo de asignación de esquema existente](./existing-schema.md). Para obtener información sobre la transmisión de datos a Platform en tiempo real mediante conexiones de origen prediseñadas, consulte la [información general de orígenes](../../../sources/home.md).
