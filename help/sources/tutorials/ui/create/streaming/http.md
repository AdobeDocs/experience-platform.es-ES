---
title: Creación de una conexión de flujo HTTP API mediante la IU
description: Esta guía de la interfaz de usuario le ayudará a crear una conexión de flujo continuo mediante Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# Crear una conexión de flujo continuo [!DNL HTTP API] mediante la IU

Este tutorial proporciona los pasos para crear una conexión de origen de flujo continuo usando el espacio de trabajo [!UICONTROL Sources].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Creación de una conexión de flujo continuo

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Transmisión]**, seleccione **[!UICONTROL API HTTP]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/http/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de API HTTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, selecciona la cuenta de la API HTTP con la que deseas crear un nuevo flujo de datos y luego selecciona **[!UICONTROL Siguiente]** para continuar.

![cuenta existente](../../../../images/tutorials/create/http/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]**. En el formulario de entrada que aparece, proporcione un nombre de cuenta y una descripción opcional. También tendrá la opción de proporcionar las siguientes propiedades de configuración:

- **[!UICONTROL Autenticación]:** Esta propiedad determina si la conexión de flujo continuo requiere o no autenticación. La autenticación garantiza que los datos se recopilen de fuentes de confianza. Si está tratando con información de identificación personal (PII), esta propiedad debe estar activada. De forma predeterminada, esta propiedad está desactivada.
- **[!UICONTROL Compatible con XDM]:** Esta propiedad indica si esta conexión de flujo continuo enviará eventos compatibles con esquemas XDM. De forma predeterminada, esta propiedad está desactivada.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![nueva cuenta](../../../../images/tutorials/create/http/new.png)

## Seleccionar datos

Después de crear la conexión HTTP API, aparece el paso **[!UICONTROL Seleccionar datos]**, que le proporciona una interfaz para cargar y previsualizar los datos.

Seleccione **[!UICONTROL Cargar archivos]** para cargar los datos. También puede arrastrar y soltar sus datos en la sección [!UICONTROL Arrastrar y soltar archivos] de la interfaz.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con los datos cargados, puede utilizar el lado derecho de la interfaz para obtener una vista previa de la jerarquía de archivos. Seleccione **[!UICONTROL Siguiente]** para continuar.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Asignación de campos de datos a un esquema XDM

Aparecerá el paso [!UICONTROL Mapping], que proporciona una interfaz para asignar los datos de origen a un conjunto de datos de Experience Platform.

El origen [!DNL HTTP API] admite la ingesta de archivos JSON. Los archivos JSON no requieren configuración manual si están marcados como quejas de XDM. Si no es así, debe configurar explícitamente la asignación.

Elija un conjunto de datos para los datos de entrada que se van a introducir en. Puede utilizar un conjunto de datos existente o crear uno nuevo.

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]**. En el formulario que aparece, proporcione el nombre, una descripción opcional, así como el esquema de destino del conjunto de datos. Si selecciona un esquema habilitado para [!DNL Profile], puede elegir si el conjunto de datos también debe estar habilitado para [!DNL Profile].

![nuevo conjunto de datos](../../../../images/tutorials/create/http/new-dataset.png)

### Usar un conjunto de datos existente

Para usar un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. En el formulario que aparece, seleccione el conjunto de datos que desee utilizar. Una vez que seleccione un conjunto de datos, puede elegir si este debería estar habilitado para [!DNL Profile].

![conjunto de datos existente](../../../../images/tutorials/create/http/existing-dataset.png)

### Asignar campos estándar

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

Para agregar un nuevo campo de origen, seleccione **[!UICONTROL Agregar nueva asignación]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Aparece un nuevo emparejamiento de campo de origen y campo de destino. Para agregar un nuevo campo de origen, seleccione el icono de flecha al lado de la barra de entrada [!UICONTROL Seleccionar campo de origen].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

El panel [!UICONTROL Seleccionar atributos] le permite explorar la jerarquía de archivos y seleccionar un campo de origen específico para asignarlo a un campo XDM de destino. Una vez que haya seleccionado el campo de origen que desea asignar, seleccione **[!UICONTROL Seleccionar]** para continuar.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Con un campo de origen seleccionado, ahora puede identificar el campo XDM de destino adecuado al que asignar. Seleccione el icono de esquema en la sección del campo de destino.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Aparecerá la ventana [!UICONTROL Asignar campo de origen al campo de destino], que le proporcionará una interfaz para explorar el esquema del conjunto de datos de destino. Seleccione el campo de destino que coincida con el campo de origen y, a continuación, seleccione **[!UICONTROL Seleccionar]** para continuar.

![campo de asignación a destino](../../../../images/tutorials/create/http/map-to-target-field.png)

Una vez que todos los campos de origen estén asignados a los campos XDM de destino correspondientes, seleccione **[!UICONTROL Siguiente]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Detalles del flujo de datos

Aparece el paso **[!UICONTROL Detalle del flujo de datos]**. En esta página, puede proporcionar detalles para el flujo de datos creado proporcionando un nombre y una descripción opcional.

Después de proporcionar detalles para el flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![detalle de flujo de datos](../../../../images/tutorials/create/http/dataflow-detail.png)

## Revisar

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar los detalles del flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- **[!UICONTROL Conexión]**: muestra el nombre de cuenta, la plataforma de origen y el nombre de origen.
- **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra el conjunto de datos de destino y el esquema al que se adhiere el conjunto de datos.

Después de confirmar que los detalles son correctos, seleccione **[!UICONTROL Finalizar]**.

![revisión](../../../../images/tutorials/create/http/review.png)

## Obtener URL del extremo de flujo continuo

Con la conexión creada, aparecerá la página de detalles de orígenes. Esta página muestra detalles de la conexión recién creada, incluidos los flujos de datos ejecutados anteriormente, el ID y la URL del extremo de flujo continuo.

![extremo](../../../../images/tutorials/create/http/endpoint.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión HTTP de flujo continuo que le permite utilizar el extremo de flujo continuo para acceder a una variedad de API de [!DNL Data Ingestion]. Para obtener instrucciones para crear una conexión de flujo continuo en la API, lea el [tutorial sobre la creación de una conexión de flujo continuo](../../../api/create/streaming/http.md).

Para aprender a transmitir datos a Experience Platform, lea el tutorial sobre [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md) o el tutorial sobre [transmisión de datos de registros](../../../../../ingestion/tutorials/streaming-record-data.md).
