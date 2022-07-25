---
title: Notas de la versión de Adobe Experience Platform, febrero de 2022
description: Notas de la versión de febrero de 2022 para Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 3%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 7 de marzo de 2022**

>[!NOTE]
>
>Esta versión fue modificada desde la fecha original del 23 de febrero hasta el 7 de marzo.

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través de la cual puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas utilidades de destinos estándar | Los siguientes widgets estándar le permiten visualizar distintas métricas relacionadas con sus destinos.<ul><li>Segmentos activados recientemente por destino. Esta utilidad muestra los cinco segmentos activados más recientemente en orden descendente según el destino elegido.</li><li>Tendencia del tamaño de la audiencia. Esta utilidad representa la relación del recuento de perfiles durante un período de tiempo para un segmento que se ha asignado a esa cuenta de destino.</li><li>Segmentos no asignados por identidad. Esta utilidad enumera los cinco segmentos sin asignar principales clasificados por recuento de identidad descendente para un destino e identidad determinados.</li><li>Segmentos asignados por identidad. Esta utilidad enumera los cinco segmentos asignados principales. Los segmentos se ordenan de mayor a menor según sus respectivos recuentos de ID de origen que coincidan con el ID de destino seleccionado en el menú desplegable del widget.</li><li>Audiencias comunes. Esta utilidad proporciona una lista de los cinco segmentos principales activados en la cuenta de destino elegida en la parte superior de la página y el destino seleccionado en la lista desplegable de la utilidad.</li></ul> Para obtener más información sobre los widgets estándar disponibles, consulte la [documentación del panel de destinos .](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Para obtener más información, consulte [!DNL Dashboards], consulte la [[!DNL Dashboards] información general](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Flujo de trabajo de IU mejorado para la configuración del conjunto de datos | Se ha actualizado el flujo de trabajo para crear un nuevo conjunto de datos en la interfaz de usuario de la recopilación de datos. Al añadir servicios a un conjunto de datos, solo los servicios a los que tiene acceso se incluirán en la lista de opciones. Consulte la guía de [configuración de un conjunto de datos](../../edge/datastreams/overview.md) para obtener más información. |
| Preparación de datos para la recopilación de datos | Si utiliza el SDK web de Adobe Experience Platform, ahora puede aprovechar las funciones de preparación de datos para asignar los datos al Modelo de datos de experiencia (XDM) en el servidor. Consulte la sección sobre [Preparación de datos para la recopilación de datos](../../edge/datastreams/data-prep.md) en la guía de conjuntos de datos para obtener más información. |
| ID de dispositivos de origen | Ahora puede enviar sus propios ID de dispositivo a la red perimetral de Adobe Experience Platform al recopilar datos de clientes mediante el SDK web de Platform, lo que proporciona una solución alternativa a las recientes restricciones del explorador en los planes de vida de cookies de terceros. Consulte la guía de [ID de dispositivos de origen](../../edge/identity/first-party-device-ids.md) para obtener más información. |

Para obtener más información sobre la recopilación de datos en Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Compatibilidad con Destination SDK (Beta) para destinos basados en archivos | [Compatibilidad del Destination SDK con destinos basados en archivos](../../destinations/destination-sdk/file-based-destination-configuration.md) está actualmente en versión beta privada y solo está disponible para un número determinado de socios y clientes. La funcionalidad y la documentación asociada están sujetas a cambios antes de la versión de disponibilidad general.<br><br>Póngase en contacto con el representante de cuentas de Adobe para obtener información sobre cómo acceder a la función. Los representantes de cuentas internas del Adobe deben ponerse en contacto con los equipos de ingeniería y productos de destinos de Experience Platform para analizar los casos de uso admitidos. <br><br> En la fase beta de la compatibilidad con Destination SDK para destinos basados en archivos, los socios beta y los clientes pueden usar la variable [Destination SDK del Experience Platform](/help/destinations/destination-sdk/overview.md) para crear destinos privados para beneficiarse de las siguientes funciones: <ul><li>Cree un destino basado en archivos (por lotes) mediante Amazon S3, servidores SFTP, Azure Blob, almacenamiento de Azure Data Lake, almacenamiento de Data Landing Zone.</li><li>Configure y establezca las opciones predeterminadas de programación y frecuencia de exportación de archivos.</li><li>Configure y defina opciones para dar formato a los archivos CSV exportados (delimitadores, caracteres de escape y otras opciones).</li><li>Posibilidad de establecer y editar encabezados de archivo personalizados.</li><li>Capacidad para recibir notificaciones de eventos sobre la exportación de archivos y segmentos.</li><li>Capacidad para exportar tipos de archivo adicionales, como CSV, TSV, JSON y Parquet.</li></ul>  <br>Para comenzar con la nueva funcionalidad, lea [(Beta) Usar el Destination SDK para configurar un destino basado en archivos](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> La funcionalidad para crear privado o productizado *streaming* destinos mediante Destination SDK ya está disponible para todos los clientes y socios Experience Platform. Lea la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](/help/destinations/destination-sdk/configure-destination-instructions.md) para obtener más información. |

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo permiso para `view-identity-graph` | Ahora puede usar la variable `view-identity-graph` permiso para controlar si los usuarios de su organización pueden ver datos de gráficos de identidad. A los usuarios que no tengan este permiso se les prohibirá acceder al visor de gráficos de identidad en la interfaz de usuario o al acceder a él [!DNL Identity Service] API que devuelven identidades. Consulte la [información general sobre el control de acceso](../../access-control/home.md) para obtener más información sobre los permisos. |

Para obtener información más general, consulte [!DNL Identity Service], consulte [Información general del servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).