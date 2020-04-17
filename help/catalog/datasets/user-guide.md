---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del usuario de conjuntos de datos
topic: datasets
translation-type: tm+mt
source-git-commit: 7d3f64db787aebe46179c0e08ad01878b0ad2877

---


# Guía del usuario de conjuntos de datos

Esta guía del usuario proporciona instrucciones sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Conjuntos](overview.md)de datos: almacenamiento y administración para la persistencia de datos en la plataforma de experiencia.
* [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Editor](../../xdm/tutorials/create-schema-ui.md)de Esquemas: Obtenga información sobre cómo crear sus propios esquemas XDM personalizados mediante el Editor de Esquemas en la interfaz de usuario de la plataforma.
* [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Administración](../../data-governance/home.md)de datos: Garantizar el cumplimiento de las regulaciones, restricciones y políticas relativas al uso de los datos del cliente.

## datasets de Vista

En la interfaz de usuario de la plataforma de experiencia, haga clic en **Conjuntos** de datos en el panel de navegación izquierdo para abrir el panel *Conjuntos* de datos. El panel lista todos los conjuntos de datos disponibles para su organización. Se muestran detalles de cada conjunto de datos de la lista, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de la ingestión más reciente.

![](../images/datasets/user-guide/browse_datasets.png)

Haga clic en el nombre de un conjunto de datos para acceder a la pantalla de actividad *del* conjunto de datos y ver los detalles del conjunto de datos seleccionado. La ficha actividad incluye un gráfico que visualiza la tasa de mensajes que se consumen, así como una lista de lotes exitosos y fallidos.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Previsualización de un conjunto de datos

En la pantalla actividad *de* conjuntos de datos, haga clic en Conjunto de datos **de** Previsualización cerca de la esquina superior derecha de la pantalla para realizar una previsualización de hasta 100 filas de datos. Si el conjunto de datos está vacío, el vínculo de previsualización se desactivará y, en su lugar, dirá que la **Previsualización no está disponible**.

![](../images/datasets/user-guide/click_to_preview.png)

En la ventana previsualización, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

![](../images/datasets/user-guide/preview_dataset.png)

Para obtener métodos más sólidos para acceder a los datos, Experience Platform proporciona servicios de flujo descendente como Consulta Service y JupyterLab para explorar y analizar los datos. Consulte los siguientes documentos para obtener más información:

