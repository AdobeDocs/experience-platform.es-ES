---
keywords: Experience Platform;introducción;inteligencia artificial aplicada al cliente;temas populares
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Introducción a Customer AI
description: Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 8%

---

# Introducción a Customer AI

Las guías de Customer AI requieren una comprensión práctica de los distintos servicios de Platform implicados en el uso de Customer AI. Antes de empezar, revise los siguientes documentos:

- [Información general del sistema del modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco de trabajo básico que permite [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, para enviar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se crea el Experience Platform, el sistema XDM, pone en funcionamiento los esquemas del modelo de datos de experiencia para que los utilicen los servicios de Platform.
- [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Este documento proporciona una introducción a los esquemas XDM (Experience Data Model) y a los componentes básicos, principios y prácticas recomendadas para componer esquemas que se utilizarán en [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial cubre los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
- [Resumen del perfil del cliente en tiempo real](../../rtcdp/overview.md): compilado en [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform (Real-Time CDP) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido del cliente. Real-Time CDP combina varias fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.
- [Resumen del servicio de segmentación](../../segmentation/home.md): la segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Se olvidó de comprar sus zapatillas de deporte?&quot;, es posible que desee una audiencia de todos los usuarios que buscaron zapatillas de running en los últimos 30 días, pero que no completaron una compra. Con diferentes segmentos, puede centrarse en sus distintas audiencias y ofrecer una experiencia de marketing más personalizada.
- [Guía del usuario del Generador de segmentos](../../segmentation/tutorials/create-a-segment.md): Platform le permite crear y acceder fácilmente a segmentos, así como utilizar diferentes componentes básicos para caracterizar aún más sus segmentos.

## Descarga de puntuaciones de Customer AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con la [guía de configuración](./user-guide/configure.md).

La descarga de las puntuaciones de inteligencia artificial aplicada al cliente se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de Experience Platform están aislados para zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de Platform, consulte la [documentación general de zona protegida](../../sandboxes/home.md).

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Pasos siguientes

Una vez que haya completado los pasos descritos en el documento anterior, visite la [Entrada y salida](./data-requirements.md) documentación. Este documento proporciona una breve descripción de qué tipos de datos se utilizan y producen en la inteligencia artificial aplicada al cliente.
