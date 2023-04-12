---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Guía de API de fuentes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre el proceso de creación de una nueva fuente, incluidos los pasos para recuperar, escribir y enviar una nueva especificación de conexión mediante la API de servicio de flujo.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Guía de API de fuentes de autoservicio (SDK por lotes)

Este documento proporciona una descripción general del proceso de creación de una nueva fuente, incluidos los pasos para escribir y enviar una nueva especificación de conexión mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen con varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

La variable [!DNL Flow Service] La API proporciona varios puntos de conexión que le permiten administrar mediante programación las especificaciones de conexión y flujo para una nueva fuente que está integrando mediante fuentes de autoservicio (SDK por lotes).

## Crear una nueva especificación de conexión

El primer paso para configurar un nuevo origen es crear una nueva especificación de conexión.

Las especificaciones de conexión devuelven las propiedades del conector de un origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen en particular. Las especificaciones de conexión no dependen del inquilino ni de la organización. Una especificación de conexión típica contiene información básica sobre un origen determinado, así como tres secciones diferentes: `authSpec`, `sourceSpec`y `exploreSpec`.

Para obtener instrucciones detalladas, consulte la guía de [creación de una nueva especificación de conexión](./create.md). Para obtener información sobre las propiedades y los valores utilizados para una especificación de conexión, incluidos los detalles sobre la configuración de la autenticación, el origen y las especificaciones de exploración, consulte [documento de opciones de configuración](../config/config.md).

## Actualización de especificaciones de flujo

Una vez que haya creado correctamente una especificación de conexión, debe adjuntar la variable `RestStorageToAEP` especificación de flujo para permitir que el origen cree un flujo de datos.

Las especificaciones de flujo contienen información que define un flujo, incluidos los ID de conexión de origen y destino que admite, las especificaciones de transformación que deben aplicarse a los datos y los parámetros de programación necesarios para generar un flujo.

Para obtener instrucciones detalladas, consulte la guía de [actualizar especificaciones de flujo](./update-flow-specs.md).

## Actualizar la especificación de conexión

Puede actualizar la especificación de conexión realizando una solicitud de PUT al [!DNL Flow Service] API. Consulte la guía de [actualización de las especificaciones de conexión](./update-connection-specs.md) para obtener más información.

## Enviar el origen

Para enviar la fuente para su integración a Experience Platform, primero debe completar la [!DNL Flow Service] Flujo de trabajo de API para fuentes para garantizar que el origen funcione correctamente. Si la fuente se ejecuta correctamente, puede continuar y ponerse en contacto con el representante de Adobes para la verificación y promoción. Consulte la guía de [probar y enviar su fuente](./submit.md) para obtener más información

## Pasos siguientes

Para empezar a usar la variable [!DNL Flow Service] y cree una fuente nueva a través de fuentes de autoservicio (SDK por lotes), lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos.
