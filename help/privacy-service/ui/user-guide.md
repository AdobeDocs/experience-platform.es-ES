---
keywords: Experience Platform;inicio;temas populares;exportar;Exportar
solution: Experience Platform
title: Guía del usuario del Privacy Service
topic: UI guide
description: Obtenga información sobre cómo utilizar la interfaz de usuario de Privacy Service para coordinar y supervisar las solicitudes de privacidad en diversas aplicaciones de Experience Cloud.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---


# [!DNL Privacy Service] Guía del usuario

Este documento proporciona los pasos para crear y administrar solicitudes de privacidad mediante la interfaz de usuario [!DNL Privacy Service].

## Examinar el panel de la interfaz de usuario [!DNL Privacy Service]

El panel de la interfaz de usuario [!DNL Privacy Service] proporciona dos utilidades que le permiten realizar la vista del estado de sus trabajos de privacidad: &quot;[!UICONTROL Informe de estado]&quot; y &quot;[!UICONTROL Solicitudes de trabajo]&quot;. El panel también muestra la regulación seleccionada actual para los trabajos mostrados.

![PANEL de la interfaz de usuario](../images/user-guide/dashboard.png)

### Tipo de regulación

[!DNL Privacy Service] admite solicitudes de trabajo para varias regulaciones de privacidad:

