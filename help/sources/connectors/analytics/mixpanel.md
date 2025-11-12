---
title: Información general sobre el conector Mixpanel Source
description: Obtenga información sobre cómo conectar Mixpanel a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 6%

---

# [!DNL Mixpanel]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que ofrece la posibilidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una aplicación de análisis de terceros. Los proveedores de análisis admiten [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de productos que le permite capturar datos sobre cómo los usuarios interactúan con un producto digital. Mixpanel le permite analizar estos datos de producto con informes sencillos e interactivos que le permiten consultar y visualizar los datos con solo unos clics.

Sources aprovecha [Mixpanel Event Export API > Download](https://developer.mixpanel.com/reference/raw-event-export) para descargar los datos de evento a medida que se reciben y almacenan en [!DNL Mixpanel], junto con todas las propiedades de evento (incluido `distinct_id`) y la marca de tiempo exacta en que se envió el evento a Experience Platform. Mixpanel utiliza tokens de portador como mecanismo de autenticación para comunicarse con la API de exportación de eventos de Mixpanel.

## LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

## Autenticar su cuenta de [!DNL Mixpanel]

Esta sección describe los pasos necesarios que se deben seguir para autenticar su cuenta y llevar los datos de [!DNL Mixpanel] a Experience Platform.

Para crear una conexión de origen y un flujo de datos de [!DNL Mixpanel], primero debe tener una cuenta de [!DNL Mixpanel] válida. Si no tiene una cuenta de [!DNL Mixpanel] válida, consulte la página [Registro de Mixpanel](https://mixpanel.com/register/) para crear su cuenta.

Una vez que haya creado correctamente una cuenta de [!DNL Mixpanel], vaya a la pestaña [!DNL Project Details] en la página [!DNL Project Seettings] de la interfaz de usuario de [!DNL Mixpanel] para recuperar el ID de proyecto y configurar la zona horaria.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

A continuación, vaya a la ficha [!DNL Service Accounts] en la página [!DNL Project Settings] de la interfaz de usuario de [!DNL Mixpanel] para recuperar las credenciales de la cuenta de servicio.

>[!TIP]
>
>Para una práctica recomendada, seleccione una cuenta de servicio que [no caduque](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Cuenta De Servicio De Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Finalmente, cree un Experience Platform [schema](../../../xdm/schema/composition.md) necesario para [!DNL Mixpanel Event Export API]. Para obtener más información sobre las asignaciones necesarias para su esquema, consulte la guía sobre [creación de una conexión de origen en la interfaz de usuario [!DNL Mixpanel] .](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources)

![Crear esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Conectar [!DNL Mixpanel] a Experience Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Mixpanel] a Experience Platform mediante API o la interfaz de usuario:

* [Cree una conexión de origen y un flujo de datos para [!DNL Mixpanel] usando la API de Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Conectar [!DNL Mixpanel] a Experience Platform mediante la interfaz de usuario

* [Crear una  [!DNL Mixpanel] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/analytics/mixpanel.md)
* [Crear un flujo de datos para una conexión de origen de éxito de cliente en la interfaz de usuario](../../tutorials/ui/dataflow/analytics.md)
