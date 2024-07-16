---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Guía de API de fuentes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre el proceso de creación de un nuevo origen, incluidos los pasos sobre cómo recuperar, escribir y enviar una nueva especificación de conexión mediante la API de Flow Service.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Guía de API de fuentes de autoservicio (SDK por lotes)

Este documento proporciona información general del proceso de creación de un nuevo origen, incluidos los pasos para escribir y enviar una nueva especificación de conexión mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] se usa para recopilar y centralizar datos de clientes de distintos orígenes dentro de Platform. El servicio proporciona una interfaz de usuario y una API RESTful que le permite configurar conexiones de origen a varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticar sus sistemas de terceros, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

La API [!DNL Flow Service] proporciona varios extremos que le permiten administrar mediante programación las especificaciones de conexión y flujo para un nuevo origen que está integrando mediante fuentes de autoservicio (SDK por lotes).

## Crear una nueva especificación de conexión

El primer paso para configurar un nuevo origen es crear una nueva especificación de conexión.

Las especificaciones de conexión devuelven las propiedades del conector de origen. Incluyen especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen y un ID de especificación de conexión fijo que se asigna a un origen determinado. Las especificaciones de conexión no dependen del inquilino ni de la organización. Una especificación de conexión típica contiene información básica sobre un origen determinado, así como tres secciones distintas: `authSpec`, `sourceSpec` y `exploreSpec`.

Para obtener instrucciones detalladas, consulte la guía sobre [creación de una nueva especificación de conexión](./create.md). Para obtener información sobre las propiedades y los valores utilizados para una especificación de conexión, incluidos detalles sobre la configuración de la autenticación, el origen y la exploración de especificaciones, consulte el [documento de opciones de configuración](../config/config.md).

## Actualizar especificaciones de flujo

Una vez que haya creado correctamente una especificación de conexión, debe anexar la especificación de flujo `RestStorageToAEP` para permitir que el origen cree un flujo de datos.

Las especificaciones de flujo contienen información que define un flujo, incluidos los ID de conexión de origen y destino que admite, las especificaciones de transformación que se deben aplicar a los datos y los parámetros de programación necesarios para generar un flujo.

Para obtener instrucciones detalladas, consulte la guía sobre [actualización de las especificaciones de flujo](./update-flow-specs.md).

## Actualizar la especificación de conexión

Puede realizar actualizaciones en la especificación de conexión realizando una solicitud de PUT a la API [!DNL Flow Service]. Consulte la guía de [actualización de las especificaciones de conexión](./update-connection-specs.md) para obtener más información.

## Enviar el origen

Para enviar el origen para su integración al Experience Platform, primero debe completar todo el flujo de trabajo de la API [!DNL Flow Service] para los orígenes a fin de asegurarse de que el origen funciona correctamente. Si el origen se ejecuta correctamente, puede continuar y ponerse en contacto con el representante del Adobe para la verificación y la promoción. Consulte la guía sobre [probar y enviar el origen](./submit.md) para obtener más información

## Pasos siguientes

Para empezar a usar la API [!DNL Flow Service] y crear una nueva fuente a través de fuentes de autoservicio (SDK por lotes), lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a usar extremos específicos.
