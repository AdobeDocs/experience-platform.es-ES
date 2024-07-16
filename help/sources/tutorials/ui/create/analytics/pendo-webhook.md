---
title: Creación de una conexión de Pendo Source en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Pendo mediante la interfaz de usuario de Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# Crear un flujo de datos de conexión de origen [!DNL Pendo] y en la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL Pendo] está en la versión beta. Lea [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Este tutorial proporciona los pasos para crear una conexión de origen y un flujo de datos de [!DNL Pendo] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Requisitos previos {#prerequisites}

La siguiente sección proporciona información sobre los requisitos previos que se deben completar para poder crear una conexión de origen de [!DNL Pendo].

### Ejemplo de JSON para definir el esquema de origen de [!DNL Pendo] {#prerequisites-json-schema}

Antes de crear una conexión de origen de [!DNL Pendo], necesitará que se proporcione un esquema de origen. Puede utilizar el siguiente JSON.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Para obtener más información, lea la [[!DNL Pendo] guía de webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Crear un esquema de plataforma para [!DNL Pendo] {#create-platform-schema}

También debe asegurarse de crear primero un esquema de Platform para utilizarlo en el origen. Consulte el tutorial de [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para ver los pasos detallados sobre cómo crear un esquema.

![IU de plataforma que muestra un esquema de ejemplo para Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Conectar su cuenta de [!DNL Pendo] {#connect-account}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources] y ver un catálogo de orígenes disponibles en el Experience Platform.

Utilice el menú *[!UICONTROL Categorías]* para filtrar orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la categoría [!UICONTROL Analytics] para ver la tarjeta de origen [!DNL Pendo]. Para empezar, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de origen de la interfaz de usuario de Platform con la tarjeta Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Seleccionar datos {#select-data}

Aparecerá el paso **[!UICONTROL Seleccionar datos]**, que proporciona una interfaz para que pueda seleccionar los datos que desea llevar a Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccione **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en el panel [!UICONTROL Arrastrar y soltar archivos].

![Paso para agregar datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la utilidad [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Detalles del flujo de datos {#dataflow-detail}

Aparecerá el paso **Detalle del flujo de datos**, que le proporcionará opciones para usar un conjunto de datos existente o establecer uno nuevo para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de origen.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Asignación {#mapping}

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

Las asignaciones enumeradas a continuación son obligatorias y deben configurarse antes de continuar con la fase [!UICONTROL Revisar].

| Campo de destino | Descripción |
| --- | --- |
| `uniqueId` | El identificador [!DNL Pendo] del evento. |

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Revisar {#review}

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint-url}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform.

Para construir la dirección URL utilizada para configurar el webhook en [!DNL Pendo], debe recuperar lo siguiente:

* **[!UICONTROL ID de flujo de datos]**
* **[!UICONTROL Extremo de streaming]**

Para recuperar tu **[!UICONTROL ID de flujo de datos]** y **[!UICONTROL extremo de transmisión]**, ve a la página de [!UICONTROL actividad de flujo de datos] del flujo de datos que acabas de crear y copia los detalles desde la parte inferior del panel [!UICONTROL Propiedades].

![Punto final de flujo continuo en la actividad del flujo de datos.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Una vez que haya recuperado su extremo de flujo continuo y el ID de flujo de datos, genere una URL basada en el siguiente patrón: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por ejemplo, una URL de gancho web construida puede tener el siguiente aspecto: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configurar webhook en [!DNL Pendo] {#set-up-webhook}

A continuación, inicia sesión en tu cuenta el [[!DNL Pendo]](https://pendo.io/) y crea un webhook. Para ver los pasos sobre cómo crear un webhook usando la interfaz de usuario de [!DNL Pendo], consulte la [[!DNL Pendo] guía sobre la creación de webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Una vez creado el gancho web, vaya a la página de configuración del gancho web [!DNL Pendo] y escriba la dirección URL del gancho en el campo [!DNL URL].

![Captura de pantalla de la IU Pendo que muestra el campo de extremo del gancho web](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Puede suscribirse a diferentes categorías de eventos para determinar el tipo de eventos que desea enviar desde la instancia de [!DNL Pendo] a Platform. Para obtener más información sobre los diferentes eventos, consulte la [[!DNL Pendo] documentación](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Pasos siguientes {#next-steps}

Al seguir este tutorial, configuró correctamente un flujo de datos de flujo continuo para llevar los datos de [!DNL Pendo] al Experience Platform. Para supervisar los datos que se están ingiriendo, consulte la guía sobre [supervisión de flujos de datos de flujo continuo mediante la interfaz de usuario de Platform](../../monitor-streaming.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al usar el origen [!DNL Pendo].

### Validación {#validation}

Para comprobar que ha configurado correctamente el origen y que se están introduciendo [!DNL Pendo] mensajes, siga los pasos a continuación:

* Puede consultar la página [!DNL Pendo] **[!UICONTROL Informes]** > **[!UICONTROL Historial de chat]** para identificar los eventos que está capturando [!DNL Pendo].

![Captura de pantalla de IU de Pendo que muestra el historial de chat](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* En la interfaz de usuario de Platform, seleccione **[!UICONTROL Ver flujos de datos]** junto al menú de tarjeta [!DNL Pendo] en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]** para verificar los datos introducidos para los enlaces web que ha configurado en [!DNL Pendo].

![Captura de pantalla de IU que muestra eventos ingeridos](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Errores y solución de problemas {#errors-and-troubleshooting}

Al comprobar la ejecución de un flujo de datos, puede que aparezca el siguiente mensaje de error: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Captura de pantalla de IU de Platform que muestra error.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Para corregir este error, debe comprobar que la asignación *uniqueID* esté configurada. Para obtener más instrucciones, consulte la sección [Asignación](#mapping).

Para obtener más información, visite el [[!DNL Pendo] Centro de ayuda](https://www.pendo.io/help-center/).
