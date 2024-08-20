---
title: Notas de la versión de Adobe Experience Platform, agosto de 2024
description: Notas de la versión de agosto de 2024 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6d8c785a1e876ed6a729efbe01ad8fb4507bda0d
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: miércoles, 20 de agosto de 2024**

>[!TIP]
>
>Vea [información general sobre la documentación de casos de uso de ejemplo](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) para obtener más información sobre varios casos de uso, como prospección, adquisición y mucho más que su organización puede lograr con Real-Time CDP.

Actualizaciones de funciones y documentación existentes en Experience Platform:

- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| ----------- | ----------- |
| Ya está disponible de forma general la exportación de archivos bajo demanda a destinos por lotes. | La opción de exportar archivos bajo demanda a destinos por lotes ya está disponible para todos los clientes. Consulte la [documentación dedicada](../../destinations/ui/export-file-now.md) para obtener más detalles. |
| Edite las programaciones de exportación de varias audiencias exportadas en el [paso de programación](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | La opción para editar los programas de exportación para varias audiencias exportadas directamente desde el paso de programación del flujo de trabajo de activación de audiencia ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar programación en el paso de programación.](../2024/assets/august/edit-schedule.png) {width="250" align="center" zoomable="yes"} |
| Edite los nombres de archivo para varias audiencias exportadas en el [paso de programación](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | La opción para editar los nombres de varios archivos exportados directamente desde el paso de programación del flujo de trabajo de activación de audiencia ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar nombre de archivo en el paso de programación.](../2024/assets/august/edit-file-name.png) {width="250" align="center" zoomable="yes"} |
| Elimine varias audiencias de un flujo de datos de la página [Detalles del destino](../../destinations/ui/destination-details-page.md#bulk-remove). | La opción de quitar varias audiencias de flujos de datos existentes de la página **[!UICONTROL Detalles del destino]** ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Quitar audiencias en la página Detalles de destino.](../2024/assets/august/bulk-remove-audiences.png) {width="250" align="center" zoomable="yes"} |
| Exporte varios archivos bajo demanda a destinos por lotes desde la página [Detalles de destino](../../destinations/ui/destination-details-page.md#bulk-export). | La opción de exportar varios archivos bajo demanda a destinos por lotes desde la página **[!UICONTROL Detalles de destino]** ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Exportar archivo ahora en la página Detalles de destino.](../2024/assets/august/bulk-export-file-now.png) {width="250" align="center" zoomable="yes"} |
| Edite los nombres de archivo de varias audiencias exportadas desde la página [Detalles de destino](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Ahora puede editar los nombres de varios archivos exportados directamente desde la página **[!UICONTROL Detalles del destino]**. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción de editar nombre de archivo en la página de detalles de destino.](../2024/assets/august/edit-file-name-destination-details.png) {width="250" align="center" zoomable="yes"} |
| Elimine varios conjuntos de datos de un flujo de datos de la página [Detalles de destino](../../destinations/ui/export-datasets.md#remove-dataset). | La opción de quitar varios conjuntos de datos de un flujo de datos ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Quitar conjuntos de datos en la página de detalles de destino.](../2024/assets/august/bulk-remove-datasets.png) {width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Flujo de creación de esquema asistido por ML | Utilice algoritmos avanzados de aprendizaje automático para analizar los archivos de datos CSV de ejemplo y crear automáticamente esquemas optimizados con campos estándar y personalizados.<br>Características principales:<br><ul><li>Creación de esquemas más rápida: genere esquemas directamente a partir de archivos de datos de ejemplo utilizando campos XDM generados y recomendados por ML.</li><li>Evolución del esquema flexible: añada o actualice fácilmente los campos en el esquema generado.</li><li>Integración perfecta: se integra completamente con el flujo de creación de esquemas principal en la URL del esquema, lo que garantiza una experiencia de usuario uniforme y coherente.</li><li>Revisión y edición eficientes: vea y actualice rápidamente su esquema con el editor de vista plana, lo que hace que el proceso de creación sea más eficiente y fácil de usar.</li></ul> |

{style="table-layout:auto"}

<!-- To learn more, read the [ML-assisted schema creation overview](../../xdm/ui/ml-assisted-schema-creation.md)  -->

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

Utilice el servicio de identidad de Adobe Experience Platform para crear una vista completa de sus clientes y sus comportamientos mediante la fusión de identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Documentación actualizada**

| Función | Descripción |
| --- | --- |
| Guía de configuraciones de gráficos | Lea la [guía de configuraciones de gráficos](../../identity-service/identity-graph-linking-rules/example-configurations.md) para obtener información sobre escenarios de gráficos comunes que podrían encontrarse al trabajar con reglas de vinculación de gráficos de identidad y datos de identidad. La guía de configuraciones de gráficos proporciona ejemplos que van desde escenarios de gráficos simples de una sola persona a escenarios de gráficos complejos y jerárquicos de varias personas. También puede usar la guía para ver ejemplos de eventos y configuraciones de algoritmo que puede introducir en la [IU de simulación de gráficos](../../identity-service/identity-graph-linking-rules/graph-simulation.md), así como desgloses de cómo se seleccionan las identidades principales en determinados escenarios de gráficos. |

{style="table-layout:auto"}

Para obtener más información sobre el servicio de identidad, lea la [descripción general del servicio de identidad](../../identity-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Detalles de ingesta | En el caso de las audiencias con el origen de carga personalizada, puede ver de forma más completa los detalles de la ingesta de la audiencia en la página de detalles de audiencia. Además, puede aplicar etiquetas a los atributos de carga útil seleccionando el esquema y los atributos deseados para el etiquetado. Encontrará más información sobre la sección de detalles de ingesta en la [guía de Audience Portal](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Fuentes

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Documentación actualizada**

| Documentación actualizada | Descripción |
| --- | --- |
| Documentación ampliada sobre la actualización de flujos de datos | La guía sobre [actualización de flujos de datos de origen existentes en la interfaz de usuario](../../sources/tutorials/ui/update-dataflows.md) se ha actualizado para proporcionar más información sobre la variedad de configuraciones que puede realizar en un flujo de datos existente. La guía también se ha actualizado para aclarar el comportamiento esperado cuando se vuelve a habilitar un flujo de datos deshabilitado. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de orígenes](../../sources/home.md).