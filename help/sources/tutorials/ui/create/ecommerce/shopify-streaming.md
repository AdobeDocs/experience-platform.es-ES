---
title: Crear Una Conexión De Flujo De Datos Y Una Conexión De Flujo De Flujo De Navegación Shopify En La Interfaz De Usuario
description: Aprenda a crear una conexión de origen de Shopify Streaming y un flujo de datos mediante la interfaz de usuario de Platform
badge: Beta
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos para [!DNL Shopify Streaming] datos mediante la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Shopify Streaming] conexión de origen y flujo de datos mediante la interfaz de usuario de Platform.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Este tutorial requiere que haya completado la configuración previa para su [!DNL Shopify Streaming] cuenta. Para ver los pasos sobre la configuración de la cuenta, lea la [[!DNL Shopify Streaming] información general](../../../../connectors/ecommerce/shopify-streaming.md).

## Conecte su [!DNL Shopify Streaming] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **comercio electrónico** categoría, seleccione [!DNL Shopify Streaming]y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes del Experience Platform](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Seleccionar datos

La variable **[!UICONTROL Seleccionar datos]** , proporcionando una interfaz para que seleccione los datos que aporta a Platform.

* La parte izquierda de la interfaz es un navegador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Select **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. Como alternativa, puede arrastrar y soltar el archivo JSON que desea cargar en el [!UICONTROL Arrastrar y soltar archivos] panel.

![El paso añadir datos del flujo de trabajo de fuentes.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema que ha cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![El paso de vista previa del flujo de trabajo de fuentes.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Detalles de flujo de datos

La variable **Detalles de flujo de datos** aparece, proporcionando opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como una oportunidad para proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de ingesta de perfiles, diagnóstico de errores, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de flujo de datos detallado del flujo de trabajo de origen.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Asignación

La variable [!UICONTROL Asignación] aparece, proporcionando una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que seleccione. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Una vez asignados correctamente los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![El paso de asignación del flujo de trabajo de fuentes.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Consulte

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![El paso de revisión del flujo de trabajo de fuentes.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Obtener la URL del extremo de flujo continuo

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto final se utilizará para suscribirse a su enlace web, permitiendo que su fuente de transmisión se comunique con el Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a la [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión de origen y un flujo de datos para su [!DNL Shopify Streaming] cuenta. Para obtener instrucciones sobre cómo conectar su [!DNL Shopify Streaming] cuenta con la API de , lea el tutorial en [creación de una conexión de origen y flujo de datos a flujo [!DNL Shopify] datos mediante la API de servicio de flujo](../../../api/create/ecommerce/shopify-streaming.md).