* El [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* La Unión Europea [!DNL General Data Protection Regulation] ([!UICONTROL RGPD])
* Tailandia [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brasil [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Nueva Zelanda [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Los trabajos para cada tipo de regulación se rastrean por separado. Para cambiar entre tipos de regulación, seleccione el menú desplegable **[!UICONTROL Tipo de regulación]** y seleccione la regulación deseada en la lista.

![Lista desplegable Tipo de regulación](../images/user-guide/regulation.png)

Al cambiar el tipo de regulación, el panel se actualiza para mostrar todas las operaciones, filtros, utilidades y diálogos de creación de empleo que se aplican a la regulación seleccionada.

![Panel actualizado](../images/user-guide/dashboard-update.png)

### Informe de estado

El gráfico de la parte izquierda del widget de informe de estado realiza un seguimiento de los trabajos enviados en relación con cualquier trabajo que haya informado de errores. El gráfico de la derecha rastrea los trabajos cerca del final de la ventana de cumplimiento de 30 días.

Seleccione uno de los dos botones de alternancia que hay encima del gráfico para mostrar u ocultar sus métricas respectivas.

![](../images/user-guide/hide-errors.png)

Puede vista el número exacto de trabajos asociados con cualquier punto de datos de los gráficos pasando el ratón sobre el punto de datos en cuestión.

![Puntos de datos de pasar el ratón por encima](../images/user-guide/mouse-over.png)

Para vista de más detalles sobre un punto de datos determinado, seleccione el punto de datos en cuestión para mostrar los trabajos asociados en la utilidad Solicitudes de trabajo. Tenga en cuenta el filtro que se aplica justo encima de la lista de trabajo.

![Filtro aplicado desde la utilidad](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Cuando se ha aplicado un filtro al widget de solicitudes de trabajo, puede eliminarlo seleccionando la **X** en la píldora de filtro. Las solicitudes de trabajo luego vuelven a la lista de seguimiento predeterminada.

### Solicitudes de trabajo

El widget de solicitudes de trabajo lista todas las solicitudes de trabajo disponibles en la organización, incluidos detalles como el tipo de solicitud, el estado actual, la fecha de vencimiento y el correo electrónico del solicitante.

>[!NOTE]
>
>Los datos de los trabajos creados anteriormente solo son accesibles durante 30 días después de la fecha de finalización.

Puede filtrar la lista escribiendo las palabras clave en la barra de búsqueda debajo del título de las solicitudes de trabajo. La lista filtros automáticamente a medida que escribe, mostrando las solicitudes que contienen valores que coinciden con los términos de búsqueda. También puede utilizar el menú desplegable **[!UICONTROL Solicitado en]** para seleccionar un intervalo de tiempo para los trabajos enumerados.

![Opciones de búsqueda de solicitud de trabajo](../images/user-guide/job-search.png)

Para vista de los detalles de una solicitud de trabajo en particular, seleccione la ID de trabajo de la solicitud en la lista para abrir la página **[!UICONTROL Detalles del trabajo]**.

![Detalles del trabajo de la interfaz de usuario de GDPR](../images/user-guide/job-details.png)

Este cuadro de diálogo contiene información de estado sobre cada solución [!DNL Experience Cloud] y su estado actual en relación con el trabajo general. Dado que cada trabajo de privacidad es asincrónico, la página muestra la fecha y hora de comunicación más reciente (GMT) de cada solución, ya que algunos requieren más tiempo que otros para procesar la solicitud.

Si una solución ha proporcionado datos adicionales, se puede ver en este cuadro de diálogo. Puede vista de estos datos seleccionando filas de productos individuales.

Para descargar los datos completos del trabajo como archivo CSV, seleccione **[!UICONTROL Exportar a CSV]** en la parte superior derecha del cuadro de diálogo.

## Crear una nueva solicitud de trabajo de privacidad

>[!NOTE]
>
>Para crear una solicitud de trabajo de privacidad, debe proporcionar información de identidad para los clientes específicos cuyos datos se van a obtener o eliminar. Revise el documento de [datos de identidad para solicitudes de privacidad](../identity-data.md) antes de continuar con esta sección.

La interfaz de usuario [!DNL Privacy Service] proporciona dos métodos para crear nuevas solicitudes de trabajo:

* [Uso del Generador de solicitudes](#request-builder)
* [Cargar un archivo JSON](#json)

Los pasos para utilizar cada uno de estos métodos se proporcionan en las siguientes secciones.

### Utilizar el Generador de solicitudes {#request-builder}

Con el Creador de solicitudes, puede crear manualmente una nueva solicitud de trabajo de privacidad en la interfaz de usuario. El Generador de solicitudes se utiliza mejor para conjuntos de solicitudes más simples y pequeños, ya que el Generador de solicitudes limita las solicitudes para que solo tengan un tipo de ID por usuario. Para solicitudes más complicadas, es mejor [cargar un archivo JSON](#json) en su lugar.

Para realizar inicios con el generador de solicitudes, seleccione **[!UICONTROL Crear solicitud]** debajo del widget de informe de estado en el lado derecho de la pantalla.

![Seleccionar Crear solicitud](../images/user-guide/create-request.png)

Se abre el cuadro de diálogo **[!UICONTROL Crear solicitud]**, que muestra las opciones disponibles para enviar una solicitud de trabajo de privacidad para el tipo de regulación seleccionado actualmente.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Seleccione el **[!UICONTROL Tipo de trabajo]** de la solicitud (&quot;Eliminar&quot; o &quot;Acceso&quot;) y uno o más productos disponibles de la lista.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

En **[!UICONTROL tipo de Área de nombres]**, seleccione el tipo de Área de nombres apropiado para los ID de cliente que se envían a [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Cuando utilice el tipo de Área de nombres estándar, seleccione una Área de nombres en el menú desplegable (correo electrónico, ECID o AAID) y, a continuación, escriba los valores de ID en el cuadro de texto a la derecha, presionando **\&lt;enter>** para que cada ID se agregue a la lista.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Al utilizar el tipo de Área de nombres personalizada, debe escribir manualmente la Área de nombres antes de proporcionar los valores de ID siguientes.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Cuando termine, seleccione **[!UICONTROL Crear]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

El cuadro de diálogo desaparece y el nuevo trabajo (o trabajos) aparece en la utilidad Solicitudes de trabajo junto con su estado de procesamiento actual.

### Cargar un archivo JSON {#json}

Al crear solicitudes más complicadas, como las que utilizan varios tipos de ID para cada asunto de datos que se está procesando, puede crear una solicitud cargando un archivo JSON.

Seleccione la flecha junto a **[!UICONTROL Crear solicitud]**, debajo del widget de informe de estado en el lado derecho de la pantalla. En la lista de opciones que aparece, seleccione **[!UICONTROL Cargar JSON]**.

![Opciones de creación de solicitudes](../images/user-guide/create-options.png)

Aparece el cuadro de diálogo **[!UICONTROL Cargar JSON]**, que proporciona una ventana para arrastrar y soltar el archivo JSON.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Si no tiene un archivo JSON para cargar, seleccione **[!UICONTROL Descargar Adobe-GDPR-Request.json]** para descargar una plantilla que puede rellenar según los valores recopilados de los temas de datos.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Busque el archivo JSON en el equipo y arrástrelo a la ventana de diálogo. Si la carga se realiza correctamente, el nombre del archivo aparecerá en el cuadro de diálogo. Puede seguir agregando más archivos JSON según sea necesario arrastrándolos y soltándolos en el cuadro de diálogo.

Cuando termine, seleccione **[!UICONTROL Crear]**. El cuadro de diálogo desaparece y el nuevo trabajo (o trabajos) aparece en la utilidad Solicitudes de trabajo junto con su estado de procesamiento actual.

### Pasos siguientes

Al leer este documento, ha aprendido a utilizar la [!DNL Privacy Service] interfaz de usuario para crear un trabajo de privacidad, vista de los detalles de un trabajo y supervisión de su estado de procesamiento, y descargar los resultados una vez que se haya completado.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante la API [!DNL Privacy Service], consulte la [guía para desarrolladores](../api/getting-started.md).