---
title: Información general del panel de monitorización
description: Aprenda a utilizar el tablero de monitorización en la interfaz de usuario de Adobe Experience Platform
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Información general del panel de monitorización

Utilice el panel de monitorización de la interfaz de usuario de Adobe Experience Platform para ver el recorrido de los datos desde la ingesta hasta la activación. Con el panel de monitorización, puede:

* Monitorice el recorrido de los datos desde Orígenes, Servicio de identidad, Perfil del cliente en tiempo real, Audiencias y, finalmente, en Destinos.
* Ver diferentes métricas y estados según la fase en la que se encuentren los datos.
* Filtre la vista de monitorización de datos por tipo de datos.

El panel de monitorización admite la vista de varios tipos de datos diferentes:

* **Cliente y cuenta**: los datos del cliente hacen referencia a los datos utilizados en [Real-time Customer Data Platform](../../rtcdp/home.md), mientras que los datos de la cuenta hacen referencia a [datos de perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) a los que se puede acceder cuando se suscribe a [Real-Time CDP, B2B Edition](../../rtcdp/b2b-overview.md). Si la licencia de Real-Time CDP no incluye Real-Time CDP, edición B2B, solo puede utilizar el panel de monitorización para monitorizar los datos de los clientes.
* **Candidato**: [Los perfiles de cliente potencial](../../profile/ui/prospect-profile.md) se utilizan para representar a personas que aún no han participado en su compañía pero a las que desea ponerse en contacto. Con los perfiles de clientes potenciales, puede complementar los perfiles de sus clientes con atributos de socios de terceros de confianza. Debe tener una licencia de Real-Time CDP (servicio de aplicaciones), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate para ver el tipo de datos del cliente potencial.
* **Enriquecimiento del perfil de cuenta**: los perfiles de cuenta permiten unificar la información de cuenta de varias fuentes. Debe tener licencia de Real-Time CDP, edición B2B, para monitorizar los datos de enriquecimiento del perfil de cuenta.

Lea este documento para aprender a utilizar el panel de monitorización para monitorizar el recorrido de los datos en los distintos servicios de Experience Platform.

## Introducción 

Este documento requiere un entendimiento práctico de los siguientes componentes de Experience Platform:

* [Flujos de datos](../home.md): los flujos de datos son representaciones de trabajos de datos que mueven datos a través del Experience Platform. Puede utilizar el espacio de trabajo de fuentes para crear flujos de datos que introduzcan datos de una fuente determinada en el Experience Platform.
* [Fuentes](../../sources/home.md): Use fuentes en Experience Platform para introducir datos de una aplicación de Adobe o de una fuente de datos de terceros.
* [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Segmentación](../../segmentation/home.md): use el servicio de segmentación para crear segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real.
* [Destinos](../../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

## Guía del panel de monitorización

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Supervisión]** en [!UICONTROL Administración de datos] en el panel de navegación izquierdo.

![Panel de supervisión en la interfaz de usuario del Experience Platform.](../assets/ui/monitor-overview/monitoring.png)

Seleccione **[!UICONTROL Tipo de datos]** y, a continuación, utilice el menú desplegable para seleccionar el tipo de datos que desea ver. Las clases de esquema del Modelo de datos de experiencia (XDM) definen los tipos de datos para garantizar que sus datos sigan un formato estándar cuando se incorporan en Experience Platform. Para obtener más información, consulte la siguiente documentación:

* [Tipo de datos de cuenta B2B](../../rtcdp/b2b-tutorial.md)
* [Tipo de datos del cliente potencial](../../rtcdp/partner-data/prospecting.md)

Puede filtrar la vista en función de los siguientes tipos de datos:

>[!BEGINTABS]

>[!TAB Todos]

Seleccione **[!UICONTROL Todos]** para actualizar el tablero y mostrar las métricas de todos los datos que se han introducido en Experience Platform durante un período determinado.

![El tipo de datos de supervisión establecido en &quot;Todos&quot;.](../assets/ui/monitor-overview/all.png)

>[!TAB Cliente y cuenta]

Seleccione **[!UICONTROL Cliente y cuenta]** para actualizar su tablero y mostrar métricas con los datos de cliente y cuenta que se han introducido en Experience Platform durante un período determinado.

![El tipo de datos de supervisión establecido en Cliente y cuenta.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB Candidato]

