---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2022'
description: Las notas de la versión de febrero de 2022 de Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 27%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 7 de marzo de 2022**

>[!NOTE]
>
>Esta versión se cambió de la fecha original del 23 de febrero al 7 de marzo.

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través del cual puede ver información importante acerca de los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevos widgets de destinos estándar | Los siguientes widgets estándar le permiten visualizar diferentes métricas relacionadas con sus destinos.<ul><li>Segmentos activados recientemente por destino. Este widget muestra los cinco segmentos activados más recientemente en orden descendente según el destino elegido.</li><li>Tendencia de tamaño de audiencia. Este widget muestra la relación del recuento de perfiles durante un período de tiempo para un segmento que se ha asignado a esa cuenta de destino.</li><li>Segmentos no asignados por identidad. Este widget enumera los cinco segmentos principales sin asignar clasificados por recuento de identidad descendente para un destino e identidad determinados.</li><li>Segmentos asignados por identidad. Este widget enumera los cinco segmentos asignados principales. Los segmentos se ordenan de alto a bajo según sus respectivos recuentos de ID de origen que coinciden con el ID de destino seleccionado en el menú desplegable del widget.</li><li>Audiencias comunes. Este widget proporciona una lista de los cinco segmentos principales activados en la cuenta de destino elegida en la parte superior de la página y el destino seleccionado en el menú desplegable del widget.</li></ul> Para obtener más información sobre los widgets estándar disponibles, consulte la [documentación del panel destinos.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Para obtener más información sobre [!DNL Dashboards], consulte la [[!DNL Dashboards] descripción general](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Flujo de trabajo de IU mejorado para la configuración del flujo de datos | Se ha actualizado el flujo de trabajo para crear un nuevo conjunto de datos en la IU de recopilación de datos. Al agregar servicios a un conjunto de datos, solo los servicios a los que tiene acceso se incluyen en la lista de opciones. Consulte la guía de [configuración de una secuencia de datos](../../datastreams/overview.md) para obtener más información. |
| Preparación de datos para la recopilación de datos | Si utiliza el SDK web de Adobe Experience Platform, ahora puede aprovechar las funcionalidades de preparación de datos para asignar los datos al modelo de datos de experiencia (XDM) en el servidor. Consulte la sección sobre [Preparación de datos para la recopilación de datos](../../datastreams/data-prep.md) en la guía de flujos de datos para obtener más información. |
| ID de dispositivos de origen | Ahora puede enviar sus propios ID de dispositivo a Adobe Experience Platform Edge Network al recopilar datos de clientes mediante el SDK web de Platform, lo que proporciona una solución alternativa para las recientes restricciones del explorador sobre la duración de las cookies de terceros. Consulte la guía de [ID de dispositivos de origen](../../edge/identity/first-party-device-ids.md) para obtener más información. |

Para obtener más información sobre la recopilación de datos en Platform, consulte la [resumen de recopilación de datos](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| Compatibilidad con Destination SDK (Beta) para destinos basados en archivos | [Compatibilidad del Destination SDK con destinos basados en archivos](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) se encuentra actualmente en la versión beta privada y solo está disponible para un número selecto de socios y clientes. La funcionalidad y la documentación asociada están sujetas a cambios antes del lanzamiento de la disponibilidad general.<br><br>Póngase en contacto con el representante de su cuenta de Adobe para obtener información sobre cómo acceder a la función. Los representantes de cuentas internas del Adobe deben ponerse en contacto con los equipos de ingeniería y de productos de los destinos de los Experience Platform para analizar los casos de uso admitidos. <br><br> En la fase beta de la asistencia de Destination SDK para destinos basados en archivos, los socios y clientes de la versión beta pueden utilizar la [Destination SDK Experience Platform](../../destinations/destination-sdk/overview.md) para crear destinos privados que se beneficien de las siguientes funciones: <ul><li>Cree un destino basado en archivos (por lotes) mediante Amazon S3, servidores SFTP, Azure Blob, Azure Data Lake Storage, Data Landing Zone Storage.</li><li>Configure y establezca las opciones predeterminadas de frecuencia y programación de exportación de archivos.</li><li>Configure y defina opciones para dar formato a los archivos CSV exportados (delimitadores, caracteres de escape y otras opciones).</li><li>Capacidad para establecer y editar encabezados de archivo personalizados.</li><li>Capacidad para recibir notificaciones de eventos sobre la exportación de archivos y segmentos.</li><li>Capacidad para exportar tipos de archivo adicionales, como CSV, TSV, JSON o Parquet.</li></ul>  <br>Para empezar a usar la nueva funcionalidad, lea [(Beta) Use el Destination SDK para configurar un destino basado en archivos](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> La funcionalidad para crear contenido privado o de producción *transmisión* destinos mediante Destination SDK ya está disponible para todos los clientes y socios de Experience Platform. Lea la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](../../destinations/destination-sdk/guides/configure-destination-instructions.md) para obtener más información. |

## [!DNL Identity Service] {#identity}

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente individual parezca tener varias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo permiso para `view-identity-graph` | Ahora puede utilizar la variable `view-identity-graph` para controlar si los usuarios de su organización pueden ver los datos del gráfico de identidades. Los usuarios sin este permiso no podrán acceder al visor de gráficos de identidad en la interfaz de usuario ni al acceder a [!DNL Identity Service] API que devuelven identidades. Consulte la [información general de control de acceso](../../access-control/home.md) para obtener más información sobre los permisos. |

Para obtener información más general sobre [!DNL Identity Service], consulte la [Introducción al servicio de identidad](../../identity-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Fuentes beta que se trasladan a GA | Las siguientes fuentes se han promocionado de beta a GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).