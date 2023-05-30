---
title: Creación de una conexión de flujo HTTP API mediante la IU
description: Esta guía de la interfaz de usuario le ayudará a crear una conexión de flujo continuo mediante Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: de721d204cda8e55c72ac5f530b89b2275d94306
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Crear un [!DNL HTTP API] conexión de flujo continuo mediante la IU

En este tutorial se proporcionan los pasos para crear una conexión de origen de flujo continuo utilizando [!UICONTROL Fuentes] workspace.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Creación de una conexión de flujo continuo

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Transmisión]** categoría, seleccionar **[!UICONTROL API HTTP]** y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/http/catalog.png)

El **[!UICONTROL Conectar la cuenta de API HTTP]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta de la API HTTP con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existing-account](../../../../images/tutorials/create/http/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre de cuenta y una descripción opcional. También tendrá la opción de proporcionar las siguientes propiedades de configuración:

- **[!UICONTROL Autenticación]:** Esta propiedad determina si la conexión de flujo continuo requiere autenticación o no. La autenticación garantiza que los datos se recopilen de fuentes de confianza. Si está tratando con información de identificación personal (PII), esta propiedad debe estar activada. De forma predeterminada, esta propiedad está desactivada.
- **[!UICONTROL Compatible con XDM]:** Esta propiedad indica si esta conexión de flujo continuo enviará eventos compatibles con esquemas XDM. De forma predeterminada, esta propiedad está desactivada.

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y luego seleccione **[!UICONTROL Siguiente]** para continuar.

![new-account](../../../../images/tutorials/create/http/new.png)

## Seleccionar datos

Después de crear la conexión de la API HTTP, la variable **[!UICONTROL Seleccionar datos]** Este paso se muestra y le proporciona una interfaz para cargar y previsualizar sus datos.

Seleccionar **[!UICONTROL Cargar archivos]** para cargar los datos. También puede arrastrar y soltar los datos en el [!UICONTROL Arrastrar y soltar archivos] de la interfaz.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con los datos cargados, puede utilizar el lado derecho de la interfaz para obtener una vista previa de la jerarquía de archivos. Seleccionar **[!UICONTROL Siguiente]** para continuar.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Asignación de campos de datos a un esquema XDM

El [!UICONTROL Asignación] Este paso aparece y proporciona una interfaz para asignar los datos de origen a un conjunto de datos de Platform.

El [!DNL HTTP API] source admite la ingesta de archivos JSON. Los archivos JSON no requieren configuración manual si están marcados como quejas de XDM. Si no es así, debe configurar explícitamente la asignación.

Elija un conjunto de datos para los datos de entrada que se van a introducir en. Puede utilizar un conjunto de datos existente o crear uno nuevo.

### Crear un nuevo conjunto de datos

Para crear un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]**. En el formulario que aparece, proporcione el nombre, una descripción opcional, así como el esquema de destino del conjunto de datos. Si selecciona una [!DNL Profile]Un esquema habilitado para, puede elegir si el conjunto de datos también debe ser [!DNL Profile]-habilitado.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Usar un conjunto de datos existente

Para utilizar un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. En el formulario que aparece, seleccione el conjunto de datos que desee utilizar. Una vez que seleccione un conjunto de datos, puede elegir si se debe configurar el conjunto de datos [!DNL Profile]-habilitado.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Asignar campos estándar

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Para añadir un nuevo campo de origen, seleccione **[!UICONTROL Añadir nueva asignación]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Aparece un nuevo emparejamiento de campo de origen y campo de destino. Para añadir un nuevo campo de origen, seleccione el icono de flecha junto a la variable [!UICONTROL Seleccionar campo de origen] barra de entrada.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

El [!UICONTROL Seleccionar atributos] Este panel le permite explorar la jerarquía de archivos y seleccionar un campo de origen específico para asignarlo a un campo XDM de destino. Una vez seleccionado el campo de origen que desea asignar, seleccione **[!UICONTROL Seleccionar]** para continuar.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Con un campo de origen seleccionado, ahora puede identificar el campo XDM de destino adecuado al que asignar. Seleccione el icono de esquema en la sección del campo de destino.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

El [!UICONTROL Asignar campo de origen a campo de destino] aparece una ventana que le proporciona una interfaz para explorar el esquema del conjunto de datos de destinatario. Seleccione el campo de destino que coincida con el campo de origen y, a continuación, seleccione **[!UICONTROL Seleccionar]** para continuar.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Una vez que todos los campos de origen estén asignados a sus campos XDM de destino adecuados, seleccione **[!UICONTROL Siguiente]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Detalles de flujo de datos

El **[!UICONTROL Detalles del flujo de datos]** aparece el paso. En esta página, puede proporcionar detalles para el flujo de datos creado proporcionando un nombre y una descripción opcional.

Después de proporcionar detalles para el flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![data-flow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Consulte

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar los detalles del flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- **[!UICONTROL Conexión]**: Muestra el nombre de la cuenta, la plataforma de origen y el nombre de origen.
- **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra el conjunto de datos de destinatario y el esquema al que se adhiere el conjunto de datos.

Después de confirmar que los detalles son correctos, seleccione **[!UICONTROL Finalizar]**.

![reseña](../../../../images/tutorials/create/http/review.png)

## Obtener URL del extremo de flujo continuo

Con la conexión creada, aparecerá la página de detalles de orígenes. Esta página muestra detalles de la conexión recién creada, incluidos los flujos de datos ejecutados anteriormente, el ID y la URL del extremo de flujo continuo.

![punto final](../../../../images/tutorials/create/http/endpoint.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión HTTP de flujo continuo que le permite utilizar el extremo de flujo continuo para acceder a una variedad de [!DNL Data Ingestion] API. Para obtener instrucciones para crear una conexión de flujo continuo en la API, lea la [tutorial creación de una conexión de flujo continuo](../../../api/create/streaming/http.md).

Para aprender a transmitir datos a Platform, lea cualquiera de los dos tutoriales sobre [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md) o el tutorial sobre [streaming de datos de registro](../../../../../ingestion/tutorials/streaming-record-data.md).
