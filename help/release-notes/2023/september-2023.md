---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de septiembre de 2023 de Adobe Experience Platform.
source-git-commit: 1bfd5e05642e0ac8f80af5502878eaee0b33c704
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 28 de septiembre de 2023**

Nuevas funciones de Adobe Experience Platform:

- [Atributos calculados](#computed-attributes)

Actualizaciones de las funciones existentes en Experience Platform:

- [Alertas](#alerts)
- [Recopilación de datos](#data-collection)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Atributos calculados {#computed-attributes}

Los atributos calculados permiten resumir fácilmente los datos de evento en atributos de perfil a través de una interfaz de usuario intuitiva para una segmentación, personalización y activación basadas en el comportamiento mejoradas. Con esta función, puede crear atributos calculados de forma automática, administrarlos y utilizarlos en la segmentación, destinos de Real-Time CDP o Adobe Journey Optimizer. Además, los atributos calculados simplifican la segmentación y los flujos de trabajo de recorrido para ayudarle a ofrecer sin problemas experiencias relevantes. Para obtener más información sobre los atributos calculados, lea la [información general sobre atributos calculados](../../profile/computed-attributes/overview.md).

## Alertas {#alerts}

Experience Platform permite suscribirse a alertas basadas en eventos para diversas actividades de Platform. Puede suscribirse a diferentes reglas de alerta a través de la variable [!UICONTROL Alertas] en la interfaz de usuario de Platform y puede elegir recibir mensajes de alerta dentro de la propia interfaz de usuario o a través de notificaciones por correo electrónico.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Pestaña Historial de alertas | Las Alertas [!UICONTROL Historial] ahora incluirá todos los eventos, incluidos retrasos, inicios, aciertos y errores. Lea el [documentación de IU de alertas](../../observability/alerts/ui.md) para obtener más información sobre la pestaña history. |

{style="table-layout:auto"}

Para obtener más información sobre las alertas, lea la [[!DNL Observability Insights] descripción general](../../observability/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Secuencias de datos | Compatibilidad con la búsqueda de dispositivos | Al configurar una secuencia de datos, ahora puede seleccionar el nivel de información de búsqueda de dispositivos que desea recopilar. La información de búsqueda de dispositivos incluye datos sobre el dispositivo, el hardware, el sistema operativo y el explorador utilizados para interactuar con la página. <br>  La información de búsqueda de dispositivos no se puede recopilar junto con el agente de usuario y las sugerencias del cliente. Si elige recopilar información del dispositivo, se deshabilita la recopilación de sugerencias del agente de usuario y del cliente, y viceversa. Toda la información de búsqueda del dispositivo se almacena en `xdm:device` grupo de campos. Obtenga más información en la documentación sobre [configuración de flujos de datos](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensiones | [!DNL TikTok] extensión de API de eventos web | El [[!DNL TikTok] API de eventos web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) La extensión de le permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL TikTok] en forma de eventos del lado del servidor que utilizan el [!DNL TikTok] API de eventos web. |

{style="table-layout:auto"}

Para obtener más información sobre la recopilación de datos, lea la [resumen de recopilación de datos](../../tags/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la IU del servicio de identidad | Utilice la herramienta de creación de áreas de nombres personalizadas mejorada en la interfaz de usuario de Experience Platform para administrar mejor las áreas de nombres personalizadas y sus tipos de identidad correspondientes. La interfaz de usuario mejorada del servicio de identidad le proporciona lo siguiente: <ul><li>Experiencia contextual: Indicaciones visuales, claridad y contexto de lo que es un área de nombres de identidad y de los tipos de identidad.</li><li>Precisión: mejor gestión de errores, sin más nombres de identidad duplicados.</li><li>Capacidad de detección: acceso a la documentación desde un cuadro de diálogo dentro del producto.</li></ul> Para obtener más información, lea la guía de [crear áreas de nombres personalizadas](../../identity-service/namespaces.md#create-namespaces). |
| Cambios en los límites del gráfico de identidad | El límite del gráfico de identidades ha cambiado de 150 a 50 identidades. Cuando se incorpora una nueva identidad en un gráfico completo, se elimina la identidad más antigua en función de la marca de tiempo de ingesta y el tipo de identidad. Los tipos de identidad de cookies tienen prioridad para su eliminación. Póngase en contacto con el equipo de cuenta de Adobe para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobes procesará manualmente estas solicitudes. Para obtener más información, lea la [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Para obtener más información sobre Identity Service, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Columnas personalizables | Ahora puede personalizar el diseño de Audience Portal con columnas cuyo tamaño se puede cambiar. Para obtener más información acerca de esta funcionalidad, lea la [Guía de IU de segmentación](../../segmentation/ui/overview.md#customize). |
| Desglose de frecuencia de actualización | Ahora puede ver un desglose de las frecuencias de actualización de las audiencias de su organización. Para obtener más información acerca de esta funcionalidad, lea la [Guía de IU de segmentación](../../segmentation/ui/overview.md#browse). |

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).

Para obtener más información sobre el servicio de segmentación, lea la [Resumen del servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevos parámetros para `offset` paginación en orígenes de autoservicio (SDK por lotes) | Ahora puede especificar un `endConditionName` y `endConditionValue` para su origen al utilizar `offset` paginación. Estos parámetros le permiten indicar la condición que debe finalizar el bucle de paginación en la siguiente solicitud HTTP. Para obtener más información, lea la [Guía de paginación para orígenes de autoservicio (SDK por lotes)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).