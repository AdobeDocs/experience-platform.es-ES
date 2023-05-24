---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía del usuario;guía de la interfaz de usuario;guía de la interfaz de usuario de platform;introducción a platform;tablero;
solution: Experience Platform
title: Información general de IU de Experience Platform
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Guía de IU de Adobe Experience Platform

Esta guía sirve como introducción al uso de la interfaz de usuario (IU) de Adobe Experience Platform, donde se explica para qué se utilizan los distintos componentes y se proporcionan vínculos a documentación adicional para obtener más información.

Para obtener más información sobre Adobe Experience Platform, lea la [Introducción al Experience Platform](home.md).

## Pantalla principal

Después de iniciar sesión en Adobe Experience Platform, está en la [!UICONTROL Inicio] , que consta de la página [panel de métricas](#metrics), [datos recientes](#recent-data), y [aprendizaje recomendado](#recommended-learning) secciones.

![](images/user-guide/homepage.png)

### Métricas

El panel de métricas proporciona tarjetas que le proporcionan información sobre conjuntos de datos, perfiles, segmentos y destinos dentro de su organización.

![](images/user-guide/homepage-dashboard.png)

El **[!UICONTROL Conjuntos de datos]** Esta sección muestra el número de conjuntos de datos dentro de su organización. Este número se actualiza cuando se crea un nuevo conjunto de datos. Encontrará más información sobre los conjuntos de datos en la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

El **[!UICONTROL Perfiles]** Esta sección muestra el número total de personas con perfiles dentro de la organización, excluidos los fragmentos de perfil. Este número total de personas representa la audiencia total a la que se puede dirigir y se actualiza una vez cada 24 horas. Encontrará más información sobre los perfiles en la [Resumen del perfil del cliente en tiempo real](../profile/home.md).

El **[!UICONTROL Segmentos]** Esta sección muestra la cantidad total de segmentos creados dentro de su organización. Este número se actualiza cuando se crea un nuevo segmento. Encontrará más información sobre los segmentos en la [Resumen del servicio de segmentación](../segmentation/home.md).

El **[!UICONTROL Destinos]** Esta sección muestra el número total de destinos creados para la organización. Este número se actualiza cuando se crea un nuevo destino. Encontrará más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### Datos recientes

El panel de datos recientes proporciona información sobre conjuntos de datos, fuentes, segmentos y destinos creados recientemente.

![](images/user-guide/homepage-recent.png)

El **[!UICONTROL Conjuntos de datos recientes]** Esta sección enumera los cinco conjuntos de datos creados más recientemente dentro de su organización. Esta lista se actualiza cada vez que se crea un nuevo conjunto de datos. Puede seleccionar un conjunto de datos de la lista para ver más información sobre el conjunto de datos especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todos los conjuntos de datos creados. Encontrará más información sobre los conjuntos de datos en la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

El **[!UICONTROL Fuentes recientes]** Esta sección enumera los cinco conectores de origen creados más recientemente dentro de su organización. Esta lista se actualiza cada vez que se crea un nuevo conector de origen. Puede seleccionar una conexión de origen de la lista para ver más información acerca del conector especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todas las conexiones de origen creadas. Encontrará más información sobre las fuentes en la [información general de orígenes](../sources/home.md).

El **[!UICONTROL Segmentos recientes]** En esta sección se enumeran las cinco definiciones de segmentos creadas más recientemente en su organización. Esta lista se actualiza cada vez que se crea una nueva definición de segmento. Puede seleccionar una definición de segmento de la lista para ver más información sobre la definición de segmento especificada o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todas las definiciones de segmentos creadas. Encontrará más información sobre los segmentos en la [Resumen del servicio de segmentación](../segmentation/home.md).

El **[!UICONTROL Destinos recientes]** Esta sección enumera los cinco destinos creados más recientemente dentro de su organización. Esta lista se actualiza cada vez que se crea un nuevo destino. Puede seleccionar un destino de la lista para ver más información sobre el destino especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todos los destinos creados. Encontrará más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### Aprendizaje recomendado

El **[!UICONTROL Aprendizaje recomendado]** proporciona vínculos a documentación útil para empezar a utilizar Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegación superior

La barra de navegación superior de la IU de Platform muestra la organización en la que está conectado actualmente y proporciona varios controles importantes.

En el lado izquierdo de la barra de navegación se encuentra el logotipo de Adobe Experience Platform. Al seleccionar este logotipo en cualquier momento, volverá a la pantalla de inicio de la IU de Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Conmutador de organización

El primer elemento a la derecha de la barra de navegación superior es el **Conmutador de organización**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Al seleccionar el conmutador, se abre un menú desplegable de organizaciones a las que tiene acceso, si hay alguna disponible. Para cambiar a otra organización, seleccione una opción de la lista.

### Cambiar aplicaciones

El siguiente elemento a la derecha de la navegación superior es el **conmutador de aplicaciones**, representado por el ![conmutador de aplicaciones](./images/user-guide/app-switcher-icon.png) icono. Al seleccionar este icono, puede cambiar entre las aplicaciones de Adobe a las que su organización tiene acceso, como Experience Platform, Analytics, Assets y otras.

### Ayuda

A la derecha del conmutador de aplicaciones se encuentra el **menú ayuda y asistencia**, que está representado por el ![signo de interrogación/ayuda](./images/user-guide/help-icon.png) icono. Al seleccionar este icono, aparece un menú emergente con varios recursos de ayuda y asistencia. El **[!UICONTROL Ayuda]** Esta pestaña muestra una lista de la documentación relevante para la página en la que se encuentra actualmente. El **[!UICONTROL Asistencia]** le permite crear un vale de soporte con el equipo de soporte de Adobe. El **[!UICONTROL Comentarios]** permite enviar comentarios sobre Platform al Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificaciones y anuncios

En el **sección de notificaciones**, que está representado por el ![campana/notificaciones y anuncios](images/user-guide/notification-icon.png) icono. El **[!UICONTROL Notificaciones]** La pestaña muestra información importante sobre el producto y otras actualizaciones relevantes, mientras que la **[!UICONTROL Anuncios]** La pestaña muestra información sobre el mantenimiento del servicio.

### Perfil de usuario

El elemento final de la barra de navegación superior es el **configuración de usuario**, representado por el ![configuración de usuario/Perfil de usuario](images/user-guide/profile-icon.png) icono. Seleccione este icono para editar sus preferencias o cerrar la sesión.

Puede alternar entre el tema claro y oscuro de la interfaz de Platform con el interruptor situado justo debajo de su nombre y correo electrónico. Seleccione el tema que prefiera.

![](images/theme.png)

### Zonas protegidas

Inmediatamente debajo de la barra de navegación superior está la barra de zona protegida. Esta barra muestra qué zona protegida está utilizando actualmente para Platform. Encontrará más información sobre las zonas protegidas en la [información general sobre zonas protegidas](../sandboxes/home.md).

## Navegación izquierda {#left-nav}

La navegación en la parte izquierda de la pantalla enumera todos los diferentes servicios admitidos en la IU de Platform.

Haga clic en el icono de menú para mostrar u ocultar el panel de navegación izquierdo.

![](images/user-guide/hidemenu.png)

Puede bloquear la navegación en la posición de apertura haciendo clic de nuevo después de mostrar el panel.

>[!IMPORTANT]
>
>La barra de navegación izquierda muestra únicamente las funciones a las que puede acceder. En versiones anteriores de Adobe Experience Platform, se deshabilitaban los elementos no disponibles. Si cree que debería tener acceso a una sección que no aparece, póngase en contacto con el administrador del sistema.

![](images/user-guide/homepage-left.png)

El **[!UICONTROL Inicio]** Esta sección le permite volver a la página principal de la IU de Platform.

El **[!UICONTROL Flujos de trabajo]** Esta sección muestra una lista de flujos de trabajo de varios pasos para realizar operaciones en Platform. Encontrará más información sobre los flujos de trabajo en la [información general sobre flujos de trabajo](./workflows.md).

### [!UICONTROL Conexiones]

El **[!UICONTROL Fuentes]** Esta sección permite crear, actualizar y eliminar conexiones de origen, lo que permite introducir datos de fuentes externas en Platform. Encontrará más información sobre las fuentes en la [información general de orígenes](../sources/home.md).

El **[!UICONTROL Destinos]** Esta sección permite crear, actualizar y eliminar destinos, lo que permite exportar datos de Platform a muchos destinos externos. Encontrará más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### [!UICONTROL Cliente]

El **[!UICONTROL Perfiles]** Esta sección permite examinar los perfiles de los clientes, ver las métricas de perfil, crear y administrar políticas de combinación y ver esquemas de unión. Para obtener más información sobre el uso de [!UICONTROL Perfiles] , lea la sección [[!DNL Profile] guía del usuario](../profile/ui/user-guide.md). Puede encontrar más información sobre el perfil del cliente en tiempo real en la [Resumen del perfil del cliente en tiempo real](../profile/home.md).

El **[!UICONTROL Segmentos]** Esta sección le permite crear y gestionar definiciones de segmentos. Para obtener más información sobre el uso de [!UICONTROL Segmentos] , lea la sección [guía del usuario de segmentación](../segmentation/ui/overview.md). Encontrará más información sobre el servicio de segmentación en la [Resumen del servicio de segmentación](../segmentation/home.md).

El **[!UICONTROL Identidades]** Esta sección permite crear y administrar áreas de nombres de identidad. Para obtener más información sobre [!UICONTROL Identidades] Esta sección, que incluye información sobre áreas de nombres de identidad y cómo utilizar identidades en la interfaz de usuario de Platform, consulte la [información general del área de nombres de identidad](../identity-service/namespaces.md).

### [!UICONTROL Privacidad]

El **[!UICONTROL Políticas]** Esta sección permite crear y administrar las políticas de uso de datos. Para obtener más información sobre el uso de la sección Políticas, lea la [guía del usuario sobre políticas de uso de datos](../data-governance/policies/user-guide.md). Encontrará más información sobre las políticas de uso de datos en la [información general sobre políticas de uso de datos](../data-governance/policies/overview.md).

El **[!UICONTROL Solicitudes]** Esta sección permite crear y administrar solicitudes de privacidad. Tenga en cuenta que debe estar incluido en la lista de permitidos para tener acceso a la interfaz de usuario de Privacy Service. Para obtener más información sobre el uso de la sección Solicitudes, lea la [Guía del usuario del Privacy Service](../privacy-service/ui/user-guide.md). Encontrará más información sobre Privacy Service en la [Introducción al Privacy Service](../privacy-service/home.md).

### [!UICONTROL Ciencia de datos]

El **[!UICONTROL Notebooks]** proporciona acceso a JupyterLab, un entorno de desarrollo interactivo que le permite explorar, analizar y modelar sus datos. Para obtener más información sobre el uso de la sección Notebooks, lea la [Guía del usuario de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Encontrará más información sobre Data Science Workspace en la [Resumen de Data Science Workspace](../data-science-workspace/home.md)

El **[!UICONTROL Modelos]** Esta sección permite utilizar el aprendizaje automático y la inteligencia artificial para crear, desarrollar, entrenar y ajustar modelos para hacer predicciones. Encontrará más información sobre la sección Modelos en el tutorial sobre [formación y evaluación de un modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

El **[!UICONTROL Servicios]** Esta sección le permite administrar los modelos publicados para la formación y puntuación programadas, o utilizar los servicios inteligentes de Adobe, un conjunto de servicios de IA que ofrecen experiencias del cliente personalizadas en tiempo real. Encontrará más información sobre la sección Servicios en la [Tutorial de publicación de un modelo como servicio](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Administración de datos]

El **[!UICONTROL Esquemas]** Esta sección permite crear y administrar esquemas del Modelo de datos de experiencia (XDM). Para obtener más información sobre los esquemas, lea el tutorial sobre [creación de un esquema](../xdm/tutorials/create-schema-ui.md). Encontrará más información sobre XDM en la [Información general del sistema XDM](../xdm/home.md).

El **[!UICONTROL Conjuntos de datos]** Esta sección permite crear y administrar conjuntos de datos. Encontrará más información sobre los conjuntos de datos en la [guía del usuario de conjuntos de datos](../catalog/datasets/user-guide.md).

El **[!UICONTROL Consultas]** Esta sección permite crear y administrar consultas, registrar consultas SQL realizadas por el servicio de consultas de Adobe Experience Platform y ver su [!DNL PostgreSQL] credenciales. Encontrará más información sobre las consultas en la [Guía del usuario del servicio de consultas](../query-service/ui/overview.md).

El **[!UICONTROL Monitorización]** Esta sección permite monitorizar la ingesta por lotes y de flujo continuo. Encontrará más información sobre la monitorización en la [guía del usuario de monitorización de ingesta de datos](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Adobe Journey Optimizer es un servicio de aplicaciones de Experience Platform. Le permite utilizar potentes tecnologías de toma de decisiones para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Para obtener más información acerca de Journey Optimizer, incluyendo cómo trabajar con [!UICONTROL Ofertas] y [!UICONTROL Actividades] visite la [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es).

### [!UICONTROL Administración]

La interfaz de usuario de Platform proporciona un panel a través del cual puede ver información importante acerca del uso de licencias de su organización, tal y como se captura durante una instantánea diaria. Acceda a este panel seleccionando **[!UICONTROL Uso de licencias]** en la navegación. Para obtener más información sobre el tablero de uso de licencias, visite la [guía del tablero de uso de licencias](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funcionalidad del tablero de uso de licencias está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Pasos siguientes

Al leer esta guía, se le ha presentado la página de inicio y los principales elementos de navegación de la interfaz de usuario de Platform. Para obtener información más detallada sobre cómo trabajar en la interfaz de usuario, consulte la documentación de cada servicio de Platform individual. Los vínculos a esta documentación se proporcionan en la [navegación izquierda](#left-nav) sección que se encuentra anteriormente en este documento.
