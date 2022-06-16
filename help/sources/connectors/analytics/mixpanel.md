---
keywords: Experience Platform;inicio;temas populares;
title: (Beta) Descripción general del conector de origen de Mixpanel
description: Obtenga información sobre cómo conectar Mixpanel a Adobe Experience Platform mediante API o la interfaz de usuario.
hide: true
hidefromtoc: true
source-git-commit: e7a5e20721f5826ca1f4520b4a27d261eed1e4df
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>La variable [!DNL Mixpanel] el origen está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform permite la ingesta de datos desde una aplicación de análisis de terceros. La compatibilidad con los proveedores de análisis incluye [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de productos que le permite capturar datos sobre cómo interactúan los usuarios con un producto digital. Mixpanel le permite analizar los datos de este producto con informes sencillos e interactivos que le permiten consultar y visualizar los datos con tan solo unos clics.

Las fuentes aprovechan el [API de exportación de eventos de Mixpanel > Descargar](https://developer.mixpanel.com/reference/raw-event-export) para descargar los datos de evento a medida que se reciben y se almacenan en [!DNL Mixpanel], junto con todas las propiedades de evento (incluido `distinct_id`) y la marca de tiempo exacta en la que se envió el evento al Experience Platform. Mixpanel utiliza tokens al portador como mecanismo de autenticación para comunicarse con la API de exportación de eventos de Mixpanel.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Autentique su [!DNL Mixpanel] account

En esta sección se describen los pasos previos a completar para autenticar la cuenta y traer su [!DNL Mixpanel] a Platform.

Para crear un [!DNL Mixpanel] conexión de origen y flujo de datos, primero debe tener una [!DNL Mixpanel] cuenta. Si no tiene un [!DNL Mixpanel] consulte la [Registro de Mixpanel](https://mixpanel.com/register/) para crear su cuenta.

Una vez que haya creado correctamente un [!DNL Mixpanel] , vaya a la [!DNL Project Details] en la ficha [!DNL Project Seettings] de [!DNL Mixpanel] IU para recuperar el ID del proyecto y configurar la zona horaria.

![mixpanel-proyecto-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

A continuación, vaya a la [!DNL Service Accounts] en la ficha [!DNL Project Settings] en el [!DNL Mixpanel] IU para recuperar las credenciales de la cuenta de servicio.

>[!TIP]
>
>Para una práctica recomendada, seleccione una cuenta de servicio que [no caduca](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Cuenta de servicio de Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Finalmente, cree una plataforma [esquema](../../../xdm/schema/composition.md) necesario para [!DNL Mixpanel Event Export API]. Para obtener más información sobre las asignaciones necesarias para el esquema, consulte la guía de [crear un [!DNL Mixpanel] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Crear esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Mixpanel] a Platform mediante API o la interfaz de usuario:

* [Crear una conexión de origen y un flujo de datos para [!DNL Mixpanel] uso de la API de servicio de flujo](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] a Platform mediante la interfaz de usuario

* [Cree un [!DNL Mixpanel] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/analytics/mixpanel.md)
* [Crear un flujo de datos para una conexión de origen de éxito del cliente en la interfaz de usuario](../../tutorials/ui/dataflow/analytics.md)

