---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: Enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático
topic: tutorial
type: Tutorial
description: Este documento proporciona un tutorial paso a paso para enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático, los pasos se desglosan en las siguientes secciones, crear un esquema/conjunto de datos de salida, configurar un esquema/conjunto de datos de salida y crear segmentos mediante el Generador de segmentos.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# Enriquecimiento [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones y perspectivas de datos. Cuando las perspectivas de aprendizaje automático se ingieren en un conjunto de datos [!DNL Profile]habilitado, esos mismos datos también se ingieren como [!DNL Profile] registros que luego se pueden segmentar en subconjuntos de elementos relacionados mediante [!DNL Experience Platform Segmentation Service].

Este documento proporciona un tutorial paso a paso para enriquecerse [!DNL Real-time Customer Profile] con las perspectivas de aprendizaje automático. Los pasos se desglosan en las siguientes secciones:

1. [Crear un esquema de salida y un conjunto de datos](#create-an-output-schema-and-dataset)
2. [Configurar un esquema de salida y un conjunto de datos](#configure-an-output-schema-and-dataset)
3. [Creación de segmentos mediante el Generador de segmentos](#create-segments-using-the-segment-builder)

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos aspectos de la [!DNL Adobe Experience Platform] ingesta [!DNL Profile] de datos y la creación de segmentos. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../../rtcdp/overview.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Identity Service]](../../identity-service/home.md):: Permite [!DNL Real-time Customer Profile] el enlace de identidades de orígenes de datos dispares que se están ingeriendo en la plataforma.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

Además de los documentos mencionados, se recomienda revisar también las siguientes guías sobre esquemas y el Editor de Esquemas:

* [Conceptos básicos de la composición](../../xdm/schema/composition.md)de esquemas: Describe los esquemas XDM, los componentes básicos, los principios y las prácticas recomendadas para la composición de esquemas que se van a utilizar en [!DNL Experience Platform].
* [Tutorial](../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Proporciona instrucciones detalladas para crear esquemas con el Editor de Esquemas en [!DNL Experience Platform].

## Crear un esquema de salida y un conjunto de datos {#create-an-output-schema-and-dataset}

El primer paso hacia el enriquecimiento [!DNL Real-time Customer Profile] con perspectivas de puntuación es saber qué objeto real (como una persona) definen sus datos. Conocer los datos le permite describir y diseñar una estructura que se adapte a los datos, como diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). En esta sección se proporcionan instrucciones básicas para crear un esquema con el generador de esquemas. Para ver un tutorial más detallado, consulte el tutorial sobre la [creación de un esquema con el Editor](../../xdm/tutorials/create-schema-ui.md)de Esquemas.

1. En Adobe Experience Platform, haga clic en la ficha **[!UICONTROL Esquema]** para acceder al explorador de esquema. Haga clic en **[!UICONTROL Crear Esquema]** para acceder al Editor **de**Esquemas, donde puede crear esquemas de forma interactiva.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. En la ventana **Composición** , haga clic en **[!UICONTROL Asignar]** para examinar las clases disponibles.
   * Para asignar una clase existente, haga clic en y resalte la clase deseada y, a continuación, haga clic en **[!UICONTROL Asignar clase]**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Para crear una clase personalizada, haga clic en **[!UICONTROL Crear nueva clase]** que se encuentre cerca de la parte central de la ventana del explorador. Proporcione un nombre de clase, una descripción y elija el comportamiento de la clase. Haga clic en **[!UICONTROL Asignar clase]** una vez que haya terminado.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)

   En este punto, la estructura del esquema debe contener algunos campos de clase y está listo para asignar mezclas. Una mezcla es un grupo de uno o más campos que describen un concepto en particular.

3. En la ventana **Composición** , haga clic en **[!UICONTROL Añadir]** en la subsección **Mezclas** .
   * Para asignar una mezcla existente, haga clic en y resalte la mezcla deseada y, a continuación, haga clic en **[!UICONTROL Añadir mezcla]**. A diferencia de las clases, se pueden asignar varias mezclas a un solo esquema siempre que sea apropiado.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Para crear una nueva mezcla, haga clic en **[!UICONTROL Crear nueva mezcla]** que se encuentre cerca de la parte central de la ventana del explorador. Proporcione un nombre y una descripción para la mezcla y, a continuación, haga clic en **[!UICONTROL Asignar mezcla]** una vez que haya terminado.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Para agregar campos de mezcla, haga clic en el nombre de la mezcla dentro de la ventana *Composición* . A continuación, se le proporcionará la opción de agregar campos mezclados haciendo clic en **[!UICONTROL Añadir campo]** en la ventana *Estructura* . Asegúrese de proporcionar las propiedades de mezcla correspondientes.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Una vez que haya terminado de crear el esquema, haga clic en el campo de nivel superior del esquema dentro de la ventana *Estructura* para mostrar las propiedades del esquema en la ventana de propiedades de la derecha. Proporcione un nombre y una descripción, y haga clic en **[!UICONTROL Guardar]** para crear el esquema.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Cree un conjunto de datos de salida con el esquema recién creado haciendo clic en **[!UICONTROL Conjuntos]** de datos en la columna de navegación izquierda y, a continuación, haga clic en **[!UICONTROL Crear conjunto de datos]**. En la pantalla siguiente, elija **[!UICONTROL Crear conjunto de datos desde esquema]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. Con el navegador de esquema, busque y seleccione el esquema recién creado y, a continuación, haga clic en **[!UICONTROL Siguiente]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Proporcione un nombre y una descripción opcional y, a continuación, haga clic en **[!UICONTROL Finalizar]** para crear el conjunto de datos.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Ahora que ha creado un conjunto de datos de esquema de salida, puede continuar en la siguiente sección para configurarlo y habilitarlo para el enriquecimiento de Perfil.

