---
title: Información general de Adobe Experience Platform Assurance
description: Adobe Experience Platform Assurance le permite inspeccionar, comprobar, simular y validar cómo recopila datos o sirve experiencias en sus aplicaciones móviles.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---


# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance es un producto de [Adobe Experience Cloud](https://www.adobe.com/es/experience-cloud.html) para ayudarle a inspeccionar, comprobar, simular y validar cómo recopila datos o sirve experiencias en su aplicación móvil.

>[!IMPORTANT]
>
> El proyecto Griffon ahora se conoce como **Garantía**!
>
> El proyecto Griffon ahora está disponible para el público general **all** Clientes de Adobe Experience Cloud como seguro. Para obtener más información sobre esta transición, lea la [guía de acceso del usuario](./user-access.md).

>[!INFO]
>
>¡Las API públicas de seguro están disponibles!
>
>[Las API de seguridad](https://developer.adobe.com/adobe-assurance-public-apis/) son una colección de API que permiten a los usuarios probar y depurar sus aplicaciones web y móviles, cuando están equipadas con el SDK para móviles de Adobe Assurance.

## Disponibilidad general

A partir del 15 de octubre de 2022, Assurance estará disponible para todos los usuarios de Adobe Experience Cloud.

### ¿Qué está cambiando?

El 15 de octubre, el acceso a Assurance se gestionará mediante un Admin Console. Lea el [guía de acceso del usuario](./user-access.md) para asegurarse de que sigue teniendo acceso ininterrumpido.

No se esperan otros cambios o interrupciones en las integraciones, sesiones y eventos de Assurance existentes. Se puede seguir accediendo al seguro a través de: [https://griffon.adobe.com](https://griffon.adobe.com) **o** puede utilizar (y marcar) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## ¿Qué puede hacer Assurance por usted?

### Configuración rápida

Empiece rápidamente con algunas líneas de código. En el caso de las aplicaciones móviles, Assurance trabaja con el SDK de Adobe Experience Platform Mobile para ayudarle a inspeccionar, simular y validar eventos de aplicaciones, señales de ubicación, parámetros de configuración, registros del SDK, información del dispositivo y mucho más.

### Conexión sin complicaciones

Con Assurance, la conexión de la aplicación con Platform es sencilla y fiable. No es necesario usar proxies de red, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) y otras gimnasias de red: la conexión de la aplicación a Assurance es tan sencilla como escanear un código QR o pulsar un botón.

![](./images/index/no-hassle-connection.png)

### Inspección, simulación y validación en tiempo real

Después de conectarse a Assurance, puede inspeccionar los eventos y la actividad de las aplicaciones en directo y filtrar y buscar para eliminar el ruido. Los eventos contienen detalles sobre la validación, depuración y solución de problemas de la implementación de la aplicación móvil. Assurance también le permite realizar capturas de pantalla, simular señales de ubicación y mucho más en tiempo real.

![](./images/index/real-time-insepction.png)

### Integración con Adobe Experience Cloud

Los datos y las experiencias del lado del cliente dependen del contexto en el que los usuarios configuran las reglas, actividades y campañas de informes en las interfaces de usuario centradas en expertos en marketing. Para ayudarle a conectar los puntos entre ambos, integramos soluciones de Adobe Experience Cloud como Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service, etc.

![](./images/index/integration.png)

## Funcionalidades

### Eventos, registros y mucho más del SDK de Adobe Experience Platform Mobile

Assurance le ayuda a inspeccionar los eventos de SDK sin procesar generados por el SDK de Adobe Experience Platform Mobile. Todos los eventos recopilados por el SDK están disponibles para su inspección. Los eventos de SDK se cargan en una vista de lista, ordenados por tiempo. Cada evento tiene una vista detallada que proporciona más detalles. También se proporcionan vistas adicionales para examinar la configuración del SDK, los elementos de datos, los estados compartidos y las versiones de extensión del SDK.

### Adobe Analytics

La vista Adobe Analytics > Eventos de Analytics es una vista centrada que muestra eventos relacionados con su implementación móvil de Adobe Analytics. La vista de lista muestra el ciclo de vida o los eventos de estado o acción, el &quot;estado&quot; posprocesado, junto con los detalles de evento necesarios en una vista con formato especial. El estado Posterior al procesamiento muestra cómo Adobe Analytics procesó el evento después de aplicar las reglas de procesamiento en el evento.

### Adobe Analytics para medios de transmisión

La vista Adobe Analytics > Eventos de Media Analytics muestra los eventos de la implementación de análisis de audio y vídeo. La vista de detalles de eventos muestra metadatos estándar y personalizados que se rastrean en cada sesión de reproducción. Además, puede ver el estado posprocesado y los datos de análisis de medios posprocesados, como el tiempo invertido en los medios o la duración total del búfer.

### Places (Servicios de ubicación)

La vista Servicios de ubicación es una vista en el dispositivo que muestra los eventos de entrada y salida de la ubicación del usuario para facilitar la validación. Esta práctica vista proporciona una interfaz conveniente para ver puntos de datos específicos de la ubicación que se pueden inspeccionar en el cliente para la depuración en contexto.

## ¿Es seguro Assurance?

Assurance cuenta con las siguientes medidas de seguridad:

* Tanto Assurance como la interfaz de usuario web de Assurance tienen un protocolo de enlace seguro basado en PIN para una conexión. El usuario debe crear explícitamente un protocolo de enlace, que evita que el usuario final cree conexiones de seguro &quot;accidentales&quot;.
* Solo se admiten conexiones entre Assurance y la interfaz de usuario web de Assurance que pertenecen al mismo ID de organización de Adobe Experience Cloud.
* Los eventos de SDK de Adobe Experience Platform Mobile se transportan mediante HTTPS.
* Los SDK de Adobe Experience Platform Mobile y Assurance utilizan TLS 1.2
* Las sesiones de seguridad se eliminan a los 30 días.
* Los datos de sesión de seguridad se cifran en reposo, siguiendo las prácticas recomendadas de almacenamiento.

## Primeros pasos

Para configurar Assurance, primero debe instalar la extensión Assurance en la aplicación. Para aprender a hacer esto, lea el tutorial sobre [implementación de la extensión de Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Después de agregar Assurance a la aplicación, puede crear una sesión de Assurance que se pueda conectar al dispositivo. Para aprender a utilizar Assurance, lea la [guía sobre el uso de Assurance](./tutorials/using-assurance.md).