* [Visión general del servicio de Consulta](../../query-service/home.md)
* [Guía del usuario de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Crear un conjunto de datos {#create}

Para crear un nuevo conjunto de datos, haga inicio haciendo clic en **Crear conjunto de datos** en el panel *Conjuntos* de datos.

![](../images/datasets/user-guide/click_to_create.png)

En la pantalla siguiente, se muestran las dos opciones siguientes para crear un nuevo conjunto de datos:

* [Crear conjunto de datos a partir de esquema](#create-a-dataset-with-an-existing-schema)
* [Crear conjunto de datos a partir de un archivo CSV](#create-a-dataset-with-a-csv-file)

### Crear un conjunto de datos con un esquema existente

En la pantalla *Crear conjunto de datos* , haga clic en **Crear conjunto de datos desde esquema** para crear un nuevo conjunto de datos vacío.

![](../images/datasets/user-guide/create_dataset_schema.png)

Aparece el paso *Seleccionar esquema* . Explore la lista de esquemas y seleccione el esquema al que se adherirá el conjunto de datos antes de hacer clic en **Siguiente**.

![](../images/datasets/user-guide/select_schema.png)

Aparece el paso *Configurar conjunto de datos* . Proporcione un nombre y una descripción opcionales al conjunto de datos y, a continuación, haga clic en **Finalizar** para crearlo.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Crear un conjunto de datos con un archivo CSV

Cuando se crea un conjunto de datos con un archivo CSV, se crea un esquema ad hoc para proporcionar al conjunto de datos una estructura que coincida con el archivo CSV proporcionado. En la pantalla *Crear conjunto de datos* , haga clic en el cuadro que indica **Crear conjunto de datos a partir del archivo** CSV.

![](../images/datasets/user-guide/create_dataset_csv.png)

Aparece el paso *Configurar* . Proporcione un nombre y una descripción opcionales al conjunto de datos y, a continuación, haga clic en **Siguiente**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Aparece el paso *Añadir datos* . Para cargar el archivo CSV, arrástrelo y colóquelo en el centro de la pantalla o haga clic en **Examinar** para explorar el directorio de archivos. El archivo puede tener un tamaño de hasta diez gigabytes. Una vez cargado el archivo CSV, haga clic en **Guardar** para crear el conjunto de datos.

>[!NOTE] Los nombres de columna CSV deben tener inicios con caracteres alfanuméricos y solo pueden contener letras, números y subrayados.

![](../images/datasets/user-guide/add_csv_data.png)

## Habilitar un conjunto de datos para el Perfil del cliente en tiempo real

Cada conjunto de datos tiene la capacidad de enriquecer los perfiles de los clientes con sus datos ingestados. Para ello, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en el Perfil del cliente en tiempo real. Un esquema compatible cumple los siguientes requisitos:

* El esquema tiene al menos un atributo especificado como propiedad de identidad.
* El esquema tiene una propiedad de identidad definida como la identidad principal.

Para obtener más información sobre cómo activar un esquema para Perfil, consulte la guía [del usuario del Editor de](../../xdm/tutorials/create-schema-ui.md)Esquemas.

Para habilitar un conjunto de datos para Perfil, acceda a la pantalla de actividad *de* conjuntos de datos y haga clic en el botón de alternancia de **Perfil** de la columna *Propiedades* . Una vez habilitados, los datos que se ingieren en el conjunto de datos también se utilizarán para rellenar los perfiles de los clientes.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Si un conjunto de datos ya contiene datos y se habilita para el Perfil, Perfil no consumirá los datos existentes. Después de habilitar un conjunto de datos para el Perfil, se recomienda volver a ingerir los datos existentes para que rellenen los perfiles de los clientes.

## Administrar y aplicar la administración de datos en un conjunto de datos

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo de administración de datos principal para la plataforma de experiencia. Las etiquetas DULE permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Consulte la información general [sobre el Gobierno de](../../data-governance/home.md) datos para obtener más información sobre las etiquetas o consulte la guía [del usuario sobre las etiquetas de uso de](../../data-governance/labels/overview.md) datos para obtener instrucciones sobre cómo aplicar etiquetas a los conjuntos de datos.

## Eliminar un conjunto de datos

Puede eliminar un conjunto de datos accediendo primero a su pantalla de actividad ** de conjunto de datos. A continuación, haga clic en **Eliminar conjunto de datos** para eliminarlo.

>[!NOTE] Los conjuntos de datos creados y utilizados por aplicaciones y servicios de Adobe (como Adobe Analytics, Adobe Audiencia Manager o el servicio de toma de decisiones) no se pueden eliminar.

![](../images/datasets/user-guide/delete_dataset.png)

Aparece un cuadro de confirmación. Haga clic en **Eliminar** para confirmar la eliminación del conjunto de datos.

![](../images/datasets/user-guide/confirm_delete.png)

## Eliminar un conjunto de datos habilitado para Perfil

Si un conjunto de datos está habilitado para el Perfil, eliminarlo a través de la interfaz de usuario deshabilita el conjunto de datos para la ingestión, pero no elimina automáticamente el conjunto de datos en el servidor. Para eliminar completamente el conjunto de datos, incluidos los datos de perfil e identidad que proporciona, se debe realizar una solicitud de eliminación adicional. Para ver los pasos sobre cómo eliminar correctamente los datos del almacén de Perfiles, consulte la [subguía de la API de Perfil del cliente en tiempo real sobre los trabajos del sistema de perfil, también conocida como &quot;eliminar solicitudes&quot;](../../profile/api/profile-system-jobs.md).

## Monitoreo de la ingesta de datos

En la interfaz de usuario de la plataforma de experiencia, haga clic en **Supervisión** en el panel de navegación izquierdo. El panel *de supervisión* le permite realizar la vista de los estados de los datos de entrada desde la ingestión por lotes o por flujo continuo. Para vista de los estados de lotes individuales, haga clic en *Lote de extremo a extremo* o en *Flujo de extremo a extremo*. Los paneles listas todas las ejecuciones de ingestión por lotes o de flujo continuo, incluidas las que se hayan realizado correctamente, hayan fallado o estén en curso. Cada listado proporciona detalles del lote, incluyendo el ID del lote, el nombre del conjunto de datos del destinatario y el número de registros ingestados. Si el conjunto de datos de destinatario está habilitado para el Perfil, también se muestra el número de registros de identidad y perfil ingestados.

![](../images/datasets/user-guide/batch_listing.png)

Puede hacer clic en un ID **de** lote individual para acceder al panel de información general *de* lote y ver los detalles del lote, incluidos los registros de errores en caso de que el lote no se ingrese.

![](../images/datasets/user-guide/batch_overview.png)

Si desea eliminar el lote, puede hacerlo haciendo clic en **Eliminar lote** encontrado cerca de la parte superior derecha del panel. Al hacerlo, también se eliminarán los registros del conjunto de datos al que se ingerió originalmente el lote.

![](../images/datasets/user-guide/delete_batch.png)

## Pasos siguientes

Esta guía del usuario proporciona instrucciones para realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de la plataforma de experiencia. Para ver los pasos sobre la realización de flujos de trabajo comunes de plataforma que involucran conjuntos de datos, consulte los siguientes tutoriales:

* [Creación de un conjunto de datos mediante API](create.md)
* [Datos del conjunto de datos de Consulta mediante la API de acceso a datos](../../data-access/home.md)
* [Configurar un conjunto de datos para el Perfil de clientes en tiempo real y el servicio de identidad mediante API](../../profile/tutorials/dataset-configuration.md)