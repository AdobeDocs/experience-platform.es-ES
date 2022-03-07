---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: d407d6bedbe0eb9b4dde229d990160c114fad472
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 23 de febrero de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [[!DNL Identity Service]](#identity)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Flujo de trabajo de IU mejorado para la configuración del conjunto de datos | Se ha actualizado el flujo de trabajo para crear un nuevo conjunto de datos en la interfaz de usuario de la recopilación de datos. Al añadir servicios a un conjunto de datos, solo los servicios a los que tiene acceso se incluirán en la lista de opciones. Consulte la guía de [configuración de un conjunto de datos](../../edge/fundamentals/datastreams.md) para obtener más información. |
| Preparación de datos para la recopilación de datos | Si utiliza el SDK web de Adobe Experience Platform, ahora puede aprovechar las funciones de preparación de datos para asignar los datos al Modelo de datos de experiencia (XDM) en el servidor. Consulte la sección sobre [Preparación de datos para la recopilación de datos](../../edge/fundamentals/datastreams.md#data-prep) en la guía de conjuntos de datos para obtener más información. |
| ID de dispositivos de origen | Ahora puede enviar sus propios ID de dispositivo a la red perimetral de Adobe Experience Platform al recopilar datos de clientes mediante el SDK web de Platform, lo que proporciona una solución alternativa a las recientes restricciones del explorador en los planes de vida de cookies de terceros. Consulte la guía de [ID de dispositivos de origen](../../edge/identity/first-party-device-ids.md) para obtener más información. |

Para obtener más información sobre la recopilación de datos en Platform, consulte la [información general sobre recopilación de datos](../../collection/home.md).

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
