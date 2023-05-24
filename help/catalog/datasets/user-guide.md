---
keywords: Experience Platform;inicio;temas populares;habilitar conjunto de datos;Conjunto de datos;conjunto de datos
solution: Experience Platform
title: Guía de IU de conjuntos de datos
description: Obtenga información sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: f0cd059683531993398f0a81d6eda486276853e2
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 7%

---

# Guía de IU de conjuntos de datos

Esta guía del usuario proporciona instrucciones sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Conjuntos de datos](overview.md): la construcción de almacenamiento y administración para la persistencia de datos en [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Aprenda a crear sus propios esquemas XDM personalizados con el [!DNL Schema Editor] dentro de [!DNL Platform] interfaz de usuario.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garantice el cumplimiento de las regulaciones, restricciones y políticas relativas al uso de los datos del cliente.

## Ver conjuntos de datos {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos en la actividad del conjunto de datos"
>abstract="Los números negativos de los registros ingeridos implican que un usuario ha eliminado determinados lotes en un intervalo de tiempo seleccionado."
>text="Learn more in documentation"

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para abrir **[!UICONTROL Conjuntos de datos]** panel. El panel enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

![Imagen que resalta el elemento Conjuntos de datos en la barra de navegación izquierda.](../images/datasets/user-guide/browse-datasets.png)

De forma predeterminada, solo se muestran los conjuntos de datos que ha introducido. Si desea ver los conjuntos de datos generados por el sistema, habilite la variable **[!UICONTROL Mostrar conjuntos de datos del sistema]** alternar. Los conjuntos de datos generados por el sistema solo se utilizan para procesar otros componentes. Por ejemplo, el conjunto de datos de exportación de perfiles generado por el sistema se utiliza para procesar el panel de perfiles.

![Se resalta el conmutador que le permite elegir si se deben mostrar o no conjuntos de datos del sistema.](../images/datasets/user-guide/system-datasets.png)

Seleccione el nombre de un conjunto de datos para acceder a su **[!UICONTROL Actividad de conjunto de datos]** y ver los detalles del conjunto de datos seleccionado. La pestaña actividad incluye un gráfico que visualiza la tasa de consumo de los mensajes, así como una lista de lotes correctos y fallidos.

![Se resaltan los detalles del conjunto de datos seleccionado.](../images/datasets/user-guide/dataset-activity-1.png)
![Se resaltan los lotes de muestra que pertenecen al conjunto de datos seleccionado.](../images/datasets/user-guide/dataset-activity-2.png)

## Previsualización de un conjunto de datos

Desde el **[!UICONTROL Actividad de conjunto de datos]** pantalla, seleccione **[!UICONTROL Previsualizar conjunto de datos]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos. Si el conjunto de datos está vacío, el vínculo de vista previa se desactivará y, en su lugar, indicará que la vista previa no está disponible.

![Se resaltará el botón Vista previa del conjunto de datos.](../images/datasets/user-guide/select-preview.png)

En la ventana de vista previa, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

![Se muestra una vista previa del conjunto de datos. Se muestra información sobre la estructura y los valores de muestra.](../images/datasets/user-guide/preview-dataset.png)

Para obtener métodos más sólidos para acceder a los datos, [!DNL Experience Platform] proporciona servicios descendentes como [!DNL Query Service] y [!DNL JupyterLab] para explorar y analizar datos. Consulte los siguientes documentos para obtener más información:

* [Introducción al servicio de consultas](../../query-service/home.md)
* [Guía del usuario de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Crear un conjunto de datos {#create}

Para crear un nuevo conjunto de datos, empiece seleccionando **[!UICONTROL Crear conjunto de datos]** en el tablero Conjuntos de datos.****

![El botón Crear conjunto de datos está resaltado.](../images/datasets/user-guide/select-create.png)

En la siguiente pantalla, se le presentan las dos opciones siguientes para crear un nuevo conjunto de datos:

* [Crear conjunto de datos a partir de esquema](#schema)
* [Crear conjunto de datos a partir de archivo CSV](#csv)

### Crear un conjunto de datos con un esquema existente {#schema}

En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccione **[!UICONTROL Crear conjunto de datos a partir de esquema]** para crear un nuevo conjunto de datos vacío.

![El botón Crear conjunto de datos a partir de esquema está resaltado.](../images/datasets/user-guide/create-dataset-schema.png)

El **[!UICONTROL Seleccionar esquema]** aparece el paso. Examine la lista de esquemas y seleccione el esquema al que se adherirá el conjunto de datos antes de seleccionar **[!UICONTROL Siguiente]**.

![Se muestra una lista de esquemas. Se resalta el esquema que se utilizará para crear el conjunto de datos.](../images/datasets/user-guide/select-schema.png)

El **[!UICONTROL Configurar conjunto de datos]** aparece el paso. Proporcione al conjunto de datos un nombre y una descripción opcional y, a continuación, seleccione **[!UICONTROL Finalizar]** para crear el conjunto de datos.

![Se insertan los detalles de configuración del conjunto de datos. Esto incluye detalles como el nombre y la descripción del conjunto de datos.](../images/datasets/user-guide/configure-dataset-schema.png)

### Creación de un conjunto de datos con un archivo CSV {#csv}

Cuando se crea un conjunto de datos con un archivo CSV, se crea un esquema ad hoc para proporcionar al conjunto de datos una estructura que coincida con el archivo CSV proporcionado. En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccione **[!UICONTROL Crear conjunto de datos a partir de archivo CSV]**.

![El botón Crear conjunto de datos a partir de archivo CSV está resaltado.](../images/datasets/user-guide/create-dataset-csv.png)

El **[!UICONTROL Configurar]** aparece el paso. Proporcione al conjunto de datos un nombre y una descripción opcional y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Se insertan los detalles de configuración del conjunto de datos. Esto incluye detalles como el nombre y la descripción del conjunto de datos.](../images/datasets/user-guide/configure-dataset-csv.png)

El **[!UICONTROL Añadir datos]** aparece el paso. Cargue el archivo CSV arrastrándolo y soltándolo en el centro de la pantalla, o seleccione **[!UICONTROL Examinar]** para explorar el directorio de archivos. El archivo puede tener un tamaño de hasta diez gigabytes. Una vez cargado el archivo CSV, seleccione **[!UICONTROL Guardar]** para crear el conjunto de datos.

>[!NOTE]
>
>Los nombres de las columnas CSV deben comenzar con caracteres alfanuméricos y solo pueden contener letras, números y guiones bajos.

![Se muestra la pantalla Añadir datos. Se resaltará la ubicación donde puede cargar el archivo CSV para el conjunto de datos.](../images/datasets/user-guide/add-csv-data.png)

## Habilitar un conjunto de datos para el perfil del cliente en tiempo real {#enable-profile}

Cada conjunto de datos tiene la capacidad de enriquecer los perfiles de los clientes con los datos introducidos. Para ello, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en [!DNL Real-Time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

* El esquema tiene al menos un atributo especificado como propiedad de identidad.
* El esquema tiene una propiedad de identidad definida como la identidad principal.

Para obtener más información sobre la activación de un esquema para [!DNL Profile], consulte la [Guía del usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

Para habilitar un conjunto de datos para el perfil, acceda a su **[!UICONTROL Actividad de conjunto de datos]** y seleccione la **[!UICONTROL Perfil]** alternar dentro de **[!UICONTROL Propiedades]** columna. Una vez habilitados, los datos que se incorporen al conjunto de datos también se utilizarán para rellenar perfiles de clientes.

>[!NOTE]
>
>Si un conjunto de datos ya contiene datos y, a continuación, está habilitado para [!DNL Profile], los datos existentes no se consumen automáticamente por [!DNL Profile]. Después de habilitar un conjunto de datos para [!DNL Profile]Sin embargo, se recomienda volver a introducir los datos existentes para que contribuyan a los perfiles de los clientes.

![La opción Perfil se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/enable-dataset-profiles.png)

## Administración y aplicación del control de datos en un conjunto de datos {#manage-and-enforce-data-governance}

Las etiquetas de uso de datos, aplicadas en el nivel de esquema, le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información sobre las etiquetas, o consulte la [guía del usuario sobre etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener instrucciones sobre cómo aplicar etiquetas a esquemas para su propagación a conjuntos de datos.

## Eliminar un conjunto de datos {#delete}

Puede eliminar un conjunto de datos accediendo primero a su **[!UICONTROL Actividad de conjunto de datos]** pantalla. A continuación, seleccione **[!UICONTROL Eliminar conjunto de datos]** para eliminarlo.

>[!NOTE]
>
>Conjuntos de datos creados y utilizados por aplicaciones y servicios de Adobe (como Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) no se puede eliminar.

![El botón Eliminar conjunto de datos se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/delete-dataset.png)

Aparecerá un cuadro de confirmación. Seleccionar **[!UICONTROL Eliminar]** para confirmar la eliminación del conjunto de datos.

![Se muestra el modal de confirmación para la eliminación, con el botón Eliminar resaltado.](../images/datasets/user-guide/confirm-delete.png)

## Eliminar un conjunto de datos con perfil habilitado

Si un conjunto de datos está habilitado para Perfil, al eliminar ese conjunto de datos a través de la interfaz de usuario, se eliminará del lago de datos, el servicio de identidad y el almacén de perfiles en Platform.

Puede eliminar un conjunto de datos del [!DNL Profile] Almacenar solo (dejando los datos en el lago de datos) mediante la API de Perfil del cliente en tiempo real. Para obtener más información, consulte la [guía de extremo de API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md).

## Monitorización de la ingesta de datos

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. El **[!UICONTROL Monitorización]** El panel de control de Campaign le permite ver los estados de los datos de entrada procedentes de la ingesta por lotes o de la transmisión. Para ver los estados de los lotes individuales, seleccione **[!UICONTROL Lote de extremo a extremo]** o **[!UICONTROL Transmisión de extremo a extremo]**. Los paneles enumeran todas las ejecuciones de ingesta por lotes o de flujo continuo, incluidas las que se realizan correctamente, las que fallaron o las que aún están en curso. Cada lista proporciona detalles del lote, incluido el ID de lote, el nombre del conjunto de datos de destinatario y el número de registros introducidos. Si el conjunto de datos de destinatario está habilitado para [!DNL Profile], también se muestra el número de registros de identidad y perfil ingeridos.

![Se muestra la pantalla de monitorización de un lote completo. Se resaltan tanto la monitorización como el lote a lote.](../images/datasets/user-guide/batch-listing.png)

Puede seleccionar un individuo **[!UICONTROL ID de lote]** para acceder a **[!UICONTROL Introducción a lotes]** y ver los detalles del lote, incluidos los registros de errores en caso de que el lote no se pueda ingerir.

![Se muestran los detalles del lote seleccionado. Esto incluye el número de registros introducidos, el número de registros fallidos, el estado del lote, el tamaño del archivo, las horas de inicio y finalización de la ingesta, los ID de conjunto de datos y lote, el ID de organización, el nombre del conjunto de datos y la información de acceso.](../images/datasets/user-guide/batch-overview.png)

Si desea eliminar el lote, puede hacerlo seleccionando **[!UICONTROL Eliminar lote]** se encuentra cerca de la parte superior derecha del panel. Al hacerlo, también se eliminarán sus registros del conjunto de datos en el que se ingirió originalmente el lote.

![El botón Eliminar lote se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/delete-batch.png)

## Pasos siguientes

Esta guía del usuario proporciona instrucciones para realizar acciones comunes al trabajar con conjuntos de datos en [!DNL Experience Platform] interfaz de usuario. Para ver los pasos de realización de [!DNL Platform] flujos de trabajo que implican conjuntos de datos, consulte los siguientes tutoriales:

* [Creación de un conjunto de datos mediante API](create.md)
* [Consulta de datos de conjuntos de datos mediante la API de acceso a datos](../../data-access/home.md)
* [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../../profile/tutorials/dataset-configuration.md)
