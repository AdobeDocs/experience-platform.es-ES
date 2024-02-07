---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;campaña;servicios administrados de campaign
title: Crear una conexión de origen de Adobe Campaign Managed Cloud Services mediante la IU de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Adobe Campaign Managed Cloud Services mediante la interfaz de usuario de Platform.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 6%

---

# Crear una conexión de origen de Adobe Campaign Managed Cloud Services mediante la IU de Platform

Este tutorial proporciona pasos para crear una conexión de origen para llevar los datos de Adobe Campaign Managed Cloud Services a Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Conectar Adobe Campaign Managed Cloud Services a Platform

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccionar **[!UICONTROL Adobe Campaign Managed Cloud Services]** y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes que muestra la tarjeta de Adobe Campaign Managed Cloud Services.](../../../../images/tutorials/create/campaign/catalog.png)

### Seleccionar datos {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Instancia del entorno de Adobe Campaign"
>abstract="Nombre del entorno de Adobe Campaign que desea utilizar."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Asignación de destino"
>abstract="Las asignaciones de destino son objetos técnicos que Campaign utiliza para enviar mensajes y contienen toda la configuración técnica necesaria para realizar envíos (direcciones, números de teléfono, indicadores de inclusión, identificadores adicionales…)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Nombre del esquema"
>abstract="Nombre de la entidad definida en la base de datos de Adobe Campaign."
>text="Learn more in documentation"

El [!UICONTROL Seleccionar datos] Este paso aparece y le proporciona una interfaz para configurar su [!UICONTROL Instancia de Adobe Campaign], [!UICONTROL Asignación de destino], y [!UICONTROL Nombre del esquema].

| Propiedad | Descripción |
| --- | --- |
| Instancia de Adobe Campaign | El nombre de la instancia de entorno de Adobe Campaign que está utilizando. |
| Asignación de destino | Los objetos técnicos utilizados por Campaign para enviar mensajes y contienen toda la configuración técnica necesaria para realizar envíos. |
| Nombre del esquema | El nombre de la entidad de esquema que está trayendo a Platform. Las opciones incluyen Registro de envío y Registro de seguimiento. |

![Una interfaz en la que puede configurar la instancia de Adobe Campaign, la asignación de destino y el nombre del esquema.](../../../../images/tutorials/create/campaign/select-data.png)

Una vez que haya proporcionado los valores de la instancia de Campaign, la asignación de destino y el nombre del esquema, la pantalla se actualiza para mostrar una vista previa del esquema y un conjunto de datos de ejemplo. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Una previsualización de la jerarquía de esquemas y un ejemplo del conjunto de datos](../../../../images/tutorials/create/campaign/preview.png)

### Usar un conjunto de datos existente

El [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o configurar un nuevo conjunto de datos para el flujo de datos.

Para utilizar un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable.

Con un conjunto de datos seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional.

![Una interfaz que muestra la opción del conjunto de datos existente.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Usar un nuevo conjunto de datos

Para utilizar un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre del conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Interfaz que muestra la nueva opción del conjunto de datos.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Habilitar alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la IU](../../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![Una selección de diferentes tipos de alertas que puede habilitar para el flujo de datos.](../../../../images/tutorials/create/campaign/alerts.png)

### Asignación de campos de datos a un esquema XDM

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Al asignar los campos de origen a los campos XDM de destino, debe asegurarse de asignar el campo de identidad principal designado a su campo XDM de destino adecuado.

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Un árbol de asignación con cuatro campos de datos de origen asignados a sus campos de esquema XDM correspondientes.](../../../../images/tutorials/create/campaign/mapping.png)

### Revisión del flujo de datos

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![Una página de revisión que muestra la información de conexión y del conjunto de datos.](../../../../images/tutorials/create/campaign/review.png)

### Monitorice la actividad del conjunto de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las tasas de ingesta y los lotes correctos y fallidos.

Para empezar a ver la actividad del conjunto de datos, seleccione **[!UICONTROL Flujos de datos]** en el catálogo de fuentes.

![La página del catálogo de fuentes con la pestaña de encabezado de flujos de datos seleccionada.](../../../../images/tutorials/create/campaign/dataflows.png)

A continuación, seleccione el conjunto de datos de destino de la lista de flujos de datos que aparecen.

![Una lista de flujos de datos existentes con el conjunto de datos de destino Registros de envío de Adobe Campaign seleccionado.](../../../../images/tutorials/create/campaign/target-dataset.png)

Aparecerá la página de actividad del conjunto de datos. Aquí puede ver información sobre el rendimiento del flujo de datos, incluida la tasa de ingesta, los lotes correctos y los lotes fallidos.

Esta página también le proporciona una interfaz para actualizar la descripción de metadatos del flujo de datos, habilitar la ingesta parcial y los diagnósticos de error, así como añadir nuevos datos al conjunto de datos.

![Una interfaz con gráficos que representan la tasa de ingesta de un conjunto de datos seleccionado.](../../../../images/tutorials/create/campaign/dataset-activity.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para llevar los datos de los registros de envío y de seguimiento de Campaign v8 a Platform. Ahora, los servicios de Platform posteriores pueden utilizar los datos entrantes, como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
