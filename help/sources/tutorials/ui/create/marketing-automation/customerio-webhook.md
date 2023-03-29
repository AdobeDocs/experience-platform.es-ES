---
title: Crear una conexión de origen de Customer.io y un flujo de datos en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen Customer.io mediante la interfaz de usuario de Adobe Experience Platform.
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Cree un [!DNL Customer.io] conexión de origen y flujo de datos en la interfaz de usuario

>[!NOTE]
>
>La variable [!DNL Customer.io] el origen está en versión beta. Lea el [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Este tutorial proporciona los pasos para crear un [!DNL Customer.io] conexión de origen y flujo de datos mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Requisitos previos {#prerequisites}

La siguiente sección proporciona información sobre los requisitos previos que se deben completar antes de crear un [!DNL Customer.io] conexión de origen.

### JSON de muestra para definir el esquema de origen para [!DNL Customer.io] {#prerequisites-json-schema}

Antes de crear una [!DNL Customer.io] conexión de origen, se requiere que se proporcione un esquema de origen. Puede utilizar el siguiente JSON.

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

### Crear un esquema de Platform para [!DNL Customer.io] {#create-platform-schema}

También debe asegurarse de crear un esquema de Platform para utilizarlo con el origen. Consulte el tutorial en [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para ver los pasos completos sobre cómo crear un esquema.

![Captura de pantalla de la interfaz de usuario de Platform que muestra un esquema de ejemplo para Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Conecte su [!DNL Customer.io] account {#connect-account}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo y ver un catálogo de fuentes disponibles en Experience Platform.

Utilice la variable *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. Como alternativa, introduzca un nombre de origen en la barra de búsqueda para encontrar un origen específico del catálogo.

Vaya a la [!UICONTROL Automatización de marketing] para ver la [!DNL Customer.io] tarjeta de origen. Para empezar, seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la interfaz de usuario de Platform para el catálogo con tarjeta Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Seleccionar datos {#select-data}

La variable **[!UICONTROL Seleccionar datos]** , proporcionando una interfaz para que seleccione los datos que desea traer a Platform.

* La parte izquierda de la interfaz es un navegador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Select **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. Como alternativa, puede arrastrar y soltar el archivo JSON que desea cargar en el [!UICONTROL Arrastrar y soltar archivos] panel.

![El paso añadir datos del flujo de trabajo de fuentes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema que ha cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![El paso de vista previa del flujo de trabajo de fuentes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Detalles de flujo de datos {#dataflow-detail}

La variable **Detalles de flujo de datos** aparece, proporcionando opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como una oportunidad para proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de ingesta de perfiles, diagnóstico de errores, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de flujo de datos detallado del flujo de trabajo de origen.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Asignación {#mapping}

La variable [!UICONTROL Asignación] aparece, proporcionando una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](../../../../../data-prep/ui/mapping.md).

Todas las asignaciones que se enumeran a continuación son obligatorias y deben configurarse antes de continuar con el [!UICONTROL Consulte] etapa.

| Campo de destino | Descripción |
| --- | --- |
| `object_type` | El tipo de objeto, consulte la sección [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentación de los tipos admitidos. |
| `id` | Identificador del objeto. |
| `email` | La dirección de correo electrónico asociada al objeto. |
| `event_id` | Identificador único del evento. |
| `cio_id` | La variable [!DNL Customer.io] identificador del evento. |
| `metric` | El tipo de evento. Para obtener más información, consulte [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentación para tipos compatibles. |
| `timestamp` | Marca de fecha y hora en la que se produjo el evento. |

>[!IMPORTANT]
>
>No asignar `cio_id` al ejecutar [!DNL Customer.io] weblock en la `test mode` ya que no se enviarán campos asociados desde [!DNL Customer.io].

Una vez asignados correctamente los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![El paso de asignación del flujo de trabajo de fuentes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Consulte {#review}

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![El paso de revisión del flujo de trabajo de fuentes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto final se utilizará para suscribirse a su enlace web, permitiendo que su fuente de transmisión se comunique con el Experience Platform.

Para construir la URL utilizada para configurar el enlace web en [!DNL Customer.io] debe recuperar lo siguiente:

* **[!UICONTROL ID de flujo de datos]**
* **[!UICONTROL Punto final de transmisión]**

Para recuperar el **[!UICONTROL ID de flujo de datos]** y **[!UICONTROL Punto final de transmisión]**, vaya a la [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie los detalles desde la parte inferior de la [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Una vez que haya recuperado el punto final de flujo continuo y el ID de flujo de datos, cree una URL basada en el siguiente patrón: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por ejemplo, una URL de enlace web construida puede tener el siguiente aspecto: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configure el enlace web de informes en [!DNL Customer.io] {#set-up-webhook}

Con la URL del vínculo web creada, ahora puede configurar el vínculo web de informes mediante el complemento [!DNL Customer.io] interfaz de usuario. Para ver los pasos sobre la configuración de los enlaces web de informes, lea la [[!DNL Customer.io] guía](https://customer.io/docs/webhooks/#setup) al configurar los enlaces web.

En el [!DNL Customer.io] interfaz de usuario, introduzca su [URL del enlace web](#get-streaming-endpoint-url) en el [!DNL WEBHOOK ENDPOINT] campo .

![La interfaz de usuario de Customer.io muestra el campo de extremo de enlace web](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Puede suscribirse a una variedad de eventos diferentes para su enlace web de informes. El mensaje de cada evento se incorporará a Platform cuando se [!DNL Customer.io] se cumplen los criterios de déclencheur del evento de acción. Para obtener más información sobre los diferentes eventos, consulte la [[!DNL Customer.io] documentación de eventos](https://customer.io/docs/webhooks/#events).

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha configurado correctamente un flujo de datos de flujo continuo para traer su [!DNL Customer.io] datos para el Experience Platform. Para monitorizar los datos que se están incorporando, consulte la guía de [monitorización de flujos de datos de flujo continuo mediante la interfaz de usuario de Platform](../../monitor-streaming.md).

## Recursos adicionales {#additional-resources}

Las secciones a continuación proporcionan recursos adicionales a los que puede hacer referencia al utilizar la variable [!DNL Customer.io] fuente.

### Mecanismos de protección {#guardrails}

Para obtener información sobre las barreras, consulte la [[!DNL Customer.io] página de tiempos de espera y errores](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validación {#validation}

Para validar que ha configurado correctamente el origen y [!DNL Customer.io] se están incorporando mensajes, siga los pasos a continuación:

* Puede comprobar la [!DNL Customer.io] **[!UICONTROL Registros de actividades]** para identificar los eventos que captura [!DNL Customer.io].

![Captura de pantalla de la interfaz de usuario de Customer.io que muestra los &quot;logs&quot; de actividad](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* En la interfaz de usuario de Platform, seleccione **[!UICONTROL Ver flujos de datos]** al lado del [!DNL Customer.io] en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]** para verificar los datos introducidos para los eventos seleccionados dentro de [!DNL Customer.io].

![Captura de pantalla de la interfaz de usuario de Platform que muestra eventos ingestados](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
