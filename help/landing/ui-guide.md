---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía del usuario;guía de la interfaz de usuario;guía de la interfaz de usuario de platform;introducción a platform;tablero;
solution: Experience Platform
title: Información general sobre la IU de Experience Platform
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Guía de la interfaz de usuario de Adobe Experience Platform

Esta guía sirve como introducción al uso de la interfaz de usuario (IU) de Adobe Experience Platform, explica para qué se utilizan los distintos componentes y proporciona vínculos a documentación adicional para obtener más información.

Para obtener más información sobre Adobe Experience Platform, lea la [información general del Experience Platform](home.md).

## Pantalla principal

Después de iniciar sesión en Adobe Experience Platform, se encuentra en la página [!UICONTROL Home], que consta de las secciones [panel de métricas](#metrics), [datos recientes](#recent-data) y [aprendizaje recomendado](#recommended-learning).

![](images/user-guide/homepage.png)

### Métricas

El tablero de métricas proporciona tarjetas que le proporcionan información sobre conjuntos de datos, perfiles, segmentos y destinos dentro de su organización.

![](images/user-guide/homepage-dashboard.png)

La sección **[!UICONTROL Datasets]** muestra la cantidad de conjuntos de datos dentro de su organización de IMS. Este número se actualiza cuando se crea un nuevo conjunto de datos. Puede encontrar más información sobre los conjuntos de datos en la [información general sobre los conjuntos de datos](../catalog/datasets/overview.md).

La sección **[!UICONTROL Profiles]** muestra el número total de personas con perfiles dentro de su organización IMS, excluidos los fragmentos de perfil. Este número total de personas representa la audiencia total a la que se puede dirigir y se actualiza una vez cada 24 horas. Puede encontrar más información sobre los perfiles en la [Descripción general del perfil del cliente en tiempo real](../profile/home.md).

La sección **[!UICONTROL Segments]** muestra el número total de segmentos creados dentro de su organización de IMS. Este número se actualiza cuando se crea un nuevo segmento. Puede encontrar más información sobre los segmentos en la [información general del Servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Destinations]** muestra el número total de destinos creados para la organización IMS. Este número se actualiza cuando se crea un nuevo destino. Puede encontrar más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### Datos recientes

El panel de datos reciente proporciona información sobre conjuntos de datos, fuentes, segmentos y destinos creados recientemente.

![](images/user-guide/homepage-recent.png)

La sección **[!UICONTROL Recent datasets]** enumera los cinco conjuntos de datos creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo conjunto de datos. Puede seleccionar un conjunto de datos de la lista para ver más información sobre el conjunto de datos especificado o seleccionar **[!UICONTROL View all]** para ver una lista de todos los conjuntos de datos creados. Puede encontrar más información sobre los conjuntos de datos en la [información general sobre los conjuntos de datos](../catalog/datasets/overview.md).

La sección **[!UICONTROL Recent sources]** enumera los cinco conectores de origen creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo conector de origen. Puede seleccionar una conexión de origen de la lista para ver más información sobre el conector especificado o seleccionar **[!UICONTROL View all]** para ver una lista de todas las conexiones de origen creadas. Puede encontrar más información sobre las fuentes en la [descripción general de las fuentes](../sources/home.md).

La sección **[!UICONTROL Recent segments]** enumera las cinco definiciones de segmento creadas más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea una nueva definición de segmento. Puede seleccionar una definición de segmento de la lista para ver más información sobre la definición de segmento especificada o seleccionar **[!UICONTROL View all]** para ver una lista de todas las definiciones de segmento creadas. Puede encontrar más información sobre los segmentos en la [información general del Servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Recent destinations]** enumera los cinco destinos creados más recientemente dentro de su organización IMS. Esta lista se actualiza cada vez que se crea un nuevo destino. Puede seleccionar un destino de la lista para ver más información sobre el destino especificado o seleccionar **[!UICONTROL View all]** para ver una lista de todos los destinos creados. Puede encontrar más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### Aprendizaje recomendado

La sección **[!UICONTROL Recommended learning]** proporciona vínculos a documentación útil para empezar a usar Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra de navegación superior

La barra de navegación superior de la interfaz de usuario de Platform muestra la organización de IMS en la que ha iniciado sesión y proporciona varios controles importantes.

En el lado izquierdo de la barra de navegación está el logotipo de Adobe Experience Platform. Si selecciona esto en cualquier momento, volverá a la pantalla de inicio de la interfaz de usuario de Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Conmutador de organización IMS

El primer elemento de la parte derecha de la barra de navegación superior es el **conmutador de organización IMS**.

![](./images/user-guide/homepage-ims-org.png)

Si selecciona el selector, se abre un menú desplegable de las organizaciones de IMS a las que tiene acceso, si hay alguna disponible. Seleccione una opción de la lista para cambiar a esa organización de IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Cambiar aplicaciones

El siguiente elemento del lado derecho de la navegación superior es el **conmutador de aplicaciones**, representado por el icono ![conmutador de aplicaciones](./images/user-guide/app-switcher-icon.png). Al seleccionar este icono, puede cambiar entre las aplicaciones de Adobe a las que tiene acceso su organización IMS, como Experience Platform, Analytics, Assets y Launch.

### Ayuda

A la derecha del conmutador de aplicaciones se encuentra el **menú de ayuda y soporte**, que se representa mediante el icono ![signo de interrogación/ayuda](./images/user-guide/help-icon.png). Al seleccionar este icono, aparece un menú emergente que contiene varios recursos de ayuda y asistencia. La pestaña **[!UICONTROL Help]** muestra una lista de la documentación relevante para la página en la que se encuentra. La pestaña **[!UICONTROL Support]** le permite crear un ticket de soporte con el equipo de soporte de Adobe. La pestaña **[!UICONTROL Feedback]** le permite enviar comentarios sobre Platform a Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Notificaciones y anuncios

En la sección **notifications**, que se representa mediante el icono ![bell/Notifications and Announcements](images/user-guide/notification-icon.png). La pestaña **[!UICONTROL Notifications]** muestra información importante sobre el producto y otras actualizaciones relevantes, mientras que la pestaña **[!UICONTROL Announcements]** muestra información sobre el mantenimiento del servicio.

### Perfil de usuario

El último elemento de la barra de navegación superior es la **configuración de usuario**, que se representa mediante el icono ![configuración de usuario/Perfil de usuario](images/user-guide/profile-icon.png). Seleccione este icono para editar sus preferencias o cerrar la sesión.

### Entornos aislados

Inmediatamente debajo de la barra de navegación superior se encuentra la barra de entorno limitado. Esta barra muestra qué simulador de pruebas está utilizando para Platform. Puede encontrar más información sobre los entornos limitados en la [información general de los entornos limitados](../sandboxes/home.md).

## Navegación izquierda {#left-nav}

La navegación de la parte izquierda de la pantalla enumera todos los servicios compatibles con la interfaz de usuario de Platform.

>[!IMPORTANT]
>
>Es posible que algunas de las secciones de la barra de navegación izquierda no aparezcan o estén atenuadas. Esto se debe a que no tiene acceso a esas funciones. Si cree que debe tener acceso a estas secciones, póngase en contacto con el administrador del sistema.

![](images/user-guide/homepage-left.png)

La sección **[!UICONTROL Home]** le permite volver a la página principal de la interfaz de usuario de Platform.

La sección **[!UICONTROL Workflows]** muestra una lista de flujos de trabajo de varios pasos para realizar operaciones dentro de Platform. Puede encontrar más información sobre los flujos de trabajo en la [descripción general de los flujos de trabajo](./workflows.md).

### [!UICONTROL Connections]

La sección **[!UICONTROL Sources]** permite crear, actualizar y eliminar conexiones de origen, lo que permite introducir datos de fuentes externas en Platform. Puede encontrar más información sobre las fuentes en la [descripción general de las fuentes](../sources/home.md).

La sección **[!UICONTROL Destinations]** permite crear, actualizar y eliminar destinos, lo que permite exportar datos desde Platform a muchos destinos externos. Puede encontrar más información sobre los destinos en la [información general sobre destinos](../destinations/home.md).

### [!UICONTROL Customer]

La sección **[!UICONTROL Profiles]** permite examinar perfiles de clientes, ver métricas de perfil, crear y administrar políticas de combinación y ver esquemas de unión. Para obtener más información sobre el uso de la sección [!UICONTROL Profiles], lea la [[!DNL Profile] guía del usuario](../profile/ui/user-guide.md). Puede encontrar más información sobre el Perfil del cliente en tiempo real en la [Descripción general del Perfil del cliente en tiempo real](../profile/home.md).

La sección **[!UICONTROL Segments]** permite crear y administrar definiciones de segmento. Para obtener más información sobre el uso de la sección [!UICONTROL Segments], lea la [guía del usuario de segmentación](../segmentation/ui/overview.md). Puede encontrar más información sobre el Servicio de segmentación en la [información general del Servicio de segmentación](../segmentation/home.md).

La sección **[!UICONTROL Identities]** permite crear y administrar áreas de nombres de identidad. Para obtener más información sobre la sección [!UICONTROL Identities], incluida información sobre los espacios de nombres de identidad y cómo utilizar identidades en la interfaz de usuario de Platform, consulte la [descripción general del área de nombres de identidad](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

La sección **[!UICONTROL Policies]** permite crear y administrar políticas de uso de datos. Para obtener más información sobre el uso de la sección Directivas , lea la [guía del usuario de directivas de uso de datos](../data-governance/policies/user-guide.md). Puede encontrar más información sobre las políticas de uso de datos en la [información general sobre las políticas de uso de datos](../data-governance/policies/overview.md).

La sección **[!UICONTROL Requests]** permite crear y administrar solicitudes de privacidad. Tenga en cuenta que debe estar incluido en la lista de permitidos para tener acceso a la IU del Privacy Service. Para obtener más información sobre el uso de la sección Solicitudes, lea la [guía del usuario del Privacy Service](../privacy-service/ui/user-guide.md). Puede encontrar más información sobre el Privacy Service en la [descripción general del Privacy Service](../privacy-service/home.md).

### [!UICONTROL Data Science]

La sección **[!UICONTROL Notebooks]** proporciona acceso a JupyterLab, un entorno de desarrollo interactivo que le permite explorar, analizar y modelar sus datos. Para obtener más información sobre el uso de la sección Notebooks , lea la [guía del usuario de JupyterLab](../data-science-workspace/jupyterlab/overview.md). Encontrará más información sobre Data Science Workspace en la [información general de Data Science Workspace](../data-science-workspace/home.md)

La sección **[!UICONTROL Models]** permite aprovechar el aprendizaje automático y la inteligencia artificial para crear, desarrollar, entrenar y ajustar modelos para hacer predicciones. Puede encontrar más información sobre la sección Modelos en el tutorial sobre [formación y evaluación de un modelo](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La sección **[!UICONTROL Services]** permite administrar los modelos publicados para la formación y puntuación programadas, o aprovechar los servicios inteligentes de Adobe, un conjunto de servicios de IA que ofrecen experiencias personalizadas en tiempo real para los clientes. Puede encontrar más información sobre la sección Servicios en el tutorial [Publicación de un modelo como servicio](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

La sección **[!UICONTROL Schemas]** permite crear y administrar esquemas del Modelo de datos de experiencia (XDM). Para obtener más información sobre los esquemas, lea el tutorial sobre la [creación de un esquema](../xdm/tutorials/create-schema-ui.md). Puede encontrar más información sobre XDM en la [información general del sistema XDM](../xdm/home.md).

La sección **[!UICONTROL Datasets]** permite crear y administrar conjuntos de datos. Puede encontrar más información sobre los conjuntos de datos en la [guía del usuario de conjuntos de datos](../catalog/datasets/user-guide.md).

La sección **[!UICONTROL Queries]** permite crear y administrar consultas, registrar consultas SQL realizadas por el servicio de consulta de Adobe Experience Platform y ver las credenciales de PostgreSQL. Puede encontrar más información sobre las consultas en la [Guía del usuario del servicio de consulta](../query-service/ui/overview.md).

La sección **[!UICONTROL Monitoring]** permite monitorizar la ingesta por lotes y de flujo continuo. Puede encontrar más información sobre la monitorización en la [guía del usuario sobre la incorporación de datos de monitorización](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Offer Decisioning es un servicio de aplicaciones integrado en Adobe Experience Platform. Le permite aprovechar Experience Platform para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Para obtener más información sobre el Offer decisioning, incluido el trabajo con [!UICONTROL Offers] y [!UICONTROL Activities], visite la [documentación del Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

La interfaz de usuario (IU) de Platform proporciona un tablero a través del cual puede ver información importante sobre el uso de licencias de su organización, tal como se captura durante una instantánea diaria. Se puede acceder a esta opción seleccionando **[!UICONTROL License usage]** en la navegación. Para obtener más información sobre el panel de uso de licencias, visite la [guía del tablero de uso de licencias](license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funcionalidad del panel de uso de licencias está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Pasos siguientes

Al leer esta guía, ahora se le ha introducido en la página principal y en los principales elementos de navegación de la interfaz de usuario de Platform. Para obtener información más detallada sobre cómo trabajar en la interfaz de usuario, consulte la documentación de cada servicio de Platform individual. Los vínculos a esta documentación se proporcionan en la sección [navegación izquierda](#left-nav) que se encuentra anteriormente en este documento.
