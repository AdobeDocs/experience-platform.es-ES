---
title: Página principal y tableros de la plataforma de datos del cliente en tiempo real
seo-title: Página principal y tableros de la plataforma de datos del cliente en tiempo real
description: Tableros, página principal y experiencia de usuario de Adobe Experience Platform por primera vez
seo-description: Tableros, página principal y experiencia de usuario de Adobe Experience Platform por primera vez
translation-type: tm+mt
source-git-commit: 6c8d0757d7e7568b1976823d9c52221374e67cbb

---


# Información general sobre las métricas de la plataforma de datos del cliente en tiempo real

La página de inicio de la Plataforma de datos del cliente en tiempo real (CDP en tiempo real) de Adobe, que incluye un tablero de métricas, aparece cuando inicia sesión en CDP en tiempo real.

La página principal es sólo uno de los lugares donde aparecen las tarjetas de métricas. CDP en tiempo real proporciona tarjetas de métricas a lo largo de toda la experiencia. Estas métricas le informan sobre los datos, el perfil y las audiencias de segmentos del sistema.

![image](assets/home2.jpg)

Si no hay datos en el sistema cuando inicia sesión en CDP en tiempo real, no aparece el tablero en la página principal. En este caso, la página principal proporciona material de aprendizaje para una primera experiencia de usuario. A medida que se recopilan los datos (es decir, a medida que se crean <!--sources-->conjuntos de datos, perfiles, segmentos y destinos y los datos fluyen al sistema), el tablero se actualiza automáticamente para mostrar información sobre esos datos<!-- in metric cards-->.

## Vista del tablero de la página principal

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

El tablero se divide en<!-- two areas.-->:

* **La tabla de clasificación** se encuentra en la parte superior del tablero. La tabla de clasificación muestra el número de conjuntos de datos, perfiles, segmentos y destinos del sistema.

   ![image](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Elementos** recientes enumera los cinco conjuntos de datos, fuentes, segmentos y destinos más recientes agregados al sistema.

   ![image](assets/home-recent.jpg)

En otras partes de la plataforma de datos del cliente en tiempo real hay disponibles métricas adicionales, por ejemplo, para perfiles y segmentos.

### Conjuntos de datos

El contador **[!UICONTROL Conjuntos]** de datos muestra el número de conjuntos de datos en el sistema y la cantidad de datos en Plataforma. Este contador se actualiza cuando se crea un conjunto de datos.

Para obtener más información sobre los conjuntos de datos, consulte [Ingesta de datos en Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Perfiles

El recuento de **[!UICONTROL perfiles]** muestra el número total de personas con perfiles en el perfil de cliente en tiempo real. No incluye fragmentos de perfil. Es la audiencia total a la que puede dirigirse.

Este recuento utiliza la directiva [de](profile/merge-policies.md) combinación predeterminada como se establece en la configuración de directiva de combinación en Perfil unificado.

El número de perfiles se actualiza una vez cada 24 horas.

Para obtener más información acerca de los perfiles, consulte [Una vista unificada de su cliente en CDP](profile/profile-overview.md)en tiempo real.

### Segmentos

**[!UICONTROL Los segmentos]** muestran el número total de segmentos creados para la organización. Este número se actualiza cuando se crean nuevos segmentos.

Para obtener más información sobre los segmentos, consulte Visión general [del servicio](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)de segmentación.

### Destinos

**[!UICONTROL Destinos]** muestra el número total de destinos creados para la organización. Este número se actualiza cuando se crean nuevos destinos.

Para obtener más información sobre los destinos, consulte Información general sobre [los destinos](destinations/destinations-overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### datasets recientes

La tarjeta de conjuntos de datos **** recientes muestra los cinco conjuntos de datos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo conjunto de datos.

Haga clic en un conjunto de datos para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver la lista de conjuntos de datos. Desde allí, puede hacer clic en una fuente específica para obtener detalles.

Para obtener más información sobre los conjuntos de datos, consulte [Ingesta de datos en Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md).

### Fuentes recientes

La tarjeta de métricas de fuentes **** recientes muestra las cinco fuentes más recientes creadas en la organización. Esta lista se actualiza cuando se crea un nuevo origen.

Haga clic en un origen para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver la lista de fuentes. Desde allí, puede hacer clic en una fuente específica para obtener detalles.

Para obtener más información sobre las fuentes, consulte Información general sobre [las fuentes](sources/sources-overview.md).

### Segmentos recientes

La tarjeta de métrica Segmentos **** recientes muestra los cinco segmentos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo segmento.

Haga clic en un segmento para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver información sobre más segmentos.

Para obtener más información sobre los segmentos, consulte Visión general [del servicio](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)de segmentación.

### Destinos recientes

La tarjeta de métrica Destinos **** recientes muestra los cinco destinos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo destino.

Haga clic en un destino para ver los detalles de ese elemento o **[!UICONTROL Ver todo]** para ver información sobre más destinos.

Para obtener más información sobre los destinos, consulte Información general sobre [los destinos](destinations/destinations-overview.md).
