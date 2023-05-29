---
keywords: Experience Platform;inicio;temas populares;
title: (Beta) Información General Sobre El Conector De Origen De Mixpanel
description: Obtenga información sobre cómo conectar Mixpanel a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>El [!DNL Mixpanel] el origen está en versión beta. Consulte la [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una aplicación de análisis de terceros. La compatibilidad con proveedores de análisis incluye [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de productos que le permite capturar datos sobre cómo los usuarios interactúan con un producto digital. Mixpanel le permite analizar estos datos de producto con informes sencillos e interactivos que le permiten consultar y visualizar los datos con solo unos clics.

Fuentes aprovecha el [API de exportación de eventos de Mixpanel > Descargar](https://developer.mixpanel.com/reference/raw-event-export) para descargar los datos de evento a medida que se reciben y almacenan en [!DNL Mixpanel], junto con todas las propiedades de evento (incluidas las siguientes `distinct_id`) y la marca de tiempo exacta en la que se envió el evento al Experience Platform. Mixpanel utiliza tokens de portador como mecanismo de autenticación para comunicarse con la API de exportación de eventos de Mixpanel.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Autentique su [!DNL Mixpanel] account

Esta sección describe los pasos previos que debe seguir para autenticar su cuenta y traer su [!DNL Mixpanel] datos a Platform.

Para crear un [!DNL Mixpanel] conexión de origen y flujo de datos, primero debe tener un [!DNL Mixpanel] cuenta. Si no tiene un válido [!DNL Mixpanel] cuenta de, consulte la [Registro de Mixpanel](https://mixpanel.com/register/) para crear su cuenta de.

Una vez que haya creado correctamente una [!DNL Mixpanel] cuenta de, vaya a la [!DNL Project Details] en la pestaña [!DNL Project Seettings] página de la [!DNL Mixpanel] IU para recuperar el ID de proyecto y configurar la zona horaria.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

A continuación, vaya a [!DNL Service Accounts] en la pestaña [!DNL Project Settings] página en la [!DNL Mixpanel] IU para recuperar las credenciales de la cuenta de servicio.

>[!TIP]
>
>Para una práctica recomendada, seleccione una cuenta de servicio que [no caduca](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Cuenta de servicio de Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Finalmente, cree una plataforma [esquema](../../../xdm/schema/composition.md) necesario para el [!DNL Mixpanel Event Export API]. Para obtener más información sobre las asignaciones necesarias para el esquema, consulte la guía de [creación de un [!DNL Mixpanel] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Crear esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Mixpanel] Vaya a Platform mediante las API o la interfaz de usuario de:

* [Crear una conexión de origen y un flujo de datos para [!DNL Mixpanel] uso de la API de Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] a Platform mediante la IU

* [Crear un [!DNL Mixpanel] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/analytics/mixpanel.md)
* [Crear un flujo de datos para una conexión de origen de éxito de cliente en la interfaz de usuario](../../tutorials/ui/dataflow/analytics.md)
