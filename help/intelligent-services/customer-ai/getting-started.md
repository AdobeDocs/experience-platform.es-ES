---
keywords: Experience Platform;introducción;ayuda al cliente;temas populares
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Introducción a Customer AI
topic-legacy: Getting started
description: Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Introducción a Customer AI

Las guías para Customer AI requieren comprender bien los distintos servicios de Platform implicados en el uso de Customer AI. Antes de comenzar, revise los siguientes documentos:

- [Descripción general del sistema del Modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco fundamental que permite  [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. La metodología en la que se basa el Experience Platform, el sistema XDM, operacionaliza los esquemas del Modelo de datos de experiencia para que los utilicen los servicios de plataforma.
- [Aspectos básicos de la composición](../../xdm/schema/composition.md) del esquema: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se van a utilizar en  [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
- [Información general del perfil del cliente en tiempo real](../../rtcdp/overview.md): Real-time Customer Data Platform (CDP en tiempo real), integrado en  [!DNL Adobe Experience Platform], ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes en todo el recorrido de clientes. CDP en tiempo real combina varias fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para proporcionar experiencias personalizadas de cliente individuales en todos los canales y dispositivos.
- [Información general del servicio de segmentación](../../segmentation/home.md): La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que quiera una audiencia de todos los usuarios que buscaron zapatillas en los últimos 30 días, pero que no completaron una compra. Con distintos segmentos, puede centrarse en las distintas audiencias y ofrecer una experiencia de marketing más personalizada.
- [Guía](../../segmentation/tutorials/create-a-segment.md) del usuario del Generador de segmentos: Platform le permite crear y acceder fácilmente a segmentos, así como utilizar diferentes componentes básicos para caracterizar aún más sus segmentos.

## Descarga de puntuaciones de Customer AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con la [guía de configuración](./user-guide/configure.md).

La descarga de puntuaciones de Customer AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en Platform, consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Pasos siguientes

Una vez que haya completado los pasos descritos en el documento anterior, visite la documentación de [Entrada y salida](./input-output.md). Este documento ofrece una breve descripción general de los tipos de datos que se utilizan y producen en Customer AI.
