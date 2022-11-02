---
keywords: conectar destino;conexión de destino;cómo conectar destino
title: Crear una nueva conexión de destino
type: Tutorial
description: Obtenga información sobre cómo conectarse a un destino en Adobe Experience Platform, habilitar alertas y configurar acciones de marketing para el destino conectado.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Crear una nueva conexión de destino

>[!IMPORTANT]
> 
>* Para conectarse a un destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para conectarse a un destino que admita exportaciones de conjuntos de datos, necesita la variable **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.


## Información general {#overview}

Para poder enviar datos de audiencia a un destino, debe configurar una conexión con la plataforma de destino. Este artículo muestra cómo configurar una nueva conexión de destino, a la que puede activar segmentos o exportar conjuntos de datos mediante la interfaz de usuario de Adobe Experience Platform.

## Buscar el destino deseado en el catálogo {#setup}

1. Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña .

   ![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la página del catálogo de destinos.](../assets/ui/connect-destinations/catalog.png)

2. Las tarjetas de destino del catálogo pueden tener diferentes controles de acción, en función de si tiene una conexión existente con el destino y de si los destinos admiten la activación de segmentos, la exportación de conjuntos de datos o ambos. Puede ver cualquiera de los siguientes controles para tarjetas de destino:

   * **[!UICONTROL Configuración]**. Una conexión primero debe configurarse en este destino para poder activar segmentos o exportar conjuntos de datos.
   * **[!UICONTROL Activar]**. Ya se ha configurado una conexión con este destino. Este destino admite la activación de segmentos y las exportaciones de conjuntos de datos.
   * **[!UICONTROL Activar segmentos]**. Ya se ha configurado una conexión con este destino. Este destino solo admite la activación de segmentos.

   Para obtener más información sobre la diferencia entre estos controles, también puede consultar la [Catálogo](../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

   Seleccione: **[!UICONTROL Configuración]**, **[!UICONTROL Activar]** o **[!UICONTROL Activar segmentos]**, según el control que esté disponible.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform, que muestra la página del catálogo de destinos con el control Configurar resaltado.](../assets/ui/connect-destinations/set-up.png)

   ![Captura de pantalla de la interfaz de usuario del Experience Platform, que muestra la página del catálogo de destinos con el control Activate segments resaltado.](../assets/ui/connect-destinations/activate-segments.png)

3. Si ha seleccionado **[!UICONTROL Configuración]**, vaya al paso siguiente, para [autenticar](#authenticate) al destino.

   Si ha seleccionado **[!UICONTROL Activar]**, **[!UICONTROL Activar segmentos]** o **[!UICONTROL Exportación de conjuntos de datos]**, ahora puede ver una lista de conexiones de destino existentes.

   Select **[!UICONTROL Configurar nuevo destino]** para establecer una nueva conexión con el destino.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform, que muestra una lista de los destinos disponibles y el control Configure new destination resaltado.](../assets/ui/connect-destinations/configure-new-destination.png)

## Autenticar en destino {#authenticate}

El primer paso para conectarse a un destino es autenticarse en la plataforma de destino.

