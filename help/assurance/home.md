---
title: Información general sobre Adobe Experience Platform Assurance
description: Adobe Experience Platform Assurance le permite inspeccionar, comprobar, simular y validar cómo recopila datos o sirve experiencias en sus aplicaciones móviles.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '824'
ht-degree: 100%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance es un producto de [Adobe Experience Cloud](https://www.adobe.com/es/experience-cloud.html) para ayudarle a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil.

>[!IMPORTANT]
>
> El proyecto Griffon ahora se conoce como **Assurance**.
>
> El proyecto Griffon ya está disponible para **todos** los clientes de Adobe Experience Cloud como Assurance. Para obtener más información sobre esta transición, lea la [guía de acceso del usuario](./user-access.md).

>[!INFO]
>
>Las API públicas de Assurance están disponibles.
>
>[Las API de Assurance](https://developer.adobe.com/adobe-assurance-public-apis/) son una colección que permite a los usuarios probar y depurar sus aplicaciones web y móviles, cuando se equipan con el SDK móvil de Adobe Assurance.

## Disponibilidad general

A partir del 15 de octubre de 2022, Assurance estará disponible para Adobe Experience Cloud.

### ¿Qué está cambiando?

El 15 de octubre: el acceso a Assurance se gestionará a través de Admin Console. Lea la [guía de acceso del usuario](./user-access.md) para garantizar que siga teniendo acceso ininterrumpido.

No se esperan otros cambios o interrupciones en las integraciones, sesiones y eventos de Assurance existentes. Se puede seguir accediendo a Assurance a través de [https://griffon.adobe.com](https://griffon.adobe.com) **o** puede utilizar (y añadir como marcador) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## ¿Qué puede hacer Assurance por usted?

### Configuración rápida

Empiece con unas pocas líneas de código. En el caso de las aplicaciones móviles, Assurance funciona con el SDK móvil de Adobe Experience Platform para ayudarle a inspeccionar, simular y validar eventos de aplicaciones, señales de ubicación, parámetros de configuración, registros de SDK, información de dispositivos y mucho más.

### Conexión sin complicaciones

Con Assurance, la conexión de la aplicación con Platform es sencilla y fiable. No es necesario que utilice proxies de red ([MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) u otras gimnasias de red: conectar la aplicación a Assurance es tan fácil como escanear un código QR o pulsar un botón.

![](./images/index/no-hassle-connection.png)

### Inspección, simulación y validación en tiempo real

Después de conectarse a Assurance, puede inspeccionar los eventos y la actividad de las aplicaciones transmitidas en directo y filtrar y buscar para eliminar el ruido. Los eventos contienen detalles sobre la validación, depuración y solución de problemas de la implementación de la aplicación móvil. Assurance también le permite realizar capturas de pantalla, simular señales de ubicación y mucho más en tiempo real.

![](./images/index/real-time-insepction.png)

### Integración con Adobe Experience Cloud

Los datos y las experiencias del lado del cliente se contextualizan según la forma en que los usuarios configuran las reglas de creación de informes, las actividades y las campañas en las interfaces de usuario centradas en los especialistas en marketing. Para ayudarle a conectar los puntos entre ambos, nos integramos con soluciones de Adobe Experience Cloud como Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service y más.

![](./images/index/integration.png)

## Funcionalidades

### Eventos, registros y mucho más del SDK móvil de Adobe Experience Platform

Assurance le ayuda a inspeccionar los eventos de SDK sin procesar generados por el SDK para móviles de Adobe Experience Platform. Todos los eventos recopilados por el SDK están disponibles para su inspección. Los eventos del SDK se cargan en una vista de lista, ordenados por tiempo. Cada evento tiene una vista detallada que proporciona más detalles. También se proporcionan vistas adicionales para examinar la configuración del SDK, los elementos de datos, los estados compartidos y las versiones de extensión del SDK.

### Adobe Analytics

La vista Adobe Analytics > Eventos de Analytics es una vista centrada que muestra eventos relacionados con la implementación de Adobe Analytics Mobile. La vista de lista muestra los eventos de ciclo vital o acción/estado, el “estado” posterior al procesamiento, junto con los detalles de evento necesarios en una vista con formato especial. El estado Posterior al procesamiento muestra cómo Adobe Analytics ha procesado el evento después de aplicar las reglas de procesamiento al evento.

### Adobe Analytics para medios de streaming

La vista Adobe Analytics > Eventos de Media Analytics muestra eventos para la implementación de análisis de audio y vídeo. La vista de detalles de eventos muestra metadatos estándar y personalizados que se rastrean en cada sesión de reproducción. Además, puede ver el estado posprocesado y los datos de análisis de medios posprocesados, como el tiempo invertido en medios o la duración total del búfer.

### Places (Servicios de ubicación)

La vista Servicios de ubicación es una vista en el dispositivo que muestra los eventos de entrada y salida de la ubicación del usuario para facilitar la validación. Esta práctica vista proporciona una interfaz práctica para ver puntos de datos específicos de la ubicación para inspeccionarlos en el cliente y depurarlos en contexto.

## ¿Assurance es seguro?

Assurance dispone de las siguientes medidas de seguridad:

* Tanto Assurance como la interfaz de usuario web de Assurance tienen un protocolo de enlace seguro basado en PIN para la conexión. El usuario debe crear explícitamente un protocolo de enlace, que evita que un usuario final cree conexiones de Assurance “accidentales”.
* Solo se admiten conexiones entre Assurance y la IU web de Assurance que pertenezcan al mismo ID de organización de Adobe Experience Cloud.
* Los eventos del SDK de Adobe Experience Platform Mobile se transportan a través de HTTPS.
* Los SDK de Assurance y Adobe Experience Platform Mobile utilizan TLS 1.2
* Las sesiones de Assurance se eliminan a los 30 días.
* Los datos de la sesión de Assurance se cifran en reposo, según las prácticas recomendadas de almacenamiento.

## Introducción

Para configurar Assurance, primero debe instalar la extensión de Assurance en la aplicación. Para aprender a hacer esto, lea el tutorial sobre [implementación de la extensión Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Después de agregar Assurance a la aplicación, puede crear una sesión de Assurance que se pueda conectar al dispositivo. Para aprender a utilizar Assurance, lea la [guía de uso de Assurance](./tutorials/using-assurance.md).
