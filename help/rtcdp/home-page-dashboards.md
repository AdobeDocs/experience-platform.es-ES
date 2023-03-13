---
keywords: resumen de métricas; resumen de métricas de rtcdp
title: Página de inicio y paneles de Real-time Customer Data Platform
description: Paneles, página de inicio y primera experiencia de usuario en Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---

# [!DNL Real-Time Customer Data Platform] página de inicio y paneles

La página de inicio de Adobe Real-time Customer Data Platform (Real-Time CDP), que incluye un panel de métricas, aparece al iniciar sesión en Real-Time CDP.

La página de inicio es solo uno de los lugares en los que aparecen las tarjetas de métricas. Real-Time CDP proporciona tarjetas de métricas en toda la experiencia. Estas métricas le informan sobre los datos, el perfil y las audiencias de segmentos en el sistema.

![imagen](assets/home.png)

Si no hay datos en el sistema cuando inicia sesión en Real-Time CDP, el panel de la página principal no aparece. En este caso, la página de inicio proporciona material de aprendizaje por primera vez para la experiencia del usuario. A medida que se recopilan los datos, es decir, como <!--sources-->se crean conjuntos de datos, perfiles, segmentos y destinos y los datos fluyen al sistema; el tablero se actualiza automáticamente para mostrar información sobre esos datos<!-- in metric cards-->.

## Vista del panel de página principal

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

El tablero se divide en<!-- two areas.-->:

* **La tabla de clasificación** está en la parte superior del panel. La tabla de clasificación muestra el número de conjuntos de datos, perfiles, segmentos y destinos del sistema.

   ![imagen](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Elementos recientes** enumera los cinco conjuntos de datos, fuentes, segmentos y destinos más recientes agregados al sistema.

   ![imagen](assets/recent.png)

Hay métricas adicionales disponibles en otras partes de Real-time Customer Data Platform, por ejemplo, para perfiles y segmentos.

### Conjuntos de datos

El **[!UICONTROL Conjuntos de datos]** muestra el número de conjuntos de datos del sistema y la cantidad de datos en [!DNL Platform]. Este contador se actualiza cuando se crea un conjunto de datos.

Para obtener más información sobre los conjuntos de datos, consulte la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

### Perfiles

El **[!UICONTROL Perfiles]** El recuento muestra el número total de personas con perfiles en la [!DNL Real-Time Customer Profile]. No incluye fragmentos de perfil. Esta es su audiencia total a la que puede dirigirse.

Este recuento utiliza el valor predeterminado [política de combinación](profile/merge-policies.md) tal como se establece en la configuración de la política de combinación en Perfil unificado.

El número de perfiles se actualiza una vez cada 24 horas.

Para obtener más información sobre los perfiles, consulte [Una vista unificada de su cliente en Real-Time CDP](profile/profile-overview.md).

### Segmentos

**[!UICONTROL Segmentos]** muestra el número total de segmentos creados para la organización. Este número se actualiza cuando se crean nuevos segmentos.

Para obtener más información sobre los segmentos, consulte [Resumen del servicio de segmentación](segmentation/segmentation-overview.md).

### Destinos

**[!UICONTROL Destinos]** muestra el número total de destinos creados para la organización. Este número se actualiza cuando se crean nuevos destinos.

Para obtener más información sobre los destinos, consulte [Resumen de destinos](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Conjuntos de datos recientes

El **[!UICONTROL Conjuntos de datos recientes]** muestra los cinco conjuntos de datos creados más recientemente dentro de la organización. Esta lista se actualiza cuando se crea un nuevo conjunto de datos.

Seleccione un conjunto de datos para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver la lista de conjuntos de datos. Desde allí, puede seleccionar una fuente específica para obtener más información.

Para obtener más información sobre los conjuntos de datos, consulte la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

### Fuentes recientes

El **[!UICONTROL Fuentes recientes]** La tarjeta de métrica de muestra los cinco orígenes más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo origen.

Seleccione un origen para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver la lista de fuentes. Desde allí, puede seleccionar una fuente específica para obtener más información.

Para obtener más información sobre las fuentes, consulte [Resumen de orígenes](sources/sources-overview.md).

### Segmentos recientes

El **[!UICONTROL Segmentos recientes]** La tarjeta de métrica de muestra los cinco segmentos creados más recientemente dentro de la organización. Esta lista se actualiza cuando se crea un nuevo segmento.

Seleccione un segmento para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver información sobre más segmentos.

Para obtener más información sobre los segmentos, consulte [Resumen del servicio de segmentación](segmentation/segmentation-overview.md).

### Destinos recientes

El **[!UICONTROL Destinos recientes]** La tarjeta de métrica de muestra los cinco destinos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo destino.

Seleccione un destino para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver información sobre más destinos.

Para obtener más información sobre los destinos, consulte [Resumen de destinos](destinations/overview.md).