Según el destino al que se conecte, se le puede llevar a la página del socio de destino para autenticarse o se le puede pedir que introduzca las credenciales de autenticación directamente en el flujo de trabajo de Platform. A continuación se muestra un ejemplo de la entrada necesaria para autenticarse en un [!DNL Amazon S3] destino. En cada página de documentación de destino se proporcionan instrucciones detalladas sobre la entrada necesaria (consulte, por ejemplo, la sección de autenticación de [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) y para [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parámetros de autenticación opcionales y requeridos**

![Imagen que muestra los parámetros de entrada opcionales y requeridos al autenticarse en un destino de Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Configuración de parámetros de conexión {#set-up-connection-parameters}

Si ya ha configurado la autenticación en el destino, puede continuar con la cuenta existente o configurar una nueva cuenta.

En función del destino al que se conecte, se le puede pedir que introduzca diferentes tipos de parámetros de conexión. Por ejemplo, al conectarse a un [!DNL Amazon S3] destino, se le pedirá que proporcione detalles sobre el [!DNL Amazon S3] nombre del contenedor y ruta de carpeta donde se depositarán los archivos. A continuación se muestran dos ejemplos de entradas necesarias para un [!DNL Amazon S3] destino y [!DNL Trade Desk] destino. En cada página de documentación de destino se proporcionan instrucciones detalladas sobre la entrada necesaria.

>[!IMPORTANT]
>
>Las imágenes siguientes se utilizan únicamente con fines ilustrativos. Los detalles de la conexión de destino varían según el destino. Para obtener información detallada sobre los detalles de conexión de su destino, lea la **Conectarse al destino** en cada [catálogo de destino](../catalog/overview.md) (por ejemplo, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)o [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parámetros de entrada opcionales y requeridos**

![Imagen que muestra los parámetros de entrada opcionales y requeridos al conectarse a un destino de Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parámetros de entrada opcionales y requeridos**

![Imagen que muestra los parámetros de entrada opcionales y requeridos al conectarse a un destino de centro de comercio.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Configurar las opciones de formato de archivo para los archivos exportados {#file-formatting-and-compression-options}

Para los destinos basados en archivos, puede configurar varias opciones relacionadas con el formato y la compresión de los archivos exportados. Para obtener más información sobre todas las opciones de formato y compresión disponibles, lea la [Tutorial sobre la configuración de opciones de formato de archivo para destinos basados en archivos](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Imagen que muestra la selección del tipo de archivo y las distintas opciones para los archivos CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Configurar la conexión de destino para la activación de segmentos o las exportaciones de conjuntos de datos {#segment-activation-or-dataset-exports}

Algunos destinos basados en archivos admiten la activación de segmentos, así como las exportaciones de conjuntos de datos. Para estos destinos, puede elegir si crear una conexión que le permita activar segmentos o exportar conjuntos de datos.

![Imagen que muestra el control de selección de tipo de datos que permite a los usuarios seleccionar entre la activación de segmentos y las exportaciones de conjuntos de datos.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Habilitar alertas de destino {#enable-alerts}

1. (Opcional) Seleccione las alertas de flujo de datos de destino a las que desee suscribirse. Puede suscribirse a las alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo. Las alertas disponibles difieren según el tipo de destino (basado en archivos o flujo) al que se esté conectando. Lectura [Suscripción a alertas de destino en contexto](alerts.md) para obtener información detallada sobre las alertas de flujo de datos de destino.

   ![El cuadro de diálogo Configurar nuevo destino con las opciones de suscripción de alertas de destino en contexto resaltadas.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Seleccione **[!UICONTROL Siguiente]**.

   ![El cuadro de diálogo Configurar nuevo destino con el control Siguiente resaltado, que permite al usuario continuar con el paso siguiente en el flujo de trabajo.](../assets/ui/connect-destinations/next.png)

## Seleccionar acciones de marketing {#select-marketing-actions}

1. Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la [información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md) página.

   ![El cuadro de diálogo Configurar nuevo destino con las acciones de marketing disponibles resaltadas. También se resaltan los controles disponibles para completar el flujo de trabajo Conectar con destino .](../assets/ui/connect-destinations/governance.png)

2. Select **[!UICONTROL Guardar y salir]** para guardar la configuración de destino o seleccione **[!UICONTROL Siguiente]** para continuar con los datos de audiencia [flujo de activación](activation-overview.md).

## Pasos siguientes {#next-steps}

Al leer este documento, ha aprendido a utilizar la interfaz de usuario del Experience Platform para establecer una conexión con un destino. Como recordatorio, los parámetros de conexión disponibles y requeridos varían de un destino a otro. También debe consultar la página de documentación de destino en la [catálogo de destinos](/help/destinations/catalog/overview.md) para obtener información específica sobre las entradas necesarias y las opciones disponibles por tipo de destino.

A continuación, puede continuar con [activación de segmentos](/help/destinations/ui/activation-overview.md) o [exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md) a su destino.