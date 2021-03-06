---
keywords: información general sobre las métricas; información general sobre las métricas de rtcdp
title: Página principal de Real-time Customer Data Platform y tableros
description: Paneles, página de inicio y primera experiencia de usuario en Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---

# [!DNL Real-time Customer Data Platform] página de inicio y tableros

La página de inicio de Real-time Customer Data Platform (CDP en tiempo real), que incluye un panel de métricas, aparece cuando inicia sesión en CDP en tiempo real.

La página de inicio es solo uno de los lugares en los que aparecen las tarjetas de métricas. CDP en tiempo real proporciona tarjetas de métricas a lo largo de su experiencia. Estas métricas le informan sobre los datos, el perfil y las audiencias de segmento del sistema.

![imagen](assets/home.png)

Si no hay datos en el sistema cuando inicia sesión en CDP en tiempo real, no aparece el panel en la página principal. En este caso, la página principal proporciona material de aprendizaje para una primera experiencia de usuario. A medida que se recopilan los datos, es decir, como <!--sources-->se crean conjuntos de datos, perfiles, segmentos y destinos, y los flujos de datos se actualizan en el sistema; el tablero se actualiza automáticamente para mostrar información sobre esos datos<!-- in metric cards-->.

## Vista del tablero de la página de inicio

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

El tablero se divide en<!-- two areas.-->:

* **El panel de control** en la parte superior del tablero. El panel de control muestra la cantidad de conjuntos de datos, perfiles, segmentos y destinos del sistema.

   ![imagen](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Artículos recientes** enumera los cinco conjuntos de datos, fuentes, segmentos y destinos más recientes agregados al sistema.

   ![imagen](assets/recent.png)

En otras partes de Real-time Customer Data Platform hay disponibles métricas adicionales, por ejemplo para perfiles y segmentos.

### Conjuntos de datos

La variable **[!UICONTROL Conjuntos de datos]** counter muestra la cantidad de conjuntos de datos en el sistema y la cantidad de datos en [!DNL Platform]. Este contador se actualiza cuando se crea un conjunto de datos.

Para obtener más información sobre los conjuntos de datos, consulte la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

### Perfiles

La variable **[!UICONTROL Perfiles]** count muestra el número total de personas con perfiles en la variable [!DNL Real-time Customer Profile]. No incluye fragmentos de perfil. Esta es su audiencia total a la que puede dirigirse.

Este recuento utiliza el valor predeterminado [combinar directiva](profile/merge-policies.md) tal y como se establece en la configuración de directiva de combinación en Perfil unificado.

El número de perfiles se actualiza una vez cada 24 horas.

Para obtener más información sobre los perfiles, consulte [Una visión unificada de su cliente en CDP en tiempo real](profile/profile-overview.md).

### Segmentos

**[!UICONTROL Segmentos]** muestra el número total de segmentos creados para la organización. Este número se actualiza cuando se crean nuevos segmentos.

Para obtener más información sobre los segmentos, consulte [Información general del servicio de segmentación](segmentation/segmentation-overview.md).

### Destinos

**[!UICONTROL Destinos]** muestra el número total de destinos creados para la organización. Este número se actualiza cuando se crean nuevos destinos.

Para obtener más información sobre los destinos, consulte [Información general sobre destinos](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Conjuntos de datos recientes

La variable **[!UICONTROL Conjuntos de datos recientes]** la tarjeta muestra los cinco conjuntos de datos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo conjunto de datos.

Seleccione un conjunto de datos para ver los detalles de ese elemento, o **[!UICONTROL Ver todo]** para ver la lista de conjuntos de datos. Desde allí, puede seleccionar una fuente específica para obtener más información.

Para obtener más información sobre los conjuntos de datos, consulte la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

### Fuentes recientes

La variable **[!UICONTROL Fuentes recientes]** tarjeta de métrica muestra las cinco fuentes más recientes creadas dentro de la organización. Esta lista se actualiza cuando se crea un nuevo origen.

Seleccione un origen para ver los detalles de ese elemento, o bien **[!UICONTROL Ver todo]** para ver la lista de fuentes. Desde allí, puede seleccionar una fuente específica para obtener más información.

Para obtener más información sobre las fuentes, consulte [Resumen de fuentes](sources/sources-overview.md).

### Segmentos recientes

La variable **[!UICONTROL Segmentos recientes]** tarjeta de métrica muestra los cinco segmentos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo segmento.

Seleccione un segmento para ver los detalles de ese elemento, o bien **[!UICONTROL Ver todo]** para ver información sobre más segmentos.

Para obtener más información sobre los segmentos, consulte [Información general del servicio de segmentación](segmentation/segmentation-overview.md).

### Destinos recientes

La variable **[!UICONTROL Destinos recientes]** tarjeta de métrica muestra los cinco destinos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo destino.

Seleccione un destino para ver los detalles de ese elemento, o bien **[!UICONTROL Ver todo]** para ver información sobre más destinos.

Para obtener más información sobre los destinos, consulte [Información general sobre destinos](destinations/overview.md).
