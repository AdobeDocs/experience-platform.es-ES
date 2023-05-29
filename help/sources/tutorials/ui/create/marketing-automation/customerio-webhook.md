---
title: Crear una conexión de origen y un flujo de datos de Customer.io en la IU de
description: Obtenga información sobre cómo crear una conexión de origen Customer.io mediante la interfaz de usuario de Adobe Experience Platform.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Crear un [!DNL Customer.io] conexión de origen y flujo de datos en la IU

>[!NOTE]
>
>El [!DNL Customer.io] el origen está en versión beta. Lea el [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una [!DNL Customer.io] conexión de origen y flujo de datos mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Requisitos previos {#prerequisites}

En la siguiente sección se proporciona información sobre los requisitos previos que se deben completar para poder crear una [!DNL Customer.io] conexión de origen.

### JSON de muestra para definir el esquema de origen de [!DNL Customer.io] {#prerequisites-json-schema}

Antes de crear un [!DNL Customer.io] conexión de origen, necesitará que se proporcione un esquema de origen. Puede utilizar el siguiente JSON.

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### Creación de un esquema de Platform para [!DNL Customer.io] {#create-platform-schema}

También debe asegurarse de crear un esquema de Platform para utilizarlo con el origen. Consulte el tutorial sobre [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para obtener información detallada sobre cómo crear un esquema.

![Captura de pantalla de la IU de Platform que muestra un esquema de ejemplo para Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Conecte su [!DNL Customer.io] account {#connect-account}

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace y vea un catálogo de fuentes disponibles en Experience Platform.

Utilice el *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la [!UICONTROL Automatización de marketing] para ver la [!DNL Customer.io] tarjeta de origen. Para empezar, seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la IU de Platform para el catálogo con la tarjeta Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Seleccionar datos {#select-data}

El **[!UICONTROL Seleccionar datos]** Este paso aparece y proporciona una interfaz para que seleccione los datos que desea llevar a Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccionar **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde el sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en [!UICONTROL Arrastrar y soltar archivos] panel.

![Paso para añadir datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede utilizar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Detalles de flujo de datos {#dataflow-detail}

El **Detalles del flujo de datos** Este paso se muestra y le proporciona opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Asignación {#mapping}

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Todas las asignaciones enumeradas a continuación son obligatorias y deben configurarse antes de continuar con la [!UICONTROL Revisar] escenario.

| Campo de destino | Descripción |
| --- | --- |
| `object_type` | El tipo de objeto, consulte la [!DNL Customer.io] [eventos](https://customer.io/docs/webhooks/#events) para los tipos compatibles. |
| `id` | El identificador del objeto. |
| `email` | La dirección de correo electrónico asociada con el objeto. |
| `event_id` | El identificador único del evento. |
| `cio_id` | El [!DNL Customer.io] identificador del evento. |
| `metric` | El tipo de evento. Para obtener más información, consulte la [!DNL Customer.io] [eventos](https://customer.io/docs/webhooks/#events) para los tipos compatibles. |
| `timestamp` | La marca de tiempo cuando se produjo el evento. |

>[!IMPORTANT]
>
>No asignar `cio_id` al ejecutar [!DNL Customer.io] webhook en el `test mode` ya que no habrá campos asociados enviados desde [!DNL Customer.io].

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Consulte {#review}

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform.

Para construir la URL utilizada para configurar el webhook en [!DNL Customer.io] debe recuperar lo siguiente:

* **[!UICONTROL ID de flujo de datos]**
* **[!UICONTROL Extremo de streaming]**

Para recuperar su **[!UICONTROL ID de flujo de datos]** y **[!UICONTROL Extremo de streaming]**, vaya a la [!UICONTROL Actividad de flujo de datos] página del flujo de datos que acaba de crear y copie los detalles de la parte inferior de la [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Una vez que haya recuperado el extremo de flujo continuo y el ID de flujo de datos, cree una URL basada en el siguiente patrón: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por ejemplo, una URL de gancho web construida puede tener el siguiente aspecto: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configuración del webhook de informes en [!DNL Customer.io] {#set-up-webhook}

Con la URL del gancho web creada, ahora puede configurar el gancho web de informes con la variable [!DNL Customer.io] interfaz de usuario. Para ver los pasos de configuración de los webhooks de creación de informes, lea la [[!DNL Customer.io] guía](https://customer.io/docs/webhooks/#setup) al configurar webhooks.

En el [!DNL Customer.io] interfaz de usuario, escriba su [URL de webhook](#get-streaming-endpoint-url) en el [!DNL WEBHOOK ENDPOINT] field.

![Interfaz de usuario de Customer.io que muestra el campo de extremo del gancho web](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Puede suscribirse a una variedad de eventos diferentes para su webhook de informes. Cada mensaje de los eventos se incorporará a Platform cuando [!DNL Customer.io] se cumplen los criterios de déclencheur de eventos de acción. Para obtener más información sobre los diferentes eventos, consulte la [[!DNL Customer.io] documentación de eventos](https://customer.io/docs/webhooks/#events).

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha configurado correctamente un flujo de datos de flujo continuo para traer su [!DNL Customer.io] datos al Experience Platform. Para monitorizar los datos que se están introduciendo, consulte la guía de [monitorización de flujos de datos de flujo continuo mediante la IU de Platform](../../monitor-streaming.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL Customer.io] origen.

### Mecanismos de protección {#guardrails}

Para obtener información sobre las barreras, consulte la [[!DNL Customer.io] página tiempos de espera y errores](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validación {#validation}

Para validar que ha configurado correctamente el origen y [!DNL Customer.io] Si se están introduciendo mensajes, siga los pasos a continuación:

* Puede consultar la [!DNL Customer.io] **[!UICONTROL Registros de actividades]** para identificar los eventos que captura [!DNL Customer.io].

![Captura de pantalla de la IU de Customer.io que muestra registros de actividad](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* En la IU de Platform, seleccione **[!UICONTROL Ver flujos de datos]** al lado del [!DNL Customer.io] menú de tarjeta en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para verificar los datos introducidos para los eventos seleccionados en [!DNL Customer.io].

![Captura de pantalla de la IU de Platform que muestra eventos ingeridos](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
