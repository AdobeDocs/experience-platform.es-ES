---
keywords: Experience Platform;inicio;temas populares;sistema local;carga de archivos;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;
solution: Experience Platform
title: Creación de un conector de origen de carga de archivos locales en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen para el sistema local para llevar archivos locales a Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Crear un conector de origen de carga de archivos local en la interfaz de usuario

Este tutorial proporciona los pasos para crear un conector de origen de carga de archivos local para introducir archivos locales en Platform mediante la interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Carga de archivos locales en Platform

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Sistema local] categoría, seleccionar **[!UICONTROL Carga de archivo local]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/local/catalog.png)

### Usar un conjunto de datos existente

El [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea introducir los datos CSV en un conjunto de datos existente o en uno nuevo.

Para introducir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable.

Con un conjunto de datos seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional.

Durante este proceso, también puede activar [!UICONTROL Diagnósticos de error] y [!UICONTROL Ingesta parcial]. [!UICONTROL Diagnósticos de error] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] permite la ingesta de datos que contienen errores, hasta un determinado umbral que se define manualmente. Consulte la [resumen de ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

![existing-dataset](../../../../images/tutorials/create/local/existing-dataset.png)

### Usar un nuevo conjunto de datos

Para introducir los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre del conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable.

Con un esquema seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional y, a continuación, aplique la variable [!UICONTROL Diagnósticos de error] y [!UICONTROL Ingesta parcial] la configuración que desee para el flujo de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Seleccionar datos

El [!UICONTROL Seleccionar datos] Este paso se muestra y proporciona una interfaz para cargar los archivos locales y previsualizar su estructura y contenido. Seleccionar **[!UICONTROL Elegir archivos]** para cargar un archivo CSV desde el sistema local. También puede arrastrar y soltar el archivo CSV que desea cargar en la variable [!UICONTROL Arrastrar y soltar archivos] panel.

>[!TIP]
>
>Actualmente solo se admiten archivos CSV en la carga de archivos locales. El tamaño máximo de archivo para cada archivo es 1 GB.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar el contenido y la estructura del archivo.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Según el archivo, puede seleccionar un delimitador de columna como tabulaciones, comas, barras verticales o un delimitador de columna personalizado para los datos de origen. Seleccione el **[!UICONTROL Delimitador]** y, a continuación, seleccione el delimitador adecuado en el menú.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![delimitador](../../../../images/tutorials/create/local/delimiter.png)

## Asignación

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez que los conjuntos de asignaciones estén listos, seleccione **[!UICONTROL Finalizar]** y espere unos momentos para crear el nuevo flujo de datos.

![asignación](../../../../images/tutorials/create/local/mapping.png)

## Monitorización de la ingesta de datos

Una vez asignado y creado el archivo CSV, puede monitorizar los datos que se están introduciendo a través de él mediante el panel de monitorización. Para obtener más información, consulte el tutorial sobre [monitorización de fuentes y flujos de datos en la IU](../../../../../dataflows/ui/monitor-sources.md).

## Pasos siguientes

Al seguir este tutorial, ha asignado correctamente un archivo CSV sin formato a un esquema XDM y lo ha introducido en Platform. Estos datos ahora se pueden utilizar en la fase posterior [!DNL Platform] servicios como [!DNL Real-Time Customer Profile]. Consulte la descripción general de [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) para obtener más información.