## Configurar un esquema de salida y un conjunto de datos {#configure-an-output-schema-and-dataset}

Antes de habilitar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para tener un campo de identidad principal y luego habilitar el esquema para [!DNL Profile]. Si desea crear y activar un nuevo esquema, puede consultar el tutorial sobre la [creación de un esquema con el Editor](../../xdm/tutorials/create-schema-ui.md)de Esquemas. De lo contrario, siga las instrucciones a continuación para habilitar un esquema y un conjunto de datos existentes.

1. En Adobe Experience Platform, utilice el navegador esquema para buscar el esquema de salida en el que desea activar y haga clic [!DNL Profile] en su nombre para vista de la composición.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Expanda la estructura de esquema y busque un campo adecuado para establecerlo como identificador principal. Haga clic en el campo que desee para mostrar sus propiedades.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Establezca el campo como identidad principal habilitando la propiedad **[!UICONTROL Identity]** del campo, la propiedad **[!UICONTROL Primary Identity]** y, a continuación, seleccionando una Área de nombres **** Identity apropiada. Haga clic en **[!UICONTROL Aplicar]** una vez que haya realizado los cambios.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Haga clic en el objeto de nivel superior de la estructura del esquema para mostrar las propiedades del esquema y activar el esquema para el Perfil alternando el conmutador de **[!UICONTROL Perfil]** . Haga clic en **[!UICONTROL Guardar]** para finalizar los cambios. El conjunto de datos que se creó con este esquema ahora se puede habilitar para Perfil.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Utilice el explorador de conjuntos de datos para encontrar el conjunto de datos en el que desea habilitar y haga clic [!DNL Profile] en su nombre para acceder a sus detalles.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Habilite el conjunto de datos para [!DNL Profile] conmutar el conmutador de **[!UICONTROL Perfil]** que se encuentra en la columna de información derecha.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

Cuando los datos se ingieren en un conjunto de datos [!DNL Profile]habilitado, esos mismos datos también se ingieren como [!DNL Profile] registros. Ahora que el esquema y el conjunto de datos están preparados, genere algunos datos en el conjunto de datos realizando ejecuciones de puntuación utilizando un modelo adecuado y continúe con este tutorial para crear segmentos de perspectiva mediante el Generador de segmentos.

## Creación de segmentos mediante el Generador de segmentos {#create-segments-using-the-segment-builder}

Ahora que ha generado e ingestado perspectivas en el conjunto de datos [!DNL Profile]habilitado, puede administrar esos datos identificando subconjuntos de elementos relacionados mediante el Generador de segmentos. Siga los pasos a continuación para crear sus propios segmentos.

1. En Adobe Experience Platform, haga clic en la ficha **[!UICONTROL Segmentos]** seguida de **[!UICONTROL Crear segmento]** para acceder al Generador de segmentos.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. En el Generador de segmentos, el carril izquierdo proporciona acceso a los componentes principales de los segmentos: atributos, eventos y segmentos existentes. Cada bloque de creación aparece en su propia ficha respectiva. Seleccione la clase a la que se extiende el esquema [!DNL Profile]habilitado y, a continuación, busque los componentes básicos del segmento.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Arrastre y suelte los bloques de creación en el lienzo del generador de reglas, rellénelos con instrucciones comparativas.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Mientras crea el segmento, puede previsualización los resultados estimados del mismo observando el panel Propiedades ** del segmento.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Seleccione una directiva **[!UICONTROL de]** combinación adecuada, proporcione un nombre y una descripción opcional y, a continuación, haga clic en **[!UICONTROL Guardar]** para completar el nuevo segmento.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Pasos siguientes {#next-steps}

Este documento lo guió por los pasos necesarios para habilitar un esquema y un conjunto de datos [!DNL Profile], y mostró brevemente el flujo de trabajo para crear segmentos de perspectiva mediante el Generador de segmentos. Para obtener más información sobre los segmentos y el Generador de segmentos, consulte la descripción general [del servicio](../../segmentation/home.md)Segmentación.