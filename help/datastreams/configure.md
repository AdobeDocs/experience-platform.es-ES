---
title: Configuración de una secuencia de datos
description: Obtenga información sobre cómo conectar la integración del SDK web del lado del cliente con otros productos de Adobe y destinos de terceros.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: db75771d09caef00db58073333909f730a303975
workflow-type: tm+mt
source-wordcount: '2777'
ht-degree: 75%

---


# Configuración de una secuencia de datos

Este documento describe los pasos para configurar una [secuencia de datos](./overview.md) en la interfaz de usuario.

## Acceda al espacio de trabajo [!UICONTROL Secuencias de datos]

Puede crear y administrar flujos de datos en la IU de recopilación de datos o en la IU del Experience Platform seleccionando **[!UICONTROL Secuencias de datos]** en el panel de navegación izquierdo.

![Pestaña Secuencias de datos en la IU de recopilación de datos](assets/configure/datastreams-tab.png)

La pestaña **[!UICONTROL Secuencias de datos]** muestra una lista de las secuencias de datos existentes, incluidos su nombre descriptivo, ID y fecha de la última modificación. Seleccione el nombre de una secuencia de datos para [ver sus detalles y configurar servicios](#view-details).

Seleccione el icono “más” (**...**) de una secuencia de datos en concreto para mostrar más opciones. Seleccione **[!UICONTROL Editar]** para actualizar la [configuración básica](#configure) para la secuencia de datos o seleccione **[!UICONTROL Eliminar]** para eliminar la secuencia de datos.

![Opciones para editar o eliminar una secuencia de datos existente](assets/configure/edit-datastream.png)

## Creación de una nueva secuencia de datos {#create}

Para crear una secuencia de datos, empiece seleccionando una **[!UICONTROL nueva secuencia de datos]**.

![Seleccione nueva secuencia de datos](assets/configure/new-datastream-button.png)

Aparece el flujo de trabajo de creación de secuencia de datos, empezando por el paso de configuración. Aquí debe proporcionar un nombre y una descripción opcional para la secuencia de datos.

Si está configurando esta secuencia de datos para utilizarla en Experience Platform y utiliza el SDK web de Platform, también debe seleccionar un [esquema del modelo de datos de experiencia (XDM) basado en eventos](../xdm/classes/experienceevent.md) para representar los datos que tiene previsto introducir.

![Configuración básica de una secuencia de datos](assets/configure/configure.png)

### Configurar la geolocalización y la búsqueda de red {#geolocation-network-lookup}

La configuración de geolocalización y búsqueda de red le ayuda a definir el nivel de granularidad de los datos geográficos y de red que desea recopilar.

Expanda el **[!UICONTROL Geolocalización y búsqueda de red]** para configurar las opciones que se describen a continuación.

![Captura de pantalla de la IU de Platform que muestra la pantalla de configuración de la secuencia de datos con los ajustes de geolocalización y búsqueda de red resaltados.](assets/configure/geolookup.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Búsquedas de geolocalización] | Activa las búsquedas de geolocalización para las opciones seleccionadas en función de la dirección IP del visitante. Las opciones disponibles incluyen: <ul><li>**País**: rellena `xdm.placeContext.geo.countryCode`</li><li>**Código postal**: rellena `xdm.placeContext.geo.postalCode`</li><li>**Estado/Provincia**: rellena `xdm.placeContext.geo.stateProvince`</li><li>**DMA**: rellena `xdm.placeContext.geo.dmaID`</li><li>**Ciudad**: rellena `xdm.placeContext.geo.city`</li><li>**Latitud**: rellena `xdm.placeContext.geo._schema.latitude`</li><li>**Longitud**: rellena `xdm.placeContext.geo._schema.longitude`</li></ul>Seleccionar **[!UICONTROL Ciudad]**, **[!UICONTROL Latitud]** o **[!UICONTROL Longitud]** proporciona coordenadas de hasta dos decimales, independientemente de las demás opciones seleccionadas. Se considera una granularidad de nivel de ciudad.<br> <br>Al no seleccionar ninguna opción, se desactivan las búsquedas de geolocalización. La geolocalización se produce antes de [!UICONTROL Confusión de IP], lo que significa que no se ve afectado por el [!UICONTROL Confusión de IP] configuración. |
| [!UICONTROL Búsqueda de red] | Activa las búsquedas de red para las opciones seleccionadas según la dirección IP del visitante. Las opciones disponibles incluyen: <ul><li>**Portadora**: rellena `xdm.environment.carrier`</li><li>**Dominio**: rellena `xdm.environment.domain`</li><li>**ISP**: rellena `xdm.environment.ISP`</li></ul> |

Si habilita cualquiera de los campos anteriores para la recopilación de datos, asegúrese de establecer correctamente la variable [`context`](../edge/data-collection/automatic-information.md) propiedad de matriz cuando [configuración del SDK web](../edge/fundamentals/configuring-the-sdk.md).

Los campos de búsqueda de geolocalización utilizan la variable `context` cadena de matriz `"placeContext"`, mientras que los campos de búsqueda de red utilizan la variable `context` cadena de matriz `"environment"`.

Además, asegúrese de que cada campo XDM deseado exista en el esquema. Si no es así, puede agregar el Adobe proporcionado `Environment Details` grupo de campos al esquema.

### Configurar la búsqueda de dispositivos {#geolocation-device-lookup}

El **[!UICONTROL Búsqueda de dispositivos]** La configuración de le permite seleccionar la información específica del dispositivo que desea recopilar.

Expanda el **[!UICONTROL Búsqueda de dispositivos]** para configurar las opciones que se describen a continuación.

![Captura de pantalla de la IU de Platform que muestra la pantalla de configuración de la secuencia de datos con los ajustes de búsqueda del dispositivo resaltados.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>La configuración que se describe en la tabla siguiente es mutuamente excluyente. No puede seleccionar simultáneamente la información del agente de usuario y los datos de búsqueda del dispositivo.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Mantener encabezados de agente de usuario y sugerencias del cliente]** | Seleccione esta opción para recopilar únicamente la información almacenada en la cadena del agente de usuario. Esta opción está seleccionada de forma predeterminada. Rellena `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Utilice la búsqueda de dispositivos para recopilar la siguiente información]** | Seleccione esta opción si desea recopilar una o más de las siguientes informaciones específicas del dispositivo: <ul><li>**[!UICONTROL Dispositivo]** información:<ul><li>**Fabricante del dispositivo**: rellena `xdm.device.manufacturer`</li><li>**Modelo de dispositivo**: rellena `xdm.device.modelNumber`</li><li>**Nombre de marketing**: rellena `xdm.device.model`</li></ul></li><li>**[!UICONTROL Hardware]** información: <ul><li>**Tipo de hardware**: rellena `xdm.device.type`</li><li>**Altura de visualización**: rellena `xdm.device.screenHeight`</li><li>**Anchura de visualización**: rellena `xdm.device.screenWidth`</li><li>**Profundidad de color de visualización**: rellena `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Explorador]** información: <ul><li>**Proveedor del explorador**: rellena `xdm.environment.browserDetails.vendor`</li><li>**Nombre del explorador**: rellena `xdm.environment.browserDetails.name`</li><li>**Versión del explorador**: rellena `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Sistema operativo]** información: <ul><li>**Proveedor de SO**: rellena `xdm.environment.operatingSystemVendor`</li><li>**Nombre del SO**: rellena `xdm.environment.operatingSystem`</li><li>**Versión del SO**: rellena `xdm.environment.operatingSystemVersion`</li></ul></li></ul>La información de búsqueda de dispositivos no se puede recopilar junto con el agente de usuario y las sugerencias del cliente. Si elige recopilar información del dispositivo, se deshabilita la recopilación de sugerencias del agente de usuario y del cliente, y viceversa. |
| **[!UICONTROL No recopilar información de ningún dispositivo]** | Seleccione esta opción si no desea recopilar ninguna información de búsqueda de dispositivos. No se recopilan datos de dispositivos, hardware, exploradores, sistemas operativos, agentes de usuario o sugerencias del cliente. |

Si habilita cualquiera de los campos anteriores para la recopilación de datos, asegúrese de establecer correctamente la variable [`context`](../edge/data-collection/automatic-information.md) propiedad de matriz cuando [configuración del SDK web](../edge/fundamentals/configuring-the-sdk.md).

La información de dispositivo y hardware utiliza el `context` cadena de matriz `"device"`, mientras que la información del explorador y del sistema operativo utiliza el `context` cadena de matriz `"environment"`.

Además, asegúrese de que cada campo XDM deseado exista en el esquema. Si no es así, puede agregar el Adobe proporcionado `Environment Details` grupo de campos al esquema.

### Configuración de opciones avanzadas {#@advanced-options}

Seleccionar **[!UICONTROL Opciones avanzadas]** para mostrar controles adicionales para configurar el conjunto de datos, como ofuscación de IP, cookies de ID de origen y más.

![Opciones de configuración avanzadas](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> Es responsable de garantizar que ha obtenido todos los permisos, consentimientos, acreditaciones y autorizaciones necesarios según las leyes y regulaciones aplicables para recopilar, procesar y transmitir datos personales, incluida información precisa sobre geolocalización.
> 
> La selección de la ofuscación de la dirección IP no afecta al nivel de información de geolocalización que se derivará de la dirección IP y se enviará a las soluciones de Adobe configuradas. Las búsquedas de geolocalización deben limitarse o deshabilitarse por separado.

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Ofuscación de IP] | Indica el tipo de ofuscación de IP que se aplicará a la secuencia de datos. Cualquier procesamiento basado en la IP del cliente se verá afectado por la configuración de ofuscación de la IP. Esto incluye todos los servicios de Experience Cloud que reciben datos de la secuencia de datos. <p>Opciones disponibles:</p> <ul><li>**[!UICONTROL Ninguno]**: deshabilita la ofuscación de la IP. La dirección IP completa del usuario se envía a través de la secuencia de datos.</li><li>**[!UICONTROL Parcial]**: para las direcciones IPv4, oculta el último octeto de la dirección IP del usuario. Para las direcciones IPv6, ofusca los últimos 80 bits de la dirección. <p>Ejemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Completo]**: ofusca toda la dirección IP. <p>Ejemplos:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Impacto de la ofuscación de IP en otros productos de Adobe: <ul><li>**Adobe Target**: El nivel de flujo de datos [!UICONTROL Confusión de IP] se aplica antes de que [!UICONTROL Confusión de IP] realizado en Adobe Target, a todas las direcciones IP presentes en la solicitud. Por ejemplo, si el nivel de flujo de datos [!UICONTROL Confusión de IP] se establece en **[!UICONTROL Completo]** y la opción de confusión de IP de Adobe Target está configurada en **[!UICONTROL Ofuscación del último octeto]**, Adobe Target recibe una IP totalmente oculta. Si el nivel de secuencia de datos [!UICONTROL Confusión de IP] se establece en **[!UICONTROL Parcial]** y la opción de confusión de IP de Adobe Target está configurada en **[!UICONTROL Completo]**, Adobe Target recibe una IP parcialmente oculta y, a continuación, le aplica la confusión completa. La confusión de IP de Adobe Target se administra independientemente de la del conjunto de datos. Consulte la documentación de Adobe Target sobre [ofuscación de IP](https://developer.adobe.com/target/before-implement/privacy/privacy/) y [geolocalización](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=es) para obtener más información.</li><li>**Audience Manager**: El nivel de flujo de datos [!UICONTROL Confusión de IP] se aplica antes de que [!UICONTROL Confusión de IP] realizado en el Audience Manager, a todas las direcciones IP presentes en la solicitud. Cualquier búsqueda de geolocalización realizada por Audience Manager se ve afectada por la opción [!UICONTROL Ofuscación de IP] del nivel de secuencia de datos. Una búsqueda de geolocalización en Audience Manager, basada en una IP completamente oculta, dará como resultado una región desconocida y no se realizará ningún segmento basado en los datos de geolocalización resultantes. Consulte la documentación del Audience Manager sobre [ofuscación de IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=es) para obtener más información.</li><li>**Adobe Analytics**: Adobe Analytics recibe actualmente las direcciones IP parcialmente ocultas si se selecciona cualquier opción de ofuscación de IP distinta de NINGUNA. Para que Analytics reciba direcciones IP ofuscadas, debe configurar la ofuscación de IP por separado en Adobe Analytics. Este comportamiento se actualizará en futuras versiones. Consulte la [documentación](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html?lang=es) de Adobe Analytics para obtener más información sobre cómo habilitar la ofuscación de IP en Analytics.</li></ul> |
| [!UICONTROL ID de cookie de origen] | Cuando está habilitada, esta configuración indica a Edge Network que haga referencia a una cookie especificada al buscar una [ID de dispositivo de origen](../edge/identity/first-party-device-ids.md), en lugar de buscar este valor en el mapa de identidad.<br><br>Al habilitar esta configuración, debe proporcionar el nombre de la cookie en la que se espera almacenar el ID. |
| [!UICONTROL Sincronización de ID de terceros] | Las sincronizaciones de ID se pueden agrupar en contenedores para permitir que diferentes sincronizaciones de ID se ejecuten en momentos diferentes. Cuando está habilitada, esta configuración le permite especificar qué contenedor de sincronizaciones de ID se ejecuta para esta secuencia de datos. |
| [!UICONTROL ID del contenedor de sincronización de ID de terceros] | El ID numérico del contenedor que se utilizará para la sincronización de ID de terceros. |
| [!UICONTROL Anulaciones de ID de contenedor] | En esta sección puede definir los ID de contenedor de sincronización de ID de terceros adicionales que puede utilizar para anular el predeterminado. |
| [!UICONTROL Tipo de acceso] | Define el tipo de autenticación que Edge Network acepta para la secuencia de datos. <ul><li>**[!UICONTROL Autenticación mixta]**: cuando se selecciona esta opción, Edge Network acepta solicitudes autenticadas y no autenticadas. Seleccione esta opción si tiene previsto utilizar el SDK web o el [SDK móvil](https://developer.adobe.com/client-sdks/documentation/), junto con la [API de servidor](../server-api/overview.md). </li><li>**[!UICONTROL Solo autenticado]**: cuando se selecciona esta opción, Edge Network solo acepta solicitudes autenticadas. Seleccione esta opción cuando tenga previsto utilizar únicamente la API de servidor y desee evitar que Edge Network procese solicitudes no autenticadas.</li></ul> |
| [!UICONTROL Media Analytics] | Seleccione esta opción para habilitar el procesamiento de los datos de seguimiento de streaming para la integración de red perimetral mediante SDK de Experience Platform o API de Media Edge. Obtenga información acerca de Media Analytics en [documentación](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=es). |

A partir de aquí, si está configurando la secuencia de datos para Experience Platform, siga el tutorial de [Preparación de datos para la recopilación de datos](./data-prep.md) para asignar los datos a un esquema de evento de Platform antes de volver a esta guía. De lo contrario, seleccione **[!UICONTROL Guardar]** y continúe a la siguiente sección.

## Ver detalles de secuencia de datos {#view-details}

Después de configurar una secuencia de datos nueva o seleccionar una existente para verla, aparecerá la página de detalles de dicha secuencia de datos. Aquí puede encontrar más información sobre la secuencia de datos, incluido su ID.

![Página de detalles de una secuencia de datos creada](assets/configure/view-details.png)

En la pantalla de detalles de la secuencia de datos, puede [añadir servicios](#add-services) para habilitar las funciones de los productos de Adobe Experience Cloud a los que tiene acceso. También puede editar la [configuración básica](#create) de la secuencia de datos, actualizar su [reglas de asignación](./data-prep.md), [copiar la secuencia de datos](#copy) o eliminarla por completo.

## Añadir servicios a una secuencia de datos {#add-services}

En la página de detalles de una secuencia de datos, seleccione **[!UICONTROL Añadir servicio]** para empezar a añadir los servicios disponibles para ese conjunto de datos.

![Seleccione Añadir servicio para continuar](assets/configure/add-service.png)

En la pantalla siguiente, utilice el menú desplegable para seleccionar un servicio para configurar para esta secuencia de datos. En esta lista solo aparecen los servicios a los que tiene acceso.

![Seleccione un servicio de la lista](assets/configure/service-selection.png)

Seleccione el servicio deseado, rellene las opciones de configuración que aparecen y, a continuación, seleccione **[!UICONTROL Guardar]** para añadir el servicio a la secuencia de datos. Todos los servicios añadidos aparecen en la vista de detalles de la secuencia de datos.

![Servicios añadidos a una secuencia de datos](assets/configure/services-added.png)

Las subsecciones siguientes describen las opciones de configuración de cada servicio.

>[!NOTE]
>
>Cada configuración de servicio contiene una alternancia **[!UICONTROL Habilitada]** que se activa automáticamente cuando se selecciona el servicio. Para deshabilitar el servicio seleccionado para esta secuencia de datos, seleccione la alternancia **[!UICONTROL Habilitada]** de nuevo.

### Configuración de Adobe Analytics {#analytics}

Ese servicio controla si los datos se envían a Adobe Audience Manager y cómo. Puede encontrar más información en la guía sobre el [envío de datos a Analytics](../edge/data-collection/adobe-analytics/analytics-overview.md).

![Bloque de configuración de Adobe Analytics](assets/configure/analytics-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL ID del grupo de informes] | **(Obligatorio)** El ID del grupo de informes de Analytics al que desea enviar los datos. Este ID se encuentra en la interfaz de usuario de Adobe Analytics, en [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Si se especifican varios grupos de informes, los datos se copian en cada grupo de informes. |
| [!UICONTROL Anulaciones de grupos de informes] | En esta sección, puede añadir ID de grupos de informes adicionales que puede utilizar para anular el predeterminado. |

### Configuración de Adobe Audience Manager {#audience-manager}

Ese servicio controla si los datos se envían a Adobe Audience Manager y cómo. Todo lo que se necesita para enviar datos a Audience Manager es habilitar esta sección. El resto de la configuración es opcional, pero se recomienda usarla.

![Bloque de configuración de Adobe Audience Manager](assets/configure/audience-manager-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Destinos de cookies habilitados] | Permite al SDK compartir información de segmentos mediante los [destinos de cookies](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=es) de [!DNL Audience Manager]. |
| [!UICONTROL Destinos de URL habilitados] | Permite al SDK compartir información de segmentos mediante los [destinos de URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=es) de [!DNL Audience Manager]. |

### Configuración de Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Al habilitar una corriente de datos para Platform, tome nota de la zona protegida de Platform que está utilizando, tal como se muestra en la cinta superior de la interfaz de usuario.
>
>![Zona protegida seleccionada](assets/configure/platform-sandbox.png)
>
>Las zonas protegidas son particiones virtuales en Adobe Experience Platform que le permiten aislar los datos y las implementaciones de otros miembros de la organización. Una vez creada una secuencia de datos, su zona protegida no se puede cambiar. Para obtener más información sobre la función de los entornos limitados en Experience Platform, consulte la [documentación sobre zonas protegidas](../sandboxes/home.md).

Ese servicio controla si los datos se envían a Adobe Experience Platform y cómo.

![Bloque de configuración de Adobe Experience Platform](assets/configure/platform-config.png)

| Configuración | Descripción |
|---| --- |
| [!UICONTROL Conjunto de datos del evento] | **(Obligatorio)** Seleccione el conjunto de datos de Platform al que se transmitirán los datos de evento del cliente. Este esquema debe utilizar la [clase ExperienceEvent de XDM](../xdm/classes/experienceevent.md). Para añadir conjuntos de datos adicionales, seleccione **[!UICONTROL Añadir conjunto de datos de evento]**. |
| [!UICONTROL Conjunto de datos del perfil] | Seleccione el conjunto de datos de Platform al que se enviarán los datos de atributos del cliente. Este esquema debe utilizar la [clase de perfil individual de XDM](../xdm/classes/individual-profile.md). |
| [!UICONTROL Toma de decisiones sobre ofertas] | Seleccione esta casilla de verificación para habilitar la toma de decisiones sobre ofertas para una implementación del SDK web de Platform. Consulte la guía sobre el [uso de la toma de decisiones sobre ofertas con el SDK web de Platform](../edge/personalization/offer-decisioning/offer-decisioning-overview.md) para obtener más información sobre la implementación.<br><br>Para obtener más información sobre las capacidades de la toma de decisiones sobre ofertas, consulte la [Documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=es). |
| [!UICONTROL Segmentación de Edge] | Seleccione esta casilla de verificación para activar la [segmentación de Edge](../segmentation/ui/edge-segmentation.md) para esta secuencia de datos. Cuando el SDK envía datos a través de un flujo de datos habilitado para la segmentación de Edge, cualquier pertenencia a segmentos actualizada para el perfil en cuestión se devuelve en la respuesta.<br><br>Esta opción se puede utilizar en combinación con los [!UICONTROL destinos de personalización] para [casos de uso de personalización de página siguiente](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Destinos de personalización] | Al habilitar esto después de habilitar la casilla de verificación [!UICONTROL Segmentación de Edge], esta opción permite que la secuencia de datos se conecte a destinos de personalización como [Personalización personalizada](../destinations/catalog/personalization/custom-personalization.md).<br><br>Consulte la documentación de destinos para ver los pasos específicos sobre [configuración de destinos de personalización](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Seleccione esta casilla de verificación para activar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) para esta secuencia de datos. <br><br> Al habilitar esta opción, la secuencia de datos devolverá contenido personalizado de las campañas entrantes basadas en la web y la aplicación en [!DNL Adobe Journey Optimizer]. Esta opción requiere que la [!UICONTROL segmentación de Edge] esté activa. Si la [!UICONTROL segmentación de Edge] no está marcada, esta opción aparece atenuada. |

### Configuración de Adobe Target {#target}

Ese servicio controla si los datos se envían a Adobe Target y cómo.

![Bloque de configuración de Adobe Target](assets/configure/target-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Token de propiedad] | [!DNL Target] permite a los clientes controlar los permisos mediante el uso de propiedades. Para obtener más información sobre las propiedades, consulte la guía sobre [configuración de permisos de empresa](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es) en la documentación de [!DNL Target].<br><br>El token de propiedad se puede encontrar en la interfaz de usuario de Adobe Target en [!UICONTROL Configurar] > [!UICONTROL Propiedades]. |
| [!UICONTROL ID de entornos de Target] | [Entornos en Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=es) le ayuda a administrar la implementación en todas las etapas de desarrollo. Este ajuste especifica qué entorno va a utilizar con esta secuencia de datos.<br><br>La práctica recomendada es establecerlo de forma diferente para cada uno de sus entornos de secuencia de datos `dev`, `stage` y `prod` para mantener las cosas simples. Sin embargo, si ya tiene definidos los entornos de Adobe Target, puede utilizarlos. |
| [!UICONTROL Área de nombres de ID de terceros de Target] | El área de nombres de identidad para `mbox3rdPartyId` que desee utilizar para esta secuencia de datos. Consulte la guía sobre [implementación `mbox3rdPartyId` con el SDK web](../edge/personalization/adobe-target/using-mbox-3rdpartyid.md) para obtener más información. |
| [!UICONTROL Anulaciones de tókenes de propiedad] | En esta sección puede definir tókenes de propiedad adicionales que puede utilizar para anular los predeterminados. |

### Configuración del [!UICONTROL reenvío de eventos]

Este servicio controla si los datos se envían al [reenvío de eventos](../tags/ui/event-forwarding/overview.md) y cómo.

![Sección Reenvío de eventos de la IU de configuración](assets/configure/event-forwarding-config.png)

| Configuración | Descripción |
| --- | --- |
| [!UICONTROL Propiedad de Platform Launch] | **(Obligatorio)** La propiedad de reenvío de eventos a la que desea enviar datos. |
| [!UICONTROL Entorno de Platform Launch] | **(Obligatorio)** El entorno dentro de la propiedad seleccionada al que desea enviar datos. |

>[!NOTE]
>
>Puede seleccionar **[!UICONTROL Introducir ID manualmente]** para escribir los nombres de las propiedades y los entornos en lugar de utilizar los menús desplegables.

## Copiar una secuencia de datos {#copy}

Puede crear una copia de una secuencia de datos existente y modificar sus detalles según sea necesario.

>[!NOTE]
>
>Las secuencias de datos solo se pueden copiar dentro de la misma [zona protegida](../sandboxes/home.md). En otras palabras, no se puede copiar una secuencia de datos de una zona protegida a otra.

Desde la página principal, en el espacio de trabajo [!UICONTROL Secuencia de datos], seleccione los puntos suspensivos (**...**) para la secuencia de datos en cuestión y, a continuación, seleccione **[!UICONTROL Copiar]**.

![Imagen que muestra la opción [!UICONTROL Copiar] seleccionada en la vista de lista de secuencia de datos](assets/configure/copy-datastream-list.png)

Como alternativa, puede seleccionar **[!UICONTROL Copiar secuencia de datos]** desde la vista de detalles de una secuencia de datos determinada.

![Imagen que muestra la opción [!UICONTROL Copiar] seleccionada en la vista de detalles de la secuencia de datos](assets/configure/copy-datastream-details.png)

Aparecerá un cuadro de diálogo de confirmación en el que se le solicitará que proporcione un nombre único para la nueva secuencia de datos que se va a crear, junto con detalles sobre las opciones de configuración que se copiarán. Cuando esté listo, seleccione **[!UICONTROL Copiar]**.

![Imagen del cuadro de diálogo de confirmación para copiar una secuencia de datos](assets/configure/copy-datastream-confirm.png)

La página principal del espacio de trabajo [!UICONTROL Secuencias de datos] vuelve a aparecer con la nueva secuencia de datos en la lista.

## Pasos siguientes

En esta guía se explica cómo administrar flujos de datos en la IU de recopilación de datos. Para obtener más información sobre cómo instalar y configurar el SDK web después de configurar una secuencia de datos, consulte la [Guía E2E de recopilación de datos](../collection/e2e.md#install).
