---
keywords: Experience Platform;inicio;temas populares;habilitar conjunto de datos;conjunto de datos;conjunto de datos
solution: Experience Platform
title: Guía de la interfaz de usuario de conjuntos de datos
topic-legacy: datasets
description: Aprenda a realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Guía de la interfaz de usuario de conjuntos de datos

Esta guía del usuario proporciona instrucciones sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Conjuntos de datos](overview.md): La construcción de almacenamiento y administración para la persistencia de datos en  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Editor](../../xdm/tutorials/create-schema-ui.md) de esquemas: Obtenga información sobre cómo crear sus propios esquemas XDM personalizados mediante  [!DNL Schema Editor] la interfaz de  [!DNL Platform] usuario de .
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Garantizar el cumplimiento de las regulaciones, restricciones y políticas relativas al uso de los datos de los clientes.

## Ver conjuntos de datos

En la interfaz de usuario [!DNL Experience Platform], haga clic en **[!UICONTROL Datasets]** en el panel de navegación izquierdo para abrir el panel **[!UICONTROL Datasets]**. El tablero enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

![](../images/datasets/user-guide/browse_datasets.png)

Haga clic en el nombre de un conjunto de datos para acceder a su pantalla **[!UICONTROL Dataset activity]** y ver los detalles del conjunto de datos seleccionado. La pestaña actividad incluye un gráfico que visualiza la tasa de consumo de los mensajes, así como una lista de lotes correctos y fallidos.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Vista previa de un conjunto de datos

En la pantalla **[!UICONTROL Dataset activity]**, haga clic en **[!UICONTROL Preview dataset]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos. Si el conjunto de datos está vacío, el vínculo de vista previa se desactiva y en su lugar indica que la vista previa no está disponible.

![](../images/datasets/user-guide/click_to_preview.png)

En la ventana de vista previa, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

![](../images/datasets/user-guide/preview_dataset.png)

Para métodos más sólidos para acceder a sus datos, [!DNL Experience Platform] proporciona servicios descendentes como [!DNL Query Service] y [!DNL JupyterLab] para explorar y analizar los datos. Consulte los siguientes documentos para obtener más información:

