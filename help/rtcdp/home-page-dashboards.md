---
keywords: resumen de métricas; resumen de métricas de rtcdp
title: Página de inicio y paneles de Real-time Customer Data Platform
description: Paneles, página de inicio y primera experiencia de usuario en Adobe Experience Platform
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] página principal

La página de inicio de Adobe Real-time Customer Data Platform (Real-Time CDP) es la primera página que aparece después de iniciar sesión en Real-Time CDP.

La página de inicio de Real-Time CDP incluye un widget de introducción que le permite acceder rápidamente a varias funciones diferentes y una sección de métricas que muestra información actualizada sobre los datos de su organización.

Este documento proporciona información general sobre la página de inicio de Real-Time CDP y el panel de métricas.

![La página de inicio de la IU de Platform.](assets/platform-home/home.png)

## Widget de introducción

El [!UICONTROL Introducción a Real-Time Customer Profile] El widget se divide en cuatro secciones:

* **Ingesta de datos en Platform**: este widget le dirige al catálogo de fuentes. Utilice el catálogo de fuentes para seleccionar un origen e introducir los datos en el Experience Platform. Para obtener más información, lea la [información general de orígenes](../sources/home.md)
* **Estructuras de datos de modelo**: este widget le dirige a la descripción general de los esquemas. Utilice la descripción general de los esquemas para buscar esquemas existentes o crear bloques de creación que describan la estructura de los datos. Para obtener más información, lea la [información general sobre esquemas](../xdm/home.md).
* **Audiencias de segmentos**: este widget le dirige a [!DNL Segment Builder] en la interfaz de usuario. Utilice el [!DNL Segment Builder] para interactuar con elementos de datos de perfil y definir reglas para los segmentos. Para obtener más información, lea la [Resumen del servicio de segmentación](../segmentation/home.md).
* **Envío de datos a destinos**: este widget le dirige al catálogo de destinos. Utilice el catálogo de destinos para seleccionar un destino al que pueda conectarse y enviar segmentos. Para obtener más información, lea la [información general sobre destinos](../destinations/home.md)

![La página de inicio de la IU de Platform muestra el widget de introducción](assets/platform-home/getting-started-widget.png)

## Panel de métricas

El panel de métricas muestra información actualizada sobre los datos del Experience Platform. El tablero se divide en dos secciones:

### La tabla de clasificación

La tabla de clasificación muestra el número total actual de esquemas, conjuntos de datos, perfiles y segmentos en su organización, así como su fecha de actualización más reciente.

![La sección de la tabla de clasificación de la página de inicio de la IU de Platform.](assets/platform-home/leaderboard.png)

* **Esquemas totales**: La **Esquemas totales** counter muestra el número de esquemas del sistema. Este contador se actualiza cuando se crea un esquema. Para obtener más información, lea la [información general sobre esquemas](../xdm/home.md).
* **Total de conjuntos de datos**: La **Conjuntos de datos totales** muestra el número de conjuntos de datos del sistema y la cantidad de datos en [!DNL Platform]. Este contador se actualiza cuando se crea un conjunto de datos. Para obtener más información sobre los conjuntos de datos, lea la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).
* **Perfiles totales**: La **Perfiles** El recuento muestra el número total de personas con perfiles en la [!DNL Real-Time Customer Profile]. No incluye fragmentos de perfil. Esta es su audiencia total a la que puede dirigirse. Este recuento utiliza el valor predeterminado [política de combinación](profile/merge-policies.md) tal como se establece en la configuración de la política de combinación en Perfil unificado. El número de perfiles se actualiza una vez cada 24 horas. Para obtener más información sobre los perfiles, lea la [Resumen del perfil del cliente en tiempo real](../profile/home.md).
* **Total de segmentos**: **Segmentos** muestra el número total de segmentos creados para la organización. Este número se actualiza cuando se crean nuevos segmentos. Para obtener más información sobre los segmentos, lea la [Resumen del servicio de segmentación](../segmentation/home.md).

### Elementos recientes

Elementos recientes enumera los cambios más recientes realizados en su organización. En el ejemplo siguiente, los cambios más recientes pertenecen a conjuntos de datos, fuentes, segmentos y destinos.

![La sección Elementos recientes en la página de inicio de la IU de Platform.](assets/platform-home/recent-items.png)

* **Conjuntos de datos recientes**: La **[!UICONTROL Conjuntos de datos recientes]** muestra los cinco conjuntos de datos creados más recientemente dentro de la organización. Esta lista se actualiza cuando se crea un nuevo conjunto de datos. Seleccione un conjunto de datos para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todo]** para obtener una lista de conjuntos de datos. Desde allí, puede seleccionar una fuente específica para obtener más información. Para obtener más información sobre los conjuntos de datos, consulte la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).
* **Fuentes recientes**: La **[!UICONTROL Fuentes recientes]** La tarjeta de métrica de muestra los cinco orígenes más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo origen. Seleccione un origen para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todo]** para obtener una lista de fuentes. Desde allí, puede seleccionar una fuente específica para obtener más información. Para obtener más información sobre las fuentes, consulte [Resumen de orígenes](../sources/home.md).
* **Segmentos recientes**: La **[!UICONTROL Segmentos recientes]** La tarjeta de métrica de muestra los cinco segmentos creados más recientemente dentro de la organización. Esta lista se actualiza cuando se crea un nuevo segmento. Seleccione un segmento para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todo]** para obtener una lista de segmentos. Para obtener más información sobre los segmentos, consulte [Resumen del servicio de segmentación](../segmentation/home.md).
* **Destinos recientes**: La **[!UICONTROL Destinos recientes]** La tarjeta de métrica de muestra los cinco destinos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo destino. Seleccione un destino para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todo]** para obtener una lista de destinos. Para obtener más información, lea la [información general sobre destinos](../destinations/home.md).

## Recursos

Por último, el widget de recursos le proporciona recursos de documentación adicionales a los que puede hacer referencia. Se incluyen:

![La sección de recursos de la página de inicio de la IU de Platform.](assets/platform-home/resources.png)

* [Explicación de los esquemas](../xdm/schema/composition.md)
* [Conexión de orígenes](../sources/home.md)
* [Cómo rellenar el perfil de cliente en tiempo real](../profile/home.md)
* [Conexión de destinos](../destinations/home.md)
* [Administrar acceso](../access-control/abac/overview.md)

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
