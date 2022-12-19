---
keywords: Experience Platform;inicio;temas populares;habilitar conjunto de datos;conjunto de datos;conjunto de datos
solution: Experience Platform
title: Guía de la interfaz de usuario de conjuntos de datos
topic-legacy: datasets
description: Aprenda a realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 28b6944a14c07f14d8177e3f8ae1c1a83c4c9c86
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Guía de la interfaz de usuario de conjuntos de datos

Esta guía del usuario proporciona instrucciones sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Conjuntos de datos](overview.md): La construcción de almacenamiento y administración para la persistencia de datos en [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear sus propios esquemas XDM personalizados mediante el [!DNL Schema Editor] dentro de la variable [!DNL Platform] interfaz de usuario.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Garantizar el cumplimiento de las regulaciones, restricciones y políticas relativas al uso de los datos de los clientes.

## Ver conjuntos de datos {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos en la actividad del conjunto de datos"
>abstract="Los números negativos de los registros ingestados significan que un usuario ha eliminado determinados lotes en un intervalo de tiempo seleccionado."
>text="Learn more in documentation"

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para abrir el **[!UICONTROL Conjuntos de datos]** tablero. El tablero enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

![](../images/datasets/user-guide/browse-datasets.png)

De forma predeterminada, solo se muestran los conjuntos de datos que ha introducido en . Si desea ver los conjuntos de datos generados por el sistema, habilite la variable **[!UICONTROL Mostrar conjuntos de datos del sistema]** alternar. Los conjuntos de datos generados por el sistema solo se utilizan para procesar otros componentes. Por ejemplo, el conjunto de datos de exportación de perfiles generado por el sistema se utiliza para procesar el panel de perfiles.

![](../images/datasets/user-guide/system-datasets.png)

Seleccione el nombre de un conjunto de datos para acceder a su **[!UICONTROL Actividad del conjunto de datos]** y ver los detalles del conjunto de datos seleccionado. La pestaña actividad incluye un gráfico que visualiza la tasa de consumo de los mensajes, así como una lista de lotes correctos y fallidos.

![](../images/datasets/user-guide/dataset-activity-1.png)
![](../images/datasets/user-guide/dataset-activity-2.png)

## Vista previa de un conjunto de datos

En el **[!UICONTROL Actividad del conjunto de datos]** pantalla, seleccionar **[!UICONTROL Vista previa del conjunto de datos]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos. Si el conjunto de datos está vacío, el vínculo de vista previa se desactivará y en su lugar indicará que la vista previa no está disponible.

![](../images/datasets/user-guide/select-preview.png)

En la ventana de vista previa, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

![](../images/datasets/user-guide/preview-dataset.png)

Para métodos más sólidos para acceder a sus datos, [!DNL Experience Platform] proporciona servicios descendentes como [!DNL Query Service] y [!DNL JupyterLab] para explorar y analizar datos. Consulte los siguientes documentos para obtener más información:

* [Información general del servicio de consultas](../../query-service/home.md)
* [Guía del usuario de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Crear un conjunto de datos {#create}

Para crear un nuevo conjunto de datos, comience seleccionando **[!UICONTROL Crear conjunto de datos]** en el **[!UICONTROL Conjuntos de datos]** tablero.

![](../images/datasets/user-guide/select-create.png)

En la siguiente pantalla, se le presentan las dos opciones siguientes para crear un nuevo conjunto de datos:

* [Crear conjunto de datos a partir del esquema](#schema)
* [Crear conjunto de datos a partir de un archivo CSV](#csv)

### Creación de un conjunto de datos con un esquema existente {#schema}

En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccionar **[!UICONTROL Crear conjunto de datos a partir del esquema]** para crear un nuevo conjunto de datos vacío.

![](../images/datasets/user-guide/create-dataset-schema.png)

La variable **[!UICONTROL Seleccionar esquema]** aparece. Examine la lista de esquemas y seleccione el esquema al que se adherirá el conjunto de datos antes de seleccionar **[!UICONTROL Siguiente]**.

![](../images/datasets/user-guide/select-schema.png)

La variable **[!UICONTROL Configurar el conjunto de datos]** aparece. Proporcione un nombre al conjunto de datos y una descripción opcional y, a continuación, seleccione **[!UICONTROL Finalizar]** para crear el conjunto de datos.

![](../images/datasets/user-guide/configure-dataset-schema.png)

### Creación de un conjunto de datos con un archivo CSV {#csv}

Cuando se crea un conjunto de datos con un archivo CSV, se crea un esquema ad hoc para proporcionar al conjunto de datos una estructura que coincida con el archivo CSV proporcionado. En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccionar **[!UICONTROL Crear conjunto de datos a partir de un archivo CSV]**.

![](../images/datasets/user-guide/create-dataset-csv.png)

La variable **[!UICONTROL Configurar]** aparece. Proporcione un nombre al conjunto de datos y una descripción opcional y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![](../images/datasets/user-guide/configure-dataset-csv.png)

La variable **[!UICONTROL Añadir datos]** aparece. Cargue el archivo CSV arrastrándolo y soltándolo en el centro de la pantalla o seleccione **[!UICONTROL Examinar]** para explorar el directorio de archivos. El archivo puede tener un tamaño de hasta diez gigabytes. Una vez cargado el archivo CSV, seleccione **[!UICONTROL Guardar]** para crear el conjunto de datos.

>[!NOTE]
>
>Los nombres de columna de CSV deben comenzar con caracteres alfanuméricos y solo pueden contener letras, números y guiones bajos.

![](../images/datasets/user-guide/add-csv-data.png)

## Habilitar un conjunto de datos para el perfil del cliente en tiempo real {#enable-profile}

Cada conjunto de datos tiene la capacidad de enriquecer perfiles de clientes con sus datos introducidos. Para ello, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en [!DNL Real-time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

* El esquema tiene al menos un atributo especificado como propiedad de identidad.
* El esquema tiene una propiedad de identidad definida como la identidad principal.

Para obtener más información sobre cómo habilitar un esquema para [!DNL Profile], consulte la [Guía del usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

Para habilitar un conjunto de datos para Perfil, acceda a su **[!UICONTROL Actividad del conjunto de datos]** y seleccione **[!UICONTROL Perfil]** alternar dentro de **[!UICONTROL Propiedades]** para abrir el Navegador. Una vez habilitados, los datos que se incorporan en el conjunto de datos también se utilizarán para rellenar perfiles de clientes.

>[!NOTE]
>
>Si un conjunto de datos ya contiene datos y está habilitado para [!DNL Profile], los datos existentes no se consumen automáticamente en [!DNL Profile]. Después de habilitar un conjunto de datos para [!DNL Profile], se recomienda volver a introducir los datos existentes para que contribuyan a los perfiles de los clientes.

![](../images/datasets/user-guide/enable-dataset-profiles.png)

## Administrar y hacer cumplir la administración de datos en un conjunto de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Consulte la [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información sobre las etiquetas, o consulte la [guía del usuario de etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener instrucciones sobre cómo aplicar etiquetas a conjuntos de datos.

## Eliminación de un conjunto de datos

Puede eliminar un conjunto de datos accediendo primero a su **[!UICONTROL Actividad del conjunto de datos]** en el Navegador. A continuación, seleccione **[!UICONTROL Eliminar conjunto de datos]** para eliminarlo.

>[!NOTE]
>
>Conjuntos de datos creados y utilizados por aplicaciones y servicios de Adobe (como Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) no se puede eliminar.

![](../images/datasets/user-guide/delete-dataset.png)

Aparece un cuadro de confirmación. Select **[!UICONTROL Eliminar]** para confirmar la eliminación del conjunto de datos.

![](../images/datasets/user-guide/confirm-delete.png)

## Eliminar un conjunto de datos habilitado para perfil

Si un conjunto de datos está habilitado para Perfil, al eliminar ese conjunto de datos a través de la interfaz de usuario, se eliminará del lago de datos, del servicio de identidad y del almacén de perfiles en Platform.

Puede eliminar un conjunto de datos del [!DNL Profile] solo almacene (dejando los datos en el lago de datos) mediante la API de perfil del cliente en tiempo real. Para obtener más información, consulte la [guía de extremo de la API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md).

## Monitorización de la ingesta de datos

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. La variable **[!UICONTROL Monitorización]** tablero permite ver los estados de los datos entrantes desde la ingesta por lotes o de flujo continuo. Para ver los estados de los lotes individuales, seleccione: **[!UICONTROL Lote de extremo a extremo]** o **[!UICONTROL Transmisión de extremo a extremo]**. Los tableros enumeran todas las ejecuciones de ingesta por lotes o de flujo continuo, incluidas las que se hayan realizado correctamente, que hayan fallado o que estén aún en curso. Cada lista proporciona detalles del lote, incluido el ID del lote, el nombre del conjunto de datos de destino y el número de registros introducidos. Si el conjunto de datos de destino está habilitado para [!DNL Profile], también se muestra el número de registros de identidad y perfil ingestados.

![](../images/datasets/user-guide/batch-listing.png)

Puede seleccionar una **[!UICONTROL ID de lote]** para acceder a la **[!UICONTROL Información general de lotes]** tablero y ver los detalles del lote, incluidos los registros de errores si el lote no se puede ingerir.

![](../images/datasets/user-guide/batch-overview.png)

Si desea eliminar el lote, puede hacerlo seleccionando **[!UICONTROL Eliminar lote]** se encuentra cerca de la parte superior derecha del panel. Al hacerlo, también se eliminarán sus registros del conjunto de datos al que se incorporó originalmente el lote.

![](../images/datasets/user-guide/delete-batch.png)

## Pasos siguientes

Esta guía del usuario proporciona instrucciones para realizar acciones comunes al trabajar con conjuntos de datos en la variable [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre cómo realizar [!DNL Platform] flujos de trabajo que implican conjuntos de datos, consulte los siguientes tutoriales:

* [Creación de un conjunto de datos mediante API](create.md)
* [Consultar datos de conjuntos de datos mediante la API de acceso a datos](../../data-access/home.md)
* [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../../profile/tutorials/dataset-configuration.md)
