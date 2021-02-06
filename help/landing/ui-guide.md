---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía del usuario;guía del usuario;guía del usuario de la plataforma;guía del usuario de la plataforma;introducción a la plataforma;panel;
solution: Experience Platform
title: Información general sobre la interfaz de usuario de Experience Platform
topic: ui guide
description: 'Adobe Experience Platform '
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 1%

---


# Guía de la interfaz de usuario de Adobe Experience Platform

Esta guía sirve como introducción al uso de la interfaz de usuario (IU) de Adobe Experience Platform, explica para qué se utilizan los distintos componentes y proporciona vínculos a documentación adicional para obtener más información.

Para obtener más información sobre Adobe Experience Platform, lea la [información general del Experience Platform](home.md).

## Pantalla principal

Después de iniciar sesión en Adobe Experience Platform, se encuentra en la página [!UICONTROL Inicio], que consta de las secciones [panel de métricas](#metrics), [datos recientes](#recent-data) y [aprendizaje recomendado](#recommended-learning).

![](images/user-guide/homepage.png)

### Métricas

El panel de métricas proporciona tarjetas que le proporcionan información sobre conjuntos de datos, perfiles, segmentos y destinos dentro de su organización.

![](images/user-guide/homepage-dashboard.png)

La sección **[!UICONTROL Datasets]** muestra la cantidad de datasets dentro de la organización de IMS. Este número se actualiza cuando se crea un nuevo conjunto de datos. Encontrará más información sobre los conjuntos de datos en la [información general de los conjuntos de datos](../catalog/datasets/overview.md).

La sección **[!UICONTROL Perfiles]** muestra el número total de personas con perfiles dentro de la organización de IMS, excluyendo los fragmentos de perfil. Este número total de personas representa la audiencia direccionable total y se actualiza una vez cada 24 horas. Encontrará más información sobre perfiles en la [información general del Perfil del cliente en tiempo real](../profile/home.md).

La sección **[!UICONTROL Segmentos]** muestra el número total de segmentos creados dentro de la organización de IMS. Este número se actualiza cuando se crea un nuevo segmento. Encontrará más información sobre los segmentos en la [información general del servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Destinos]** muestra el número total de destinos creados para la organización de IMS. Este número se actualiza cuando se crea un nuevo destino. Encontrará más información sobre los destinos en la [información general de destinos](../destinations/home.md).

### Datos recientes

El panel de datos reciente proporciona información sobre conjuntos de datos, fuentes, segmentos y destinos creados recientemente.

![](images/user-guide/homepage-recent.png)

La sección **[!UICONTROL datasets recientes]** lista los cinco datasets creados más recientemente dentro de la organización de IMS. Esta lista se actualiza cada vez que se crea un nuevo conjunto de datos. Puede seleccionar un conjunto de datos de la lista para obtener más información sobre el conjunto de datos especificado o seleccionar **[!UICONTROL Vista de todo]** para ver una lista de todos los conjuntos de datos creados. Encontrará más información sobre los conjuntos de datos en la [información general de los conjuntos de datos](../catalog/datasets/overview.md).

La sección **[!UICONTROL Fuentes recientes]** lista los cinco conectores de origen creados más recientemente dentro de la organización de IMS. Esta lista se actualiza cada vez que se crea un nuevo conector de origen. Puede seleccionar una conexión de origen de la lista a la vista para obtener más información sobre el conector especificado o seleccionar **[!UICONTROL Vista de todo]** para ver una lista de todas las conexiones de origen creadas. Encontrará más información sobre las fuentes en la [información general de las fuentes](../sources/home.md).

La sección **[!UICONTROL Segmentos recientes]** lista las cinco definiciones de segmentos creados más recientemente dentro de la organización de IMS. Esta lista se actualiza cada vez que se crea una nueva definición de segmento. Puede seleccionar una definición de segmento de la lista para obtener más información sobre la definición de segmento especificada o seleccionar **[!UICONTROL Vista de todo]** para ver una lista de todas las definiciones de segmento creadas. Encontrará más información sobre los segmentos en la [información general del servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Destinos recientes]** lista los cinco destinos creados más recientemente dentro de la organización de IMS. Esta lista se actualiza cada vez que se crea un nuevo destino. Puede seleccionar un destino de la lista a la vista para obtener más información sobre el destino especificado o seleccionar **[!UICONTROL Vista de todo]** para ver una lista de todos los destinos creados. Encontrará más información sobre los destinos en la [información general de destinos](../destinations/home.md).

### Aprendizaje recomendado

La sección **[!UICONTROL Aprendizaje recomendado]** proporciona vínculos a documentación útil para comenzar con Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegación superior

La barra de navegación superior de la interfaz de usuario de la plataforma muestra la organización de IMS en la que ha iniciado sesión y proporciona varios controles importantes.

En el lado izquierdo de la barra de navegación está el logotipo de Adobe Experience Platform. Si selecciona esta opción en cualquier momento, volverá a la pantalla de inicio de la interfaz de usuario de la plataforma.

![](./images/user-guide/homepage-top-nav-bar.png)

### Mezclador de organización IMS

El primer elemento en la parte derecha de la barra de navegación superior es el **conmutador de organización IMS**.

![](./images/user-guide/homepage-ims-org.png)

Al seleccionar el conmutador, se abre un menú desplegable de las organizaciones de IMS a las que tiene acceso, si hay alguna disponible. Seleccione una opción de la lista para cambiar a esa organización de IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Cambiar aplicaciones

El siguiente elemento del lado derecho de la navegación superior es el **conmutador de aplicaciones**, representado por el icono ![conmutador de aplicaciones](./images/user-guide/app-switcher-icon.png). Al seleccionar este icono, puede cambiar entre las aplicaciones de Adobe a las que tiene acceso su organización de IMS, como Experience Platform, Analytics, Assets e Launch.

### Ayuda

A la derecha del conmutador de aplicaciones se encuentra el **menú de ayuda y soporte**, que está representado por el icono ![signo de interrogación/ayuda](./images/user-guide/help-icon.png). Al seleccionar este icono, aparece un menú emergente que contiene varios recursos de ayuda y asistencia. La ficha **[!UICONTROL Ayuda]** muestra una lista de la documentación relevante para la página en la que se encuentra actualmente. La ficha **[!UICONTROL Soporte]** le permite crear un ticket de soporte técnico con el equipo de soporte de Adobe. La ficha **[!UICONTROL Comentarios]** permite enviar comentarios sobre la plataforma a Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificaciones y anuncios

En la sección **notificaciones**, que está representada por el icono ![campana/notificaciones y anuncios](images/user-guide/notification-icon.png). La ficha **[!UICONTROL Notificaciones]** muestra información importante sobre el producto y otras actualizaciones relevantes, mientras que la ficha **[!UICONTROL Anuncios]** muestra información sobre el mantenimiento del servicio.

### Perfil del usuario

El último elemento de la barra de navegación superior es la **configuración de usuario**, que se representa mediante el icono ![configuración de usuario/Perfil de usuario](images/user-guide/profile-icon.png). Seleccione este icono para editar sus preferencias o cerrar sesión.

### Sandboxes

Inmediatamente debajo de la barra de navegación superior se encuentra la barra del simulador de pruebas. Esta barra muestra el simulador para pruebas que está utilizando actualmente para la plataforma. Encontrará más información sobre los entornos limitados en la [información general de los entornos limitados](../sandboxes/home.md).

## Navegación izquierda {#left-nav}

La navegación de la parte izquierda de la pantalla lista todos los diferentes servicios admitidos en la interfaz de usuario de la plataforma.

>[!IMPORTANT]
>
>Es posible que algunas secciones de la barra de navegación izquierda no aparezcan o estén atenuadas. Esto se debe a que no tiene acceso a esas funciones. Si cree que debería tener acceso a estas secciones, póngase en contacto con el administrador del sistema.

![](images/user-guide/homepage-left.png)

La sección **[!UICONTROL Inicio]** permite volver a la página principal de la interfaz de usuario de la plataforma.

La sección **[!UICONTROL Flujos de trabajo]** muestra una lista de flujos de trabajo de varios pasos para realizar operaciones dentro de la plataforma. Encontrará más información sobre flujos de trabajo en la [información general de flujos de trabajo](./workflows.md).

### [!UICONTROL Conexiones]

La sección **[!UICONTROL Fuentes]** permite crear, actualizar y eliminar conexiones de origen, lo que permite ingerir datos de fuentes externas en la plataforma. Encontrará más información sobre las fuentes en la [información general de las fuentes](../sources/home.md).

La sección **[!UICONTROL Destinos]** le permite crear, actualizar y eliminar destinos, lo que le permite exportar datos de Platform a muchos destinos externos. Encontrará más información sobre los destinos en la [información general de destinos](../destinations/home.md).

### [!UICONTROL Cliente]

La sección **[!UICONTROL Perfiles]** permite examinar perfiles de clientes, métricas de perfiles de vista, crear y administrar políticas de combinación y esquemas de unión de vistas. Para obtener más información sobre el uso de la sección [!UICONTROL Perfiles], lea la [[!DNL Profile] guía del usuario](../profile/ui/user-guide.md). Encontrará más información sobre el Perfil del cliente en tiempo real en la [información general del Perfil del cliente en tiempo real](../profile/home.md).

La sección **[!UICONTROL Segmentos]** permite crear y administrar definiciones de segmentos. Para obtener más información sobre el uso de la sección [!UICONTROL Segmentos], lea la [guía del usuario de segmentación](../segmentation/ui/overview.md). Encontrará más información sobre el servicio de segmentación en la [información general del servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Identidades]** permite crear y administrar Áreas de nombres de identidad. Para obtener más información sobre la sección [!UICONTROL Identidades], incluida información sobre Áreas de nombres de identidad y cómo utilizar identidades en la interfaz de usuario de la plataforma, consulte la [información general de la Área de nombres de identidad](../identity-service/namespaces.md).

### [!UICONTROL Privacidad]

La sección **[!UICONTROL Directivas]** permite crear y administrar políticas de uso de datos. Para obtener más información sobre el uso de la sección Directivas, lea la [guía del usuario de directivas de uso de datos](../data-governance/policies/user-guide.md). Encontrará más información sobre las políticas de uso de datos en la [información general de las directivas de uso de datos](../data-governance/policies/overview.md).

La sección **[!UICONTROL Solicitudes]** permite crear y administrar solicitudes de privacidad. Tenga en cuenta que debe estar incluido en la lista de permitidos para tener acceso a la interfaz de usuario del Privacy Service. Para obtener más información sobre el uso de la sección Solicitudes, lea la [guía del usuario del Privacy Service](../privacy-service/ui/user-guide.md). Encontrará más información sobre Privacy Service en la [información general del Privacy Service](../privacy-service/home.md).

### [!UICONTROL Ciencia de datos]

La sección **[!UICONTROL Equipos portátiles]** proporciona acceso a JupyterLab, un entorno de desarrollo interactivo que le permite explorar, analizar y modelar sus datos. Para obtener más información sobre el uso de la sección Equipos portátiles, lea la [guía del usuario de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Encontrará más información sobre el área de trabajo de ciencias de datos en la [información general del área de trabajo de ciencias de datos](../data-science-workspace/home.md)

La sección **[!UICONTROL Modelos]** permite aprovechar el aprendizaje automático y la inteligencia artificial para crear, desarrollar, entrenar y ajustar modelos para hacer predicciones. Encontrará más información sobre la sección Modelos en el tutorial sobre [formación y evaluación de un modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La sección **[!UICONTROL Servicios]** le permite administrar los modelos publicados para la capacitación y la puntuación programadas, o aprovechar los servicios inteligentes de Adobe, un conjunto de servicios de inteligencia artificial que ofrecen experiencias personalizadas en tiempo real. Encontrará más información sobre la sección Servicios en [Publicación de un modelo como un tutorial de servicio](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Gestión de datos]

La sección **[!UICONTROL Esquemas]** permite crear y administrar esquemas del modelo de datos de experiencia (XDM). Para obtener más información sobre esquemas, lea el tutorial sobre [creación de un esquema](../xdm/tutorials/create-schema-ui.md). Encontrará más información sobre XDM en la [información general del sistema XDM](../xdm/home.md).

La sección **[!UICONTROL Conjuntos de datos]** permite crear y administrar conjuntos de datos. Encontrará más información sobre los conjuntos de datos en la [guía del usuario de conjuntos de datos](../catalog/datasets/user-guide.md).

La sección **[!UICONTROL Consultas]** permite crear y administrar consultas, registrar consultas SQL realizadas por el servicio de Consulta de Adobe Experience Platform y vista las credenciales PostgreSQL. Encontrará más información sobre consultas en la [guía del usuario del servicio de Consulta](../query-service/ui/overview.md).

La sección **[!UICONTROL Monitoreo]** permite monitorear la ingestión por lotes y por flujo continuo. Encontrará más información sobre la supervisión en la [guía del usuario para la ingestión de datos de monitoreo](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisión]

Offer Decisioning es un servicio de aplicaciones integrado con Adobe Experience Platform. Le permite aprovechar al Experience Platform para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto en el momento adecuado. Para obtener más información sobre Offer Decisioning, incluido el trabajo con [!UICONTROL Ofertas] y [!UICONTROL Actividades], visite la [documentación de Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

La interfaz de usuario de la plataforma (IU) proporciona un panel mediante el cual puede realizar vistas de información importante sobre el uso de licencias de su organización, tal como se obtiene durante una instantánea diaria. Para acceder a esto, seleccione **[!UICONTROL Uso de licencias]** en la navegación. Para obtener más información sobre el panel de uso de licencias, visite la [guía de paneles de uso de licencias](license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funcionalidad de panel de uso de licencias está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Pasos siguientes

Al leer esta guía, ahora se le ha presentado a la página de inicio y a los principales elementos de navegación de la interfaz de usuario de la plataforma. Para obtener información más detallada sobre cómo trabajar en la interfaz de usuario, consulte la documentación de cada servicio de plataforma individual. Los vínculos a esta documentación se proporcionan en la sección [navegación izquierda](#left-nav) que se encuentra anteriormente en este documento.