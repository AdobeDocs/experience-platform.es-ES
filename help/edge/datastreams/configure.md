---
title: Configurar una secuencia de datos
description: Obtenga información sobre cómo conectar la integración del SDK web del lado del cliente con otros productos de Adobe y destinos de terceros.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 611b80f2444ea86ef008f761c5d46976c55b864d
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 3%

---

# Configurar una secuencia de datos

Este documento cubre los pasos para configurar un [datastream](./overview.md) en la interfaz de usuario de .

## Acceda a la [!UICONTROL Datastreams] workspace

Puede crear y administrar conjuntos de datos en la interfaz de usuario o la interfaz de usuario del Experience Platform de la recopilación de datos seleccionando **[!UICONTROL Datastreams]** en el panel de navegación izquierdo.

![Ficha Datastreams en la interfaz de usuario de la recopilación de datos](../assets/datastreams/configure/datastreams-tab.png)

La variable **[!UICONTROL Datastreams]** muestra una lista de conjuntos de datos existentes, que incluye su nombre descriptivo, ID y fecha de la última modificación. Seleccione el nombre de un conjunto de datos para [ver sus detalles y configurar servicios](#view-details).

Seleccione el icono &quot;more&quot; (**...**) para un conjunto de datos específico para mostrar más opciones. Select **[!UICONTROL Editar]** para actualizar el [configuración básica](#configure) para el conjunto de datos, o seleccione **[!UICONTROL Eliminar]** para eliminar el conjunto de datos.

![Opciones para editar o eliminar un conjunto de datos existente](../assets/datastreams/configure/edit-datastream.png)

## Crear un nuevo conjunto de datos {#create}

Para crear un conjunto de datos, comience seleccionando **[!UICONTROL Nuevo conjunto de datos]**.

![Seleccione Nueva secuencia de datos](../assets/datastreams/configure/new-datastream-button.png)

Aparecerá el flujo de trabajo de creación del conjunto de datos, empezando por el paso de configuración. A partir de aquí, debe proporcionar un nombre y una descripción opcional para el conjunto de datos.

Si está configurando este conjunto de datos para utilizarlo en Experience Platform y utiliza el SDK web de plataforma, también debe seleccionar una [esquema del Modelo de datos de experiencias (XDM) basado en eventos](../../xdm/classes/experienceevent.md) para representar los datos que planea introducir.

![Configuración básica de un conjunto de datos](../assets/datastreams/configure/configure.png)

Select **[!UICONTROL Opciones avanzadas]** para mostrar controles adicionales para configurar el conjunto de datos.

![Opciones de configuración avanzadas](../assets/datastreams/configure/advanced-options.png) {#advanced-options}

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Ubicación geográfica] | Determina si se producen búsquedas de geolocalización en función de la dirección IP del usuario. La configuración predeterminada **[!UICONTROL Ninguna]** deshabilita las búsquedas de geolocalización, mientras que la variable **[!UICONTROL Ciudad]** proporciona coordenadas GPS a dos decimales. La geolocalización se produce antes de que [!UICONTROL Confusión de IP] y no se ve afectado por el  [!UICONTROL Confusión de IP] configuración. |
| [!UICONTROL Confusión de IP] | Indica el tipo de confusión de IP que se aplicará al conjunto de datos. Cualquier procesamiento basado en la IP del cliente se verá afectado por la configuración de confusión de IP. Esto incluye todos los servicios de Experience Cloud que reciben datos de su conjunto de datos. <p>Opciones disponibles:</p> <ul><li>**[!UICONTROL Ninguna]**: Desactiva la confusión de IP. La dirección IP completa del usuario se enviará mediante el conjunto de datos.</li><li>**[!UICONTROL Parcial]**: Para las direcciones IPv4, confunde el último octeto de la dirección IP del usuario. Para las direcciones IPv6, confunde los últimos 80 bits de la dirección. <p>Ejemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Completa]**: Protege toda la dirección IP. <p>Ejemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `::/128`</li></ul></li></ul> Impacto de la confusión de IP en otros productos de Adobe: <ul><li>**Adobe Target**: El nivel del conjunto de datos [!UICONTROL Confusión de IP] tiene prioridad sobre cualquier opción de confusión de IP establecida en Adobe Target. Por ejemplo, si el nivel del conjunto de datos [!UICONTROL Confusión de IP] está configurada en **[!UICONTROL Completa]** y la opción de confusión de IP de Adobe Target está establecida en **[!UICONTROL Confusión de último octeto]**, Adobe Target recibirá una IP totalmente ofuscada. Consulte la documentación de Adobe Target en [Confusión de IP](https://developer.adobe.com/target/before-implement/privacy/privacy/) y [geolocalización](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=en) para obtener más información.</li><li>**Audience Manager**: La configuración de confusión de IP a nivel de almacén de datos tiene prioridad sobre cualquier opción de confusión de IP establecida en Audience Manager y se aplica a todas las direcciones IP. Cualquier búsqueda de geolocalización realizada por el Audience Manager se ve afectada por el nivel del conjunto de datos [!UICONTROL Confusión de IP] . Una búsqueda de geolocalización en Audience Manager, basada en una IP totalmente ofuscada, resultará en una región desconocida y cualquier segmento basado en los datos de geolocalización resultantes no se realizará. Consulte la documentación del Audience Manager en [Confusión de IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=en) para obtener más información.</li><li>**Adobe Analytics**: Los datos enviados a Adobe Analytics no se ven afectados por el nivel del conjunto de datos [!UICONTROL Confusión de IP] configuración. Actualmente, Adobe Analytics recibe direcciones IP sin confusión. Para que Analytics reciba direcciones IP ofuscadas, debe configurar la confusión de IP por separado en Adobe Analytics. Este comportamiento se actualizará en futuras versiones. Consulte Adobe Analytics [documentación](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) para obtener más información sobre cómo habilitar la confusión de IP en Analytics.</li></ul> |
| [!UICONTROL Cookie de ID de origen] | Cuando está habilitada, esta configuración indica a la red perimetral que haga referencia a una cookie especificada al buscar una [ID de dispositivo de origen](../identity/first-party-device-ids.md), en lugar de buscar este valor en el mapa de identidad.<br><br>Al habilitar esta configuración, debe proporcionar el nombre de la cookie en la que se espera que se almacene el ID. |
| [!UICONTROL Sincronización de ID de terceros] | Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que diferentes sincronizaciones de ID se ejecuten en momentos diferentes. Cuando está habilitada, esta configuración le permite especificar qué contenedor de sincronizaciones de ID se ejecuta para este conjunto de datos. |
| [!UICONTROL Tipo de acceso] | Define el tipo de autenticación que acepta la red perimetral para el conjunto de datos. <ul><li>**[!UICONTROL Autenticación mixta]**: Cuando se selecciona esta opción, la red perimetral acepta solicitudes autenticadas y no autenticadas. Seleccione esta opción cuando desee utilizar el SDK web o [SDK móvil](https://aep-sdks.gitbook.io/docs/), junto con la variable [API de servidor](../../server-api/overview.md). </li><li>**[!UICONTROL Solo autenticado]**: Cuando se selecciona esta opción, la red perimetral solo acepta solicitudes autenticadas. Seleccione esta opción cuando vaya a utilizar solo la API de servidor y desee evitar que la red perimetral procese solicitudes no autenticadas.</li></ul> |

A partir de aquí, si va a configurar el conjunto de datos para el Experience Platform, siga el tutorial en [Preparación de datos para la recopilación de datos](./data-prep.md) para asignar los datos a un esquema de eventos de Platform antes de volver a esta guía. De lo contrario, seleccione **[!UICONTROL Guardar]** y continúe con la siguiente sección.

## Ver detalles del almacén de datos {#view-details}

Después de configurar un nuevo conjunto de datos o de seleccionar uno existente para verlo, aparecerá la página de detalles de ese conjunto de datos. Aquí puede encontrar más información sobre el conjunto de datos, incluido su ID.

![Página de detalles de un conjunto de datos creado](../assets/datastreams/configure/view-details.png)

Desde la pantalla de detalles del almacén de datos, puede [agregar servicios](#add-services) para habilitar las funcionalidades de los productos de Adobe Experience Cloud a los que tiene acceso. También puede editar el [configuración básica](#create), actualice su [reglas de asignación](./data-prep.md), [copiar el conjunto de datos](#copy)o elimínelo por completo.

## Añadir servicios a un conjunto de datos {#add-services}

En la página de detalles de un conjunto de datos, seleccione **[!UICONTROL Añadir servicio]** para empezar a añadir servicios disponibles para ese conjunto de datos.

![Seleccione Añadir servicio para continuar](../assets/datastreams/configure/add-service.png)

En la siguiente pantalla, utilice el menú desplegable para seleccionar un servicio de configuración para este conjunto de datos. En esta lista solo aparecen los servicios a los que tiene acceso.

![Seleccionar un servicio de la lista](../assets/datastreams/configure/service-selection.png)

Seleccione el servicio deseado, rellene las opciones de configuración que aparecen y, a continuación, seleccione **[!UICONTROL Guardar]** para agregar el servicio al conjunto de datos. Todos los servicios añadidos aparecen en la vista de detalles del conjunto de datos.

![Servicios agregados a un conjunto de datos](../assets/datastreams/configure/services-added.png)

Las subsecciones siguientes describen las opciones de configuración de cada servicio.

>[!NOTE]
>
>Cada configuración de servicio contiene un **[!UICONTROL Habilitado]** que se activa automáticamente cuando se selecciona el servicio. Para desactivar el servicio seleccionado para este conjunto de datos, seleccione el **[!UICONTROL Habilitado]** volver a alternar.

### Configuración de Adobe Analytics {#analytics}

Este servicio controla si los datos se envían a Adobe Analytics y cómo se hacen. Encontrará más detalles en la guía de [envío de datos a Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](../assets/datastreams/configure/analytics-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL ID del grupo de informes] | **(Obligatorio)** El ID del grupo de informes de Analytics al que desea enviar los datos. Este ID se puede encontrar en la interfaz de usuario de Adobe Analytics, en [!UICONTROL Administrador] > [!UICONTROL Grupos de informes]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes. |

### Configuración de Adobe Audience Manager {#audience-manager}

Este servicio controla si los datos se envían a Adobe Audience Manager y cómo se hacen. Todo lo que se necesita para enviar datos al Audience Manager es habilitar esta sección. Los demás ajustes son opcionales, pero se recomienda.

![Bloque de configuración de Audience Manager de Adobe](../assets/datastreams/configure/audience-manager-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Destinos de cookies habilitados] | Permite al SDK compartir información de segmentos mediante [destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) from [!DNL Audience Manager]. |
| [!UICONTROL Destinos de URL habilitados] | Permite al SDK compartir información de segmentos mediante [Destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) from [!DNL Audience Manager]. |

### Configuración de Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Al habilitar un conjunto de datos para Platform, tome nota del simulador de pruebas de Platform que está utilizando actualmente, tal y como se muestra en la cinta superior de la interfaz de usuario.
>
>![Espacio aislado seleccionado](../assets/datastreams/configure/platform-sandbox.png)
>
>Los entornos limitados son particiones virtuales en Adobe Experience Platform que le permiten aislar los datos y las implementaciones de otras personas de su organización. Una vez creado un conjunto de datos, su simulador de pruebas no se puede cambiar. Para obtener más información sobre la función de los entornos limitados en el Experience Platform, consulte la [documentación de entornos limitados](../../sandboxes/home.md).

Este servicio controla si los datos se envían a Adobe Experience Platform y cómo se hacen.

![Bloque de configuración de Adobe Experience Platform](../assets/datastreams/configure/platform-config.png)

| Configuración | Descripción |
|---| --- |
| [!UICONTROL Conjunto de datos del evento] | **(Obligatorio)** Seleccione el conjunto de datos de Platform al que se transmitirán los datos de eventos del cliente. Este esquema debe utilizar la variable [Clase XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Conjunto de datos de perfil] | Seleccione el conjunto de datos de Platform al que se enviarán los datos de atributos del cliente. Este esquema debe utilizar la variable [Clase de perfil individual XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Seleccione esta casilla de verificación para habilitar el Offer decisioning para una implementación del SDK web de Platform. Consulte la guía de [uso del Offer decisioning con el SDK web de Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) para obtener más información sobre la implementación.<br><br>Para obtener más información sobre las funciones de Offer decisioning, consulte la [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=es). |
| [!UICONTROL Segmentación de Edge] | Active esta casilla de verificación para habilitar [segmentación de arista](../../segmentation/ui/edge-segmentation.md) para este conjunto de datos. Cuando el SDK envía datos a través de un conjunto de datos habilitado para la segmentación perimetral, cualquier pertenencia de segmento actualizada para el perfil en cuestión se devuelve en la respuesta.<br><br>Esta opción se puede utilizar en combinación con [!UICONTROL Destinos de personalización] para [casos de uso de personalización de páginas siguientes](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinos de personalización] | Al habilitar esto después de habilitar la variable [!UICONTROL Segmentación de Edge] , esta opción permite que el conjunto de datos se conecte a destinos de personalización, como [Personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md).<br><br>Consulte la documentación de destinos para ver los pasos específicos sobre [configuración de destinos de personalización](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Active esta casilla de verificación para habilitar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) para este conjunto de datos. <br><br> Al habilitar esta opción, el conjunto de datos puede devolver contenido personalizado de las campañas de entrada web y basadas en aplicaciones en [!DNL Adobe Journey Optimizer]. Esta opción requiere [!UICONTROL Segmentación de Edge] para estar activo. If [!UICONTROL Segmentación de Edge] está desactivada, esta opción está atenuada. |

### Configuración de Adobe Target {#target}

Este servicio controla si los datos se envían a Adobe Target y cómo se hacen.

![Bloque de configuración de Adobe Target](../assets/datastreams/configure/target-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Token de propiedad] | [!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Para obtener más información sobre las propiedades, consulte la guía de [configuración de permisos de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es) en el [!DNL Target] documentación.<br><br>El token de propiedad se puede encontrar en la interfaz de usuario de Adobe Target, en [!UICONTROL Configuración] > [!UICONTROL Propiedades]. |
| [!UICONTROL ID de entorno de Target] | [Entornos en Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) le ayuda a administrar su implementación en todas las etapas de desarrollo. Esta configuración especifica el entorno que se va a utilizar con este conjunto de datos.<br><br>Una práctica recomendada es configurar esto de forma diferente para cada uno de sus `dev`, `stage`y `prod` entornos de datastream para mantener las cosas simples. Sin embargo, si ya tiene definidos entornos de Adobe Target, puede utilizarlos. |
| [!UICONTROL Área de nombres de ID de terceros de Target] | El área de nombres de identidad para la variable `mbox3rdPartyId` desea usar para este conjunto de datos. Consulte la guía de [implementación `mbox3rdPartyId` con el SDK web](../personalization/adobe-target/using-mbox-3rdpartyid.md) para obtener más información. |

### [!UICONTROL Reenvío de eventos] configuración

Este servicio controla si los datos se envían a [reenvío de eventos](../../tags/ui/event-forwarding/overview.md).

![Sección Reenvío de eventos de la interfaz de usuario de configuración](../assets/datastreams/configure/event-forwarding-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Propiedad Launch] | **(Obligatorio)** La propiedad de reenvío de eventos a la que desea enviar datos. |
| [!UICONTROL Entorno de Launch] | **(Obligatorio)** El entorno dentro de la propiedad seleccionada al que desea enviar los datos. |

>[!NOTE]
>
>Puede seleccionar **[!UICONTROL Introducir ID manualmente]** para escribir los nombres de propiedad y entorno en lugar de usar los menús desplegables.

## Copiar un conjunto de datos {#copy}

Puede crear una copia de un conjunto de datos existente y modificar sus detalles según sea necesario.

>[!NOTE]
>
>Los conjuntos de datos solo se pueden copiar dentro del mismo [entorno limitado](../../sandboxes/home.md). En otras palabras, no se puede copiar un conjunto de datos de un entorno limitado a otro.

Desde la página principal en la [!UICONTROL Datastreams] espacio de trabajo, seleccione los puntos suspensivos (**....**) para el conjunto de datos en cuestión, seleccione **[!UICONTROL Copiar]**.

![Imagen que muestra la variable [!UICONTROL Copiar] opción seleccionada en la vista de lista del conjunto de datos](../assets/datastreams/configure/copy-datastream-list.png)

También puede seleccionar **[!UICONTROL Copiar conjunto de datos]** de la vista de detalles de un conjunto de datos determinado.

![Imagen que muestra la variable [!UICONTROL Copiar] opción seleccionada en la vista de detalles del conjunto de datos](../assets/datastreams/configure/copy-datastream-details.png)

Aparecerá un cuadro de diálogo de confirmación en el que se le pedirá que proporcione un nombre único para el nuevo conjunto de datos que se creará, junto con detalles sobre las opciones de configuración que se copiarán. Cuando esté listo, seleccione **[!UICONTROL Copiar]**.

![Imagen del cuadro de diálogo de confirmación para copiar un conjunto de datos](../assets/datastreams/configure/copy-datastream-confirm.png)

La página principal del [!UICONTROL Datastreams] El espacio de trabajo vuelve a aparecer con el nuevo conjunto de datos enumerado.

## Pasos siguientes

Esta guía describe cómo administrar conjuntos de datos en la interfaz de usuario de recopilación de datos. Para obtener más información sobre cómo instalar y configurar el SDK web después de configurar un conjunto de datos, consulte la [Guía de recopilación de datos E2E](../../collection/e2e.md#install).
