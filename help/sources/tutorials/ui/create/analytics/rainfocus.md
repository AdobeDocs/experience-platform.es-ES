---
title: Conectar su cuenta de RainFocus a Experience Platform mediante la interfaz de usuario
description: Aprenda a conectar su cuenta de RainFocus a Experience Platform mediante la interfaz de usuario de.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# Conecte su cuenta de [!DNL RainFocus] a Experience Platform mediante la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL RainFocus] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Este tutorial proporciona pasos sobre cómo conectar su cuenta de [!DNL RainFocus] y transmitir datos de análisis y administración de eventos a Adobe Experience Platform.

>[!IMPORTANT]
>
>El equipo [!DNL RainFocus] crea y mantiene este conector de origen y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en clientcare<span>@rainfocus.com o visite el [[!DNL RainFocus] Centro de ayuda](https://help.rainfocus.com/hc/en-us)

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Requisitos previos

Para poder conectar su cuenta de [!DNL RainFocus] a Experience Platform, primero debe completar las siguientes tareas previas necesarias:

* [Recopilar credenciales necesarias](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Creación de un esquema XDM y definición del campo de identidad](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Creación de un perfil de integración en RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Una vez completada la configuración de requisitos previos, puede continuar con los pasos descritos a continuación.

## Conecte su cuenta de RainFocus a Experience Platform

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de fuentes. La pantalla *[!UICONTROL Catálogo]* muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *[!UICONTROL Analytics]*, seleccione **[!UICONTROL Experiencia con RainFocus]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de fuentes en la interfaz de usuario de Experience Platform con el origen RainFocus seleccionado.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Seleccionar datos

Aparecerá el paso Seleccionar datos, que proporciona una interfaz para que seleccione los datos que trae a Experience Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccione **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en el panel Arrastrar y soltar archivos.

Cargue la carga útil JSON de muestra descargada de **RainFocus**.

![Paso para seleccionar datos en el flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede utilizar la utilidad Buscar campo para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa de datos del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Detalles del flujo de datos

Aparecerá el paso **Detalle del flujo de datos**, que le proporcionará opciones para usar un conjunto de datos existente o establecer uno nuevo para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de origen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Asignación {#mapping}

Aparecerá el paso Asignación, que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Revisar

Aparece el paso **Revisar**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **Finalizar** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Obtener la URL del extremo de flujo continuo {#get-your-streaming-endpoint-url}

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de flujo se comunique con Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a la página *[!UICONTROL Actividad de flujo de datos]* del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del panel *[!UICONTROL Propiedades]*.

![Página de actividad de flujo de datos en el área de trabajo de orígenes, con la dirección URL de extremo de flujo continuo resaltada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Activar el perfil de integración en RainFocus

Una vez completado el flujo de datos y recuperada la dirección URL de extremo de flujo continuo, puede activar [!DNL Integration Profile] en [!DNL RainFocus].

* Inicie sesión en [[!DNL RainFocus] platform](https://app.rainfocus.com). En la navegación principal, seleccione **[!DNL Libraries]** y **[!DNL Integration Profiles]**
* Abra [!DNL Integration Profile] que creó anteriormente como parte de los [requisitos previos](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Pegue el **ID de flujo de datos** y el **extremo de streaming** copiados del flujo de datos en Experience Platform y seleccione **Guardar**

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión para el origen de [!DNL RainFocus], lo que le permite transmitir los datos de análisis y administración de eventos a Experience Platform.

## Recursos adicionales

Los siguientes documentos proporcionan sugerencias adicionales sobre los matices que rodean el origen de [!DNL RainFocus].

* [Centro de ayuda de RainFocus](https://help.rainfocus.com/hc/en-us)
* [Crear una cuenta de servicio (JWT) de Adobe en el portal de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Creación de un esquema en la API](../../../../../xdm/tutorials/create-schema-api.md)
* [Creación de un esquema en la interfaz de usuario](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definir campos de identidad en la interfaz de usuario](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=es)