* [Información general del servicio de consultas](../../query-service/home.md)
* [Guía del usuario de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Crear un conjunto de datos {#create}

Para crear un nuevo conjunto de datos, comience haciendo clic en **[!UICONTROL Create dataset]** en el panel **[!UICONTROL Datasets]** .

![](../images/datasets/user-guide/click_to_create.png)

En la siguiente pantalla, se le presentan las dos opciones siguientes para crear un nuevo conjunto de datos:

* [Crear conjunto de datos a partir del esquema](#schema)
* [Crear conjunto de datos a partir de un archivo CSV](#csv)

### Crear un conjunto de datos con un esquema existente {#schema}

En la pantalla **[!UICONTROL Create dataset]** , haga clic en **[!UICONTROL Create dataset from schema]** para crear un nuevo conjunto de datos vacío.

![](../images/datasets/user-guide/create_dataset_schema.png)

Aparece el paso **[!UICONTROL Select schema]**. Examine la lista de esquemas y seleccione el esquema al que se adherirá el conjunto de datos antes de hacer clic en **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

Aparece el paso **[!UICONTROL Configure dataset]**. Proporcione un nombre al conjunto de datos y una descripción opcional y, a continuación, haga clic en **[!UICONTROL Finish]** para crear el conjunto de datos.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Crear un conjunto de datos con un archivo CSV {#csv}

Cuando se crea un conjunto de datos con un archivo CSV, se crea un esquema ad hoc para proporcionar al conjunto de datos una estructura que coincida con el archivo CSV proporcionado. En la pantalla **[!UICONTROL Create dataset]**, haga clic en el cuadro que dice **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Aparece el paso **[!UICONTROL Configure]**. Proporcione un nombre y una descripción opcionales al conjunto de datos y haga clic en **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Aparece el paso **[!UICONTROL Add data]**. Cargue el archivo CSV arrastrándolo y soltándolo en el centro de la pantalla o haga clic en **[!UICONTROL Browse]** para explorar el directorio de archivos. El archivo puede tener un tamaño de hasta diez gigabytes. Una vez cargado el archivo CSV, haga clic en **[!UICONTROL Save]** para crear el conjunto de datos.

>[!NOTE]
>
>Los nombres de columna de CSV deben comenzar con caracteres alfanuméricos y solo pueden contener letras, números y guiones bajos.

![](../images/datasets/user-guide/add_csv_data.png)

## Habilitar un conjunto de datos para Perfil del cliente en tiempo real {#enable-profile}

Cada conjunto de datos tiene la capacidad de enriquecer perfiles de clientes con sus datos introducidos. Para ello, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en [!DNL Real-time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

* El esquema tiene al menos un atributo especificado como propiedad de identidad.
* El esquema tiene una propiedad de identidad definida como la identidad principal.

Para obtener más información sobre cómo habilitar un esquema para [!DNL Profile], consulte la [guía del usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

Para habilitar un conjunto de datos para Perfil, acceda a su pantalla **[!UICONTROL Dataset activity]** y haga clic en el botón **[!UICONTROL Profile]** dentro de la columna **[!UICONTROL Properties]** . Una vez habilitados, los datos que se incorporan en el conjunto de datos también se utilizarán para rellenar perfiles de clientes.

>[!NOTE]
>
>Si un conjunto de datos ya contiene datos y luego se habilita para [!DNL Profile], [!DNL Profile] no consume automáticamente los datos existentes. Una vez habilitado un conjunto de datos para [!DNL Profile], se recomienda volver a introducir los datos existentes para que contribuyan a los perfiles del cliente.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Administrar y hacer cumplir la administración de datos en un conjunto de datos

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Consulte la [información general sobre el control de datos](../../data-governance/home.md) para obtener más información sobre las etiquetas, o consulte la [guía del usuario sobre etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener instrucciones sobre cómo aplicar etiquetas a conjuntos de datos.

## Eliminación de un conjunto de datos

Puede eliminar un conjunto de datos accediendo primero a su pantalla **[!UICONTROL Dataset activity]**. A continuación, haga clic en **[!UICONTROL Delete dataset]** para eliminarlo.

>[!NOTE]
>
>Los conjuntos de datos creados y utilizados por aplicaciones y servicios de Adobe (como Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) no se pueden eliminar.

![](../images/datasets/user-guide/delete_dataset.png)

Aparece un cuadro de confirmación. Haga clic en **[!UICONTROL Delete]** para confirmar la eliminación del conjunto de datos.

![](../images/datasets/user-guide/confirm_delete.png)

## Eliminar un conjunto de datos habilitado para perfil

Si un conjunto de datos está habilitado para [!DNL Profile], al eliminar ese conjunto de datos a través de la interfaz de usuario, se eliminará del lago de datos y del almacén de perfiles en Platform.

Puede eliminar un conjunto de datos solo del almacén [!DNL Profile] (dejando los datos en el lago de datos) mediante la API de perfil del cliente en tiempo real. Para obtener más información, consulte la [guía de extremo de la API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md).

## Monitorización de la ingesta de datos

En la interfaz de usuario de [!DNL Experience Platform], haga clic en **[!UICONTROL Monitoring]** en el panel de navegación izquierdo. El tablero **[!UICONTROL Monitoring]** permite ver los estados de los datos entrantes desde la ingesta por lotes o de flujo continuo. Para ver los estados de los lotes individuales, haga clic en **[!UICONTROL Batch end-to-end]** o **[!UICONTROL Streaming end-to-end]**. En los tableros se enumeran todas las ejecuciones de ingesta por lotes o de flujo continuo, incluidas las que se han realizado correctamente, que han fallado o siguen en curso. Cada lista proporciona detalles del lote, incluido el ID del lote, el nombre del conjunto de datos de destino y el número de registros introducidos. Si el conjunto de datos de destino está habilitado para [!DNL Profile], también se muestra el número de registros de identidad y perfil ingestados.

![](../images/datasets/user-guide/batch_listing.png)

Puede hacer clic en un **[!UICONTROL Batch ID]** individual para acceder al tablero **[!UICONTROL Batch overview]** y ver los detalles del lote, incluidos los registros de errores en caso de que el lote no se ingrese.

![](../images/datasets/user-guide/batch_overview.png)

Si desea eliminar el lote, puede hacerlo haciendo clic en **[!UICONTROL Delete batch]** que se encuentra cerca de la parte superior derecha del panel. Al hacerlo, también se eliminarán sus registros del conjunto de datos al que se incorporó originalmente el lote.

![](../images/datasets/user-guide/delete_batch.png)

## Pasos siguientes

Esta guía del usuario proporciona instrucciones para realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario [!DNL Experience Platform]. Para ver los pasos sobre la realización de flujos de trabajo [!DNL Platform] comunes que implican conjuntos de datos, consulte los siguientes tutoriales:

* [Creación de un conjunto de datos mediante API](create.md)
* [Consultar datos de conjuntos de datos mediante la API de acceso a datos](../../data-access/home.md)
* [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../../profile/tutorials/dataset-configuration.md)
