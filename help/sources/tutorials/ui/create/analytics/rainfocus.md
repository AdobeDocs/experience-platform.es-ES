---
title: Conecte su cuenta de RainFocus a Experience Platform mediante la interfaz de usuario de
description: Aprenda a conectar su cuenta de RainFocus a Experience Platform mediante la interfaz de usuario.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# Conecte su [!DNL RainFocus] cuenta de al Experience Platform mediante la interfaz de usuario de

>[!NOTE]
>
>El [!DNL RainFocus] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona pasos sobre cómo conectar su [!DNL RainFocus] administración de cuentas y eventos de flujo y datos de análisis a Adobe Experience Platform.

>[!IMPORTANT]
>
>Este conector de origen y esta página de documentación los crea y mantiene el [!DNL RainFocus] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en clientcare<span>@rainfocus.com o visite [[!DNL RainFocus] Centro de ayuda](https://help.rainfocus.com/hc/en-us)

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Requisitos previos

Antes de poder conectar su [!DNL RainFocus] cuenta para el Experience Platform, primero debe completar las siguientes tareas previas necesarias:

* [Recopilar credenciales necesarias](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Creación de un esquema XDM y definición del campo de identidad](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Creación de un perfil de integración en RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Una vez completada la configuración de requisitos previos, puede continuar con los pasos descritos a continuación.

## Conecte su cuenta de RainFocus a Experience Platform

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. El *[!UICONTROL Catálogo]* La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *[!UICONTROL Analytics]* categoría, seleccionar **[!UICONTROL Experiencia con RainFocus]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de la interfaz de usuario del Experience Platform con la fuente RainFocus seleccionada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Seleccionar datos

Aparecerá el paso Seleccionar datos, que proporciona una interfaz para que seleccione los datos que trae a Experience Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccionar **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde el sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en el panel Arrastrar y soltar archivos.

Cargar la carga útil JSON de muestra descargada de **RainFocus**.

![El paso Seleccionar datos del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede utilizar la utilidad Buscar campo para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa de datos del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Detalles de flujo de datos

El **Detalles del flujo de datos** Este paso se muestra y le proporciona opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Asignación {#mapping}

Aparecerá el paso Asignación, que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Consulte

El **Revisar** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **Finalizar** y deje pasar un tiempo para crear el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Obtener la URL del extremo de flujo continuo {#get-your-streaming-endpoint-url}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a *[!UICONTROL Actividad de flujo de datos]* página del flujo de datos que acaba de crear y copie el punto final de la parte inferior de la *[!UICONTROL Propiedades]* panel.

![La página de actividad de flujo de datos del espacio de trabajo de fuentes, con la dirección URL del extremo de flujo continuo resaltada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Activar el perfil de integración en RainFocus

Una vez completado el flujo de datos y recuperada la dirección URL del extremo de flujo continuo, ahora puede activar la variable [!DNL Integration Profile] in [!DNL RainFocus].

* Inicie sesión en [[!DNL RainFocus] plataforma](https://app.rainfocus.com). En la navegación principal, seleccione **[!DNL Libraries]** y **[!DNL Integration Profiles]**
* Abra el [!DNL Integration Profile] que creó anteriormente como parte de la [requisitos previos](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Pegue el **ID de flujo de datos** y **Punto final de streaming** copiado del flujo de datos en el Experience Platform y seleccione **Guardar**

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión para su [!DNL RainFocus] fuente, lo que le permite transmitir los datos de análisis y administración de eventos a Experience Platform.

## Recursos adicionales

Los siguientes documentos proporcionan directrices adicionales sobre los matices que rodean a la [!DNL RainFocus] origen.

* [Centro de ayuda de RainFocus](https://help.rainfocus.com/hc/en-us)
* [Creación de una cuenta de servicio de Adobe (JWT) en el portal de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Creación de un esquema en la API](../../../../../xdm/tutorials/create-schema-api.md)
* [Creación de un esquema en la interfaz de usuario](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definición de campos de identidad en la IU](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
