---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía del usuario;guía de la interfaz de usuario;guía de la interfaz de usuario de platform;introducción a platform;tablero;
solution: Experience Platform
title: Información general sobre la IU de Experience Platform
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 1%

---

# Guía de la interfaz de usuario de Adobe Experience Platform

Esta guía sirve como introducción al uso de la interfaz de usuario (IU) de Adobe Experience Platform, explica para qué se utilizan los distintos componentes y proporciona vínculos a documentación adicional para obtener más información.

Para obtener más información sobre Adobe Experience Platform, lea la [Información general del Experience Platform](home.md).

## Pantalla principal

Después de iniciar sesión en Adobe Experience Platform, se encuentra en la [!UICONTROL Página principal] que consta de la variable [panel de métricas](#metrics), [datos recientes](#recent-data)y [aprendizaje recomendado](#recommended-learning) secciones.

![](images/user-guide/homepage.png)

### Métricas

El tablero de métricas proporciona tarjetas que le proporcionan información sobre conjuntos de datos, perfiles, segmentos y destinos dentro de su organización.

![](images/user-guide/homepage-dashboard.png)

La variable **[!UICONTROL Conjuntos de datos]** muestra la cantidad de conjuntos de datos dentro de su organización de IMS. Este número se actualiza cuando se crea un nuevo conjunto de datos. Encontrará más información sobre los conjuntos de datos en la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

La variable **[!UICONTROL Perfiles]** muestra el número total de personas con perfiles dentro de su organización IMS, excluyendo los fragmentos de perfil. Este número total de personas representa la audiencia total a la que se puede dirigir y se actualiza una vez cada 24 horas. Puede encontrar más información sobre los perfiles en la sección [Resumen del perfil del cliente en tiempo real](../profile/home.md).

La variable **[!UICONTROL Segmentos]** muestra el número total de segmentos creados dentro de su organización de IMS. Este número se actualiza cuando se crea un nuevo segmento. Puede encontrar más información sobre los segmentos en la sección [Información general del servicio de segmentación](../segmentation/home.md).

La variable **[!UICONTROL Destinos]** muestra el número total de destinos creados para la organización IMS. Este número se actualiza cuando se crea un nuevo destino. Puede encontrar más información sobre los destinos en la sección [información general sobre destinos](../destinations/home.md).

### Datos recientes

El panel de datos reciente proporciona información sobre conjuntos de datos, fuentes, segmentos y destinos creados recientemente.

![](images/user-guide/homepage-recent.png)

La variable **[!UICONTROL Conjuntos de datos recientes]** lista los cinco conjuntos de datos creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo conjunto de datos. Puede seleccionar un conjunto de datos de la lista para ver más información sobre el conjunto de datos especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todos los conjuntos de datos creados. Encontrará más información sobre los conjuntos de datos en la [información general sobre conjuntos de datos](../catalog/datasets/overview.md).

La variable **[!UICONTROL Fuentes recientes]** lista los cinco conectores de origen creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo conector de origen. Puede seleccionar una conexión de origen de la lista para ver más información sobre el conector especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todas las conexiones de origen creadas. Puede encontrar más información sobre las fuentes en la sección [información general sobre fuentes](../sources/home.md).

La variable **[!UICONTROL Segmentos recientes]** lista las cinco definiciones de segmento creadas más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea una nueva definición de segmento. Puede seleccionar una definición de segmento de la lista para ver más información sobre la definición de segmento especificada o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todas las definiciones de segmento creadas. Puede encontrar más información sobre los segmentos en la sección [Información general del servicio de segmentación](../segmentation/home.md).

La variable **[!UICONTROL Destinos recientes]** lista los cinco destinos creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo destino. Puede seleccionar un destino de la lista para ver más información sobre el destino especificado o seleccionar **[!UICONTROL Ver todo]** para ver una lista de todos los destinos creados. Puede encontrar más información sobre los destinos en la sección [información general sobre destinos](../destinations/home.md).

### Aprendizaje recomendado

La variable **[!UICONTROL Aprendizaje recomendado]** proporciona vínculos a documentación útil para empezar a usar Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegación superior

La barra de navegación superior de la interfaz de usuario de Platform muestra la organización de IMS en la que ha iniciado sesión y proporciona varios controles importantes.

En el lado izquierdo de la barra de navegación está el logotipo de Adobe Experience Platform. Si selecciona este logotipo en cualquier momento, volverá a la pantalla de inicio de la interfaz de usuario de Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Conmutador de organización IMS

El primer elemento de la parte derecha de la barra de navegación superior es la **Conmutador de organización IMS**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Si selecciona el selector, se abre un menú desplegable de las organizaciones de IMS a las que tiene acceso, si hay alguna disponible. Para cambiar a otra organización de IMS, seleccione una opción de la lista.

### Cambiar aplicaciones

El siguiente elemento del lado derecho de la navegación superior es la **alternador de aplicaciones**, representada por el ![alternador de aplicaciones](./images/user-guide/app-switcher-icon.png) icono. Al seleccionar este icono, puede cambiar entre las aplicaciones de Adobe a las que tiene acceso su organización IMS, como Experience Platform, Analytics, Assets y otras.

### Ayuda

A la derecha del conmutador de aplicaciones se encuentra el **menú ayuda y asistencia**, que está representada por el ![signo de interrogación/ayuda](./images/user-guide/help-icon.png) icono. Al seleccionar este icono, aparece un menú emergente que contiene varios recursos de ayuda y asistencia. La variable **[!UICONTROL Ayuda]** muestra una lista de la documentación relevante para la página en la que se encuentra actualmente. La variable **[!UICONTROL Asistencia]** le permite crear un ticket de asistencia con el equipo de asistencia de Adobe. La variable **[!UICONTROL Comentarios]** permite enviar comentarios sobre Platform a Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificaciones y anuncios

En el **sección notificaciones**, que está representada por el ![campana/notificaciones y anuncios](images/user-guide/notification-icon.png) icono. La variable **[!UICONTROL Notificaciones]** muestra información importante sobre el producto y otras actualizaciones relevantes, mientras que la pestaña **[!UICONTROL Anuncios]** muestra información sobre el mantenimiento del servicio.

### Perfil de usuario

El último elemento de la barra de navegación superior es la **configuración de usuario**, representada por el ![configuración de usuario/Perfil de usuario](images/user-guide/profile-icon.png) icono. Seleccione este icono para editar sus preferencias o cerrar la sesión.

Puede alternar entre el tema claro y el oscuro de la interfaz de Platform con el conmutador ubicado justo debajo de su nombre y correo electrónico. Seleccione el tema que prefiera.

![](images/theme.png)

### Zonas protegidas

Inmediatamente debajo de la barra de navegación superior se encuentra la barra de entorno limitado. Esta barra muestra qué simulador de pruebas está utilizando para Platform. Encontrará más información sobre los entornos limitados en [información general sobre los entornos limitados](../sandboxes/home.md).

## Navegación izquierda {#left-nav}

La navegación de la parte izquierda de la pantalla enumera todos los servicios compatibles con la interfaz de usuario de Platform.

Haga clic en el icono de menú para mostrar u ocultar el panel de navegación izquierdo.

![](images/user-guide/hidemenu.png)

Puede bloquear la navegación en la posición de apertura haciendo clic de nuevo después de mostrar el panel.

>[!IMPORTANT]
>
>La barra de navegación izquierda muestra únicamente las funciones a las que puede acceder. En versiones anteriores de Adobe Experience Platform, los elementos no disponibles estaban desactivados. Si cree que debería tener acceso a una sección que no aparece, póngase en contacto con el administrador del sistema.

![](images/user-guide/homepage-left.png)

La variable **[!UICONTROL Página principal]** le permite volver a la página principal de la interfaz de usuario de Platform.

La variable **[!UICONTROL Flujos de trabajo]** muestra una lista de flujos de trabajo de varios pasos para realizar operaciones dentro de Platform. Puede encontrar más información sobre los flujos de trabajo en la sección [información general sobre flujos de trabajo](./workflows.md).

### [!UICONTROL Conexiones]

La variable **[!UICONTROL Fuentes]** permite crear, actualizar y eliminar conexiones de origen, lo que permite introducir datos de fuentes externas en Platform. Puede encontrar más información sobre las fuentes en la sección [información general sobre fuentes](../sources/home.md).

La variable **[!UICONTROL Destinos]** permite crear, actualizar y eliminar destinos, lo que permite exportar datos desde Platform a muchos destinos externos. Puede encontrar más información sobre los destinos en la sección [información general sobre destinos](../destinations/home.md).

### [!UICONTROL Cliente]

La variable **[!UICONTROL Perfiles]** permite examinar perfiles de clientes, ver métricas de perfil, crear y administrar políticas de combinación y ver esquemas de unión. Para obtener más información sobre el uso de la variable [!UICONTROL Perfiles] , lea la [[!DNL Profile] guía del usuario](../profile/ui/user-guide.md). Puede encontrar más información sobre el Perfil del cliente en tiempo real en la sección [Resumen del perfil del cliente en tiempo real](../profile/home.md).

La variable **[!UICONTROL Segmentos]** permite crear y administrar definiciones de segmentos. Para obtener más información sobre el uso de la variable [!UICONTROL Segmentos] , lea la [guía del usuario sobre segmentación](../segmentation/ui/overview.md). Puede encontrar más información sobre el servicio de segmentación en la sección [Información general del servicio de segmentación](../segmentation/home.md).

La variable **[!UICONTROL Identidades]** permite crear y administrar áreas de nombres de identidad. Para obtener más información sobre la variable [!UICONTROL Identidades] , incluida información sobre áreas de nombres de identidad y cómo usar identidades en la interfaz de usuario de Platform, consulte la sección [información general del área de nombres de identidad](../identity-service/namespaces.md).

### [!UICONTROL Privacidad]

La variable **[!UICONTROL Políticas]** permite crear y administrar políticas de uso de datos. Para obtener más información sobre el uso de la sección Directivas , lea la [guía del usuario sobre políticas de uso de datos](../data-governance/policies/user-guide.md). Puede encontrar más información sobre las políticas de uso de datos en la sección [información general sobre las políticas de uso de datos](../data-governance/policies/overview.md).

La variable **[!UICONTROL Solicitudes]** permite crear y administrar solicitudes de privacidad. Tenga en cuenta que debe estar incluido en la lista de permitidos para tener acceso a la IU del Privacy Service. Para obtener más información sobre el uso de la sección Solicitudes , lea la [Guía del usuario del Privacy Service](../privacy-service/ui/user-guide.md). Puede encontrar más información sobre el Privacy Service en la [Información general del Privacy Service](../privacy-service/home.md).

### [!UICONTROL Ciencia de datos]

La variable **[!UICONTROL Portátiles]** proporciona acceso a JupyterLab, un entorno de desarrollo interactivo que le permite explorar, analizar y modelar sus datos. Para obtener más información sobre el uso de la sección Notebooks , lea la [Guía del usuario de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Puede encontrar más información sobre Data Science Workspace en la [Información general de Data Science Workspace](../data-science-workspace/home.md)

La variable **[!UICONTROL Modelos]** permite utilizar el aprendizaje automático y la inteligencia artificial para crear, desarrollar, entrenar y ajustar modelos para realizar predicciones. Puede encontrar más información sobre la sección Modelos en el tutorial de [formación y evaluación de un modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La variable **[!UICONTROL Servicios]** permite administrar los modelos publicados para la formación y puntuación programadas, o utilizar los servicios inteligentes de Adobe, un conjunto de servicios de IA que ofrecen experiencias personalizadas y en tiempo real al cliente. Puede encontrar más información sobre la sección Servicios en la sección [Tutorial sobre la publicación de un modelo como servicio](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Administración de datos]

La variable **[!UICONTROL Esquemas]** permite crear y administrar esquemas del Modelo de datos de experiencia (XDM). Para obtener más información sobre los esquemas, lea el tutorial en [creación de un esquema](../xdm/tutorials/create-schema-ui.md). Puede encontrar más información sobre XDM en la [Información general del sistema XDM](../xdm/home.md).

La variable **[!UICONTROL Conjuntos de datos]** permite crear y administrar conjuntos de datos. Encontrará más información sobre los conjuntos de datos en la [guía del usuario de conjuntos de datos](../catalog/datasets/user-guide.md).

La variable **[!UICONTROL Consultas]** permite crear y administrar consultas, registrar consultas SQL realizadas por Adobe Experience Platform Query Service y ver su [!DNL PostgreSQL] credenciales. Encontrará más información sobre las consultas en la [Guía del usuario del servicio de consultas](../query-service/ui/overview.md).

La variable **[!UICONTROL Monitorización]** permite monitorizar la ingesta por lotes y de flujo continuo. Encontrará más información sobre la monitorización en la [guía del usuario sobre la ingesta de datos de monitorización](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Adobe Journey Optimizer es un servicio de aplicaciones creado sobre el Experience Platform. Le permite utilizar potentes tecnologías de toma de decisiones para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Para obtener más información sobre Journey Optimizer, incluido el uso de [!UICONTROL Ofertas] y [!UICONTROL Actividades] visite el [Documentación de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=es).

### [!UICONTROL Administración]

La interfaz de usuario (IU) de Platform proporciona un tablero a través del cual puede ver información importante sobre el uso de licencias de su organización, tal como se captura durante una instantánea diaria. Acceda a este tablero seleccionando **[!UICONTROL Uso de licencias]** en la navegación. Para obtener más información sobre el panel de uso de licencias, visite [guía del panel de uso de licencias](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funcionalidad del panel de uso de licencias está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Pasos siguientes

Al leer esta guía, ahora se le ha introducido en la página principal y en los principales elementos de navegación de la interfaz de usuario de Platform. Para obtener información más detallada sobre cómo trabajar en la interfaz de usuario, consulte la documentación de cada servicio de Platform individual. Los vínculos a esta documentación se proporcionan en la [navegación izquierda](#left-nav) sección encontrada anteriormente en este documento.
