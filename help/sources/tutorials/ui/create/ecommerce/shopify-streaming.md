---
title: Cree Una Conexión De Flujo De Datos Y Un Flujo De Datos De Shopify En La IU
description: Aprenda a crear una conexión de origen y un flujo de datos de Shopify Streaming mediante la interfaz de usuario de Experience Platform
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos para [!DNL Shopify Streaming] datos mediante la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen y un flujo de datos de [!DNL Shopify Streaming] mediante la interfaz de usuario de Experience Platform.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Este tutorial requiere que haya completado la configuración del requisito previo para la cuenta de [!DNL Shopify Streaming]. Para ver los pasos para configurar tu cuenta, lee la [[!DNL Shopify Streaming] descripción general](../../../../connectors/ecommerce/shopify-streaming.md).

## Conectar su cuenta de [!DNL Shopify Streaming]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **comercio electrónico**, seleccione [!DNL Shopify Streaming] y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes de Experience Platform](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Seleccionar datos

Aparecerá el paso **[!UICONTROL Seleccionar datos]**, que proporciona una interfaz para que pueda seleccionar los datos que trae a Experience Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccione **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en el panel [!UICONTROL Arrastrar y soltar archivos].

![Paso para agregar datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la utilidad [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Detalles del flujo de datos

Aparecerá el paso **Detalle del flujo de datos**, que le proporcionará opciones para usar un conjunto de datos existente o establecer uno nuevo para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de origen.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Asignación

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino que seleccione. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Revisar

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Obtener la URL del extremo de flujo continuo

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de flujo se comunique con Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a la página [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del panel [!UICONTROL Propiedades].

![Punto final de flujo continuo en la actividad del flujo de datos.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión de origen y un flujo de datos en su cuenta de [!DNL Shopify Streaming]. Para obtener instrucciones sobre cómo conectar su cuenta de [!DNL Shopify Streaming] mediante la API, lea el tutorial sobre [creación de una conexión de origen y un flujo de datos para transmitir [!DNL Shopify] datos mediante la API de Flow Service](../../../api/create/ecommerce/shopify-streaming.md).