Seleccione **[!UICONTROL Candidato]** para actualizar el tablero y mostrar las métricas de los datos de prospección que se han introducido en el Experience Platform durante un período determinado. **Nota**: solo puede ver actividades de tipo de datos de clientes potenciales si tiene [derecho a recibir datos de clientes potenciales](../../rtcdp/partner-data/prospecting.md).

![El tipo de datos de supervisión establecido en &quot;Cliente potencial&quot;.](../assets/ui/monitor-overview/prospect.png)

>[!TAB Enriquecimiento del perfil de la cuenta]

Seleccione **[!UICONTROL Enriquecimiento del perfil de cuenta]** para actualizar su tablero y mostrar métricas sobre los datos de enriquecimiento del perfil. **Nota**: solo puedes ver las métricas de enriquecimiento de perfil de cuenta si tienes derecho a [datos B2B](../../rtcdp/b2b-tutorial.md).

![El tipo de datos de supervisión establecido en &quot;Enriquecimiento del perfil de cuenta&quot;.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Utilice el encabezado superior del panel para una experiencia de monitorización entre servicios. Puede filtrar la vista de métricas y gráficos seleccionando la tarjeta de funciones que elija en el encabezado de la categoría de datos.

>[!BEGINTABS]

>[!TAB Fuentes]

Seleccione **[!UICONTROL Fuentes]** para ver las métricas de su tasa de ingesta de fuentes. Lea la guía sobre [datos de fuentes de supervisión](monitor-sources.md) para obtener más información.

![Panel de supervisión en la interfaz de usuario con la tarjeta de orígenes seleccionada.](../assets/ui/monitor-overview/sources.png)

>[!TAB Identidades]

Seleccione **[!UICONTROL Identidades]** para ver la tasa de éxito de procesamiento de sus datos de identidad. Lea la guía sobre [supervisión de datos de identidad](monitor-identities.md) para obtener más información.

![Panel de supervisión en la interfaz de usuario con la tarjeta de identidades seleccionada.](../assets/ui/monitor-overview/identities.png)

>[!TAB Perfiles]

Seleccione **[!UICONTROL Perfiles]** para ver la tasa de éxito de procesamiento de sus datos de perfil. Lea la guía sobre [supervisión de datos de perfil](monitor-profiles.md) para obtener más información.

![Panel de supervisión en la interfaz de usuario con la tarjeta de perfiles seleccionada.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Públicos]

Seleccione **[!UICONTROL Audiencias]** para ver las métricas de sus audiencias y trabajos de segmentación. Lea la guía de [supervisión de datos de audiencia](monitor-audiences.md) para obtener más información.

![Panel de supervisión en la interfaz de usuario con la tarjeta de audiencias seleccionada.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Destinos]

Seleccione **[!UICONTROL Destinos]** para ver las métricas de su [!UICONTROL tasa de activación de transmisión] y [!UICONTROL ejecuciones de flujo de datos con errores por lotes]. Lea la guía sobre [supervisión de datos de destinos](monitor-destinations.md) para obtener más información.

![Panel de supervisión en la interfaz de usuario con la tarjeta de destinos seleccionada.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Configurar intervalo de tiempo de monitorización {#configure-monitoring-time-frame}

De forma predeterminada, el panel de monitorización muestra métricas de datos introducidos en las últimas 24 horas. Para actualizar el lapso de tiempo, seleccione **[!UICONTROL Últimas 24 horas]**.

![Panel de supervisión en la interfaz de usuario con la configuración de tiempo seleccionada.](../assets/ui/monitor-overview/select-time.png)

Puede configurar un nuevo lapso de tiempo para la vista de monitorización de datos en el cuadro de diálogo que aparece. Tiene la opción de crear un lapso de tiempo personalizado o seleccionar en la lista de opciones preconfiguradas:

* [!UICONTROL Últimas 24 horas]
* [!UICONTROL Últimos 7 días]
* [!UICONTROL Últimos 30 días]

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![Ventana emergente de configuración del lapso de tiempo en el panel de supervisión.](../assets/ui/monitor-overview/update-time.png)

## Pasos siguientes

Al leer este documento, ahora puede navegar por el panel de monitorización de la interfaz de usuario. Para obtener información sobre cómo monitorizar los datos de un servicio de Experience Platform específico, lea la siguiente documentación:

* [Supervisar datos de origen](monitor-sources.md).
* [Supervisar datos de identidad](monitor-identities.md).
* [Supervisar datos de perfil](monitor-profiles.md).
* [Supervisar datos de audiencia](monitor-audiences.md).
* [Supervisar datos de destinos](monitor-destinations.md).
