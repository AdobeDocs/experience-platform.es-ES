---
keywords: resumen de métricas; resumen de métricas de rtcdp
title: Página de inicio y paneles de Real-Time Customer Data Platform
description: Conozca varios paneles, la página de inicio y la experiencia del primer usuario de Adobe Real-Time CDP.
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 10%

---

# [!DNL Real-Time Customer Data Platform] página de inicio

La página de inicio de Adobe Real-Time Customer Data Platform (Real-Time CDP) es la primera página que aparece después de iniciar sesión en Real-Time CDP.

La página de inicio de Real-Time CDP incluye un widget de introducción que le permite acceder rápidamente a varias funciones diferentes y una sección de métricas que muestra información actualizada sobre los datos de su organización.

Este documento proporciona información general sobre la página de inicio de Real-Time CDP y el panel de métricas.

![Página de inicio de la interfaz de usuario de Experience Platform.](assets/platform-home/home.png)

## Widget de introducción

El widget [!UICONTROL Introducción al Perfil del cliente en tiempo real] se divide en cuatro secciones:

* **Ingesta de datos en Experience Platform**: este widget le dirige al catálogo de fuentes. Utilice el catálogo de fuentes para seleccionar un origen e introducir los datos en Experience Platform. Seleccione **[Configurar orígenes]** para navegar al catálogo de orígenes. Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
* **Estructuras de datos de modelo**: este widget le dirige a la descripción general de los esquemas. Utilice la descripción general de los esquemas para buscar esquemas existentes o crear un modelo que describa la estructura de los datos. Seleccione **[!UICONTROL Crear esquema]** para navegar a la interfaz de creación de esquemas. Para obtener más información, lea la [descripción general de esquemas](../xdm/home.md).
* **Crear audiencias**: Este widget le dirige al Generador de segmentos en la interfaz de usuario. Utilice el Generador de segmentos para interactuar con los elementos de datos de perfil y definir los criterios de la definición del segmento. Seleccione **[!UICONTROL Crear audiencia]** para navegar al Generador de segmentos. Para obtener más información, lea la [Descripción general del servicio de segmentación](../segmentation/home.md).
* **Enviar datos a destinos**: Este widget le dirige al catálogo de destinos. Utilice el catálogo de destinos para seleccionar un destino al que pueda conectarse y enviar audiencias. Seleccione **[!UICONTROL Configurar destinos]** para navegar al catálogo de destinos. Para obtener más información, lea la [Información general de destinos](../destinations/home.md).

![Página de inicio de la interfaz de usuario de Experience Platform que muestra el widget de introducción](assets/platform-home/getting-started-widget.png)

## Panel de métricas {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Recuento total de perfiles"
>abstract="El número total de perfiles que su organización tiene en Experience Platform. Este recuento se basa en la política de combinación de su organización y no incluye fragmentos de perfiles. El número de perfiles se actualiza una vez cada 24 horas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=es#profile-count" text="Obtenga más información en la documentación"

El panel de métricas muestra información actualizada sobre los datos de Experience Platform. El tablero se divide en dos secciones:

### La tabla de clasificación

La tabla de clasificación muestra el número total actual de esquemas, conjuntos de datos, perfiles y audiencias en su organización, así como su fecha de actualización más reciente.

![La sección de la tabla de clasificación de la página principal de la interfaz de usuario de Experience Platform.](assets/platform-home/leaderboard.png)

* **Esquemas totales**: El contador **Esquemas totales** muestra el número de esquemas del sistema. Este contador se actualiza cuando se crea un esquema. Para obtener más información, lea la [descripción general de esquemas](../xdm/home.md).
* **Conjuntos de datos totales**: El contador **Conjuntos de datos totales** muestra el número de conjuntos de datos en el sistema y la cantidad de datos en Experience Platform. Este contador se actualiza cuando se crea un conjunto de datos. Para obtener más información sobre los conjuntos de datos, lea la [descripción general de los conjuntos de datos](../catalog/datasets/overview.md).
* **Perfiles totales**: El recuento de **Perfiles** muestra el número total de perfiles que su organización tiene en Experience Platform. No incluye fragmentos de perfil. Esta es su audiencia total a la que puede dirigirse. Este recuento utiliza la [política de combinación](profile/merge-policies.md) predeterminada, tal como se establece en la configuración de la política de combinación en el Perfil del cliente en tiempo real. El número de perfiles se actualiza una vez cada 24 horas. Seleccione **[!UICONTROL Perfiles]** para navegar a la página Información general de Perfiles y ver todas las métricas de Perfil. Para obtener más información sobre los perfiles, lea la [Descripción general del perfil del cliente en tiempo real](../profile/home.md).
* **Audiencias totales**: El contador **Audiencias totales** muestra la cantidad total de audiencias creadas para su organización. Este número se actualiza cuando se crean nuevas audiencias. Para obtener más información sobre las audiencias, lea la [Descripción general del servicio de segmentación](../segmentation/home.md).

### Elementos recientes

Elementos recientes enumera los cambios más recientes realizados en su organización. En el ejemplo siguiente, los cambios más recientes pertenecen a conjuntos de datos, fuentes, audiencias y destinos.

![La sección de elementos recientes de la página principal de la interfaz de usuario de Experience Platform.](assets/platform-home/recent-items.png)

* **Conjuntos de datos recientes**: la tarjeta **[!UICONTROL Conjuntos de datos recientes]** muestra los cinco conjuntos de datos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo conjunto de datos. Seleccione un conjunto de datos para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todos]** para ver una lista de conjuntos de datos. Desde allí, puede seleccionar una fuente específica para obtener más información. Para obtener más información sobre los conjuntos de datos, consulte la [descripción general de los conjuntos de datos](../catalog/datasets/overview.md).
* **Fuentes recientes**: La tarjeta de métrica **[!UICONTROL Fuentes recientes]** muestra las cinco fuentes más recientes creadas dentro de la organización. Esta lista se actualiza cuando se crea un nuevo origen. Seleccione un origen para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todos]** para ver una lista de orígenes. Desde allí, puede seleccionar una fuente específica para obtener más información. Para obtener más información sobre las fuentes, consulte [Resumen de fuentes](../sources/home.md).
* **Audiencias recientes**: La tarjeta de métrica **[!UICONTROL Audiencias recientes]** muestra las cinco audiencias más recientes creadas dentro de la organización. Esta lista se actualiza cuando se crea una audiencia nueva. Seleccione una audiencia para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todas]** para ver una lista de audiencias. Para obtener más información sobre las audiencias, consulte [Resumen del servicio de segmentación](../segmentation/home.md).
* **Destinos recientes**: la tarjeta de métrica **[!UICONTROL Destinos recientes]** muestra los cinco destinos más recientes creados dentro de la organización. Esta lista se actualiza cuando se crea un nuevo destino. Seleccione un destino para ver los detalles de ese elemento o seleccione **[!UICONTROL Ver todos]** para ver una lista de destinos. Para obtener más información, lea la [Información general de destinos](../destinations/home.md).

## Recursos

Por último, el widget de recursos le proporciona recursos de documentación adicionales a los que puede hacer referencia. Se incluyen:

![La sección de recursos de la página principal de la interfaz de usuario de Experience Platform.](assets/platform-home/resources.png)

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
