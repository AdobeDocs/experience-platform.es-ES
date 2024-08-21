---
title: Notas de la versión de Adobe Experience Platform, agosto de 2024
description: Notas de la versión de agosto de 2024 de Adobe Experience Platform.
source-git-commit: d01e16938485f6648cc02ce1674e0e9e84d78147
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 21%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 20 de agosto de 2024**

>[!TIP]
>
>Vea [información general sobre la documentación de casos de uso de ejemplo](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) para obtener más información sobre varios casos de uso, como prospección, adquisición y mucho más que su organización puede lograr con Real-Time CDP.

Actualizaciones de funciones y documentación existentes en Experience Platform:

- [Control de acceso basado en atributos](#abac)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Control de acceso basado en atributos {#abac}

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad una mayor flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a funciones de usuario. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Platform específicos de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y otro tipo personalizado de datos en todos los flujos de trabajo y recursos de la plataforma. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

**Nueva funcionalidad**

| Actualización de funciones | Descripción |
| --- | --- |
| Nueva característica del Administrador de permisos | Ahora puede usar [Administrador de permisos](../../access-control/abac/permission-manager/overview.md) para generar informes mediante consultas simples, lo que le ayudará a comprender la administración de acceso y a ahorrar tiempo en la verificación de los permisos de acceso en varios flujos de trabajo y niveles de granularidad. Para obtener más información sobre la creación de informes para usuarios y funciones, consulte la [Guía del usuario del Administrador de permisos](../../access-control/abac/permission-manager/permissions.md). ![La interfaz de usuario del Experience Platform de imágenes resalta el Administrador de permisos en la barra de navegación izquierda.](../2024/assets/august/permission-manager-rn.png "Administrador de permisos en la interfaz de usuario."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información sobre el control de acceso basado en atributos, vea la [descripción general del control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo de control de acceso basado en atributos, lea la [guía completa de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| ----------- | ----------- |
| Ya está disponible de forma general la exportación de archivos bajo demanda a destinos por lotes. | La opción de exportar archivos bajo demanda a destinos por lotes ya está disponible para todos los clientes. Consulte la [documentación dedicada](../../destinations/ui/export-file-now.md) para obtener más detalles. |
| Edite las programaciones de exportación de varias audiencias exportadas en el [paso de programación](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | La opción para editar los programas de exportación para varias audiencias exportadas directamente desde el paso de programación del flujo de trabajo de activación de audiencia ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar programación en el paso de programación.](../2024/assets/august/edit-schedule.png "Editar opción de horario en el paso de horario."){width="250" align="center" zoomable="yes"} |
| Edite los nombres de archivo para varias audiencias exportadas en el [paso de programación](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | La opción para editar los nombres de varios archivos exportados directamente desde el paso de programación del flujo de trabajo de activación de audiencia ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar nombre de archivo en el paso de programación.](../2024/assets/august/edit-file-name.png "Editar opción de nombre de archivo en el paso de programación."){width="250" align="center" zoomable="yes"} |
| Elimine varias audiencias de un flujo de datos de la página [Detalles del destino](../../destinations/ui/destination-details-page.md#bulk-remove). | La opción de quitar varias audiencias de flujos de datos existentes de la página **[!UICONTROL Detalles del destino]** ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Quitar audiencias en la página Detalles de destino.](../2024/assets/august/bulk-remove-audiences.png "Opción Quitar audiencias en la página Detalles de destino."){width="250" align="center" zoomable="yes"} |
| Exporte varios archivos bajo demanda a destinos por lotes desde la página [Detalles de destino](../../destinations/ui/destination-details-page.md#bulk-export). | La opción de exportar varios archivos bajo demanda a destinos por lotes desde la página **[!UICONTROL Detalles de destino]** ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Exportar archivo ahora en la página Detalles de destino.](../2024/assets/august/bulk-export-file-now.png "Opción Exportar archivo ahora en la página Detalles de destino."){width="250" align="center" zoomable="yes"} |
| Edite los nombres de archivo de varias audiencias exportadas desde la página [Detalles de destino](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Ahora puede editar los nombres de varios archivos exportados directamente desde la página **[!UICONTROL Detalles del destino]**. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Editar nombre de archivo en la página de detalles de destino.](../2024/assets/august/edit-file-name-destination-details.png "Editar opción de nombre de archivo en la página de detalles de destino."){width="250" align="center" zoomable="yes"} |
| Elimine varios conjuntos de datos de un flujo de datos de la página [Detalles de destino](../../destinations/ui/export-datasets.md#remove-dataset). | La opción de quitar varios conjuntos de datos de un flujo de datos ya está disponible para todos los clientes. ![Imagen de la interfaz de usuario del Experience Platform que resalta la opción Quitar conjuntos de datos en la página de detalles de destino.](../2024/assets/august/bulk-remove-datasets.png "Quitar opción de conjuntos de datos en la página de detalles de destino."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Flujo de creación de esquema asistido por ML | Utilice algoritmos avanzados de aprendizaje automático para analizar los archivos de datos de ejemplo y crear automáticamente esquemas optimizados con campos estándar y personalizados.<br>Características principales:<br><ul><li>Creación de esquemas más rápida: genere esquemas directamente a partir de archivos de datos de ejemplo utilizando campos XDM generados y recomendados por ML.</li><li>Evolución del esquema flexible: añada o actualice fácilmente los campos en el esquema generado.</li><li>Integración perfecta: se integra completamente con el flujo de creación de esquemas principal en la URL del esquema, lo que garantiza una experiencia de usuario uniforme y coherente.</li><li>Revisión y edición eficientes: vea y actualice rápidamente su esquema con el editor de vista plana, lo que hace que el proceso de creación sea más eficiente y fácil de usar.</li></ul><br>Para obtener más información, lea la [guía de flujo de trabajo para la creación de esquemas asistida por ML](../../xdm/ui/ml-assisted-schema-creation.md). |

{style="table-layout:auto"}

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
