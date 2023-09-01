---
title: Creación de una conexión de origen de Chatelio en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Chatlio mediante la interfaz de usuario de Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 1%

---

# Crear un [!DNL Chatlio] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Chatlio] el origen está en versión beta. Lea el [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una [!DNL Chatlio] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Requisitos previos {#prerequisites}

En la siguiente sección se proporciona información sobre los requisitos previos que se deben completar para poder crear una [!DNL Chatlio] conexión de origen.

### JSON de muestra para definir el esquema de origen de [!DNL Chatlio] {#prerequisites-json-schema}

Antes de crear un [!DNL Chatlio] conexión de origen, necesitará que se proporcione un esquema de origen. Puede utilizar el siguiente JSON.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Creación de un esquema de Platform para [!DNL Chatlio] {#create-platform-schema}

También debe asegurarse de crear un esquema de Platform para utilizarlo con el origen. Lea el tutorial sobre [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para obtener información detallada sobre cómo crear un esquema.

![La interfaz de usuario de Platform que muestra un esquema de ejemplo para Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Conecte su [!DNL Chatlio] account {#connect-account}

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace y vea un catálogo de fuentes disponibles en Experience Platform.

Utilice el *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la [!UICONTROL Automatización de marketing] para ver la [!DNL Chatlio] tarjeta de origen. Para empezar, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de la IU de Platform con la tarjeta Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Seleccionar datos {#select-data}

El **[!UICONTROL Seleccionar datos]** Este paso aparece y proporciona una interfaz para que seleccione los datos que desea llevar a Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccionar **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde el sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en [!UICONTROL Arrastrar y soltar archivos] panel.

![Paso para añadir datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede utilizar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Detalles de flujo de datos {#dataflow-detail}

El **Detalles del flujo de datos** Este paso se muestra y le proporciona opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Asignación {#mapping}

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Las asignaciones enumeradas a continuación son obligatorias y deben configurarse antes de continuar con la [!UICONTROL Revisar] escenario.

| Campo de destino | Descripción |
| --- | --- |
| `UUID` | El [!DNL Chatlio] identificador del evento. |

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Consulte {#review}

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint-url}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform.

Para construir la URL utilizada para configurar el webhook en [!DNL Chatlio] debe recuperar lo siguiente:

* **[!UICONTROL ID de flujo de datos]**
* **[!UICONTROL Extremo de streaming]**

Para recuperar su **[!UICONTROL ID de flujo de datos]** y **[!UICONTROL Extremo de streaming]**, vaya a la [!UICONTROL Actividad de flujo de datos] página del flujo de datos que acaba de crear y copie los detalles de la parte inferior de la [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Una vez que haya recuperado el extremo de flujo continuo y el ID de flujo de datos, cree una URL basada en el siguiente patrón: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por ejemplo, una URL de gancho web construida puede tener el siguiente aspecto: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Configuración del webhook en [!DNL Chatlio] {#set-up-webhook}

Con la URL del gancho web creada, ahora puede configurar el gancho web mediante el [!DNL Chatlio] interfaz de usuario.

Inicie sesión en su [[!DNL Chatlio]](https://chatlio.com/) cuenta y seguir [la guía de instalación e instalación](https://chatlio.com/docs/setup/) para crear un widget.

Una vez creado un widget, vaya a la página de configuración del widget para agregar la URL del gancho web a ese widget.

![La página de configuración del webhook en Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

A continuación, seleccione la **[!DNL Behavior]** y añada la URL de su webhook a *[!DNL Webhook when a new conversation starts]* y cualquier otro campo de eventos de webhook al que desee suscribirse.

![Interfaz de usuario de Chatlio que muestra el campo de extremo del gancho web.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Puede suscribirse a una variedad de eventos diferentes para su [!DNL Chatlio] gancho web. Para obtener más información sobre los diferentes eventos, consulte la [[!DNL Chatlio] documentación de eventos](https://chatlio.com/docs/webhooks/).

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha configurado correctamente un flujo de datos de flujo continuo para traer su [!DNL Chatlio] datos al Experience Platform. Para monitorizar los datos que se están introduciendo, consulte la guía de [monitorización de flujos de datos de streaming mediante la IU de Platform](../../monitor-streaming.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL Chatlio] origen.

### Validación {#validation}

Para validar que ha configurado correctamente el origen y [!DNL Chatlio] Si se están introduciendo mensajes, siga los pasos a continuación:

* Puede consultar la [!DNL Chatlio] **[!UICONTROL Informes]** > **[!UICONTROL Historial de chat]** para identificar los eventos que captura [!DNL Chatlio].

![Captura de pantalla de IU de Chatlio que muestra el historial de chat](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* En la IU de Platform, seleccione **[!UICONTROL Ver flujos de datos]** al lado del [!DNL Chatlio] menú de tarjeta en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para verificar los datos introducidos para los webhooks configurados en [!DNL Chatlio].

![Captura de pantalla de la IU de Platform que muestra eventos ingeridos](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Para obtener más información sobre [!DNL Chatlio], visite la [[!DNL Chatlio] documentación](https://chatlio.com/docs/) y [FAQ](https://chatlio.com/pricing/#FAQ).
