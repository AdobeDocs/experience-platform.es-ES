---
keywords: Experience Platform;introducción;ayuda al cliente;temas populares
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Introducción a Customer AI
description: Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 596921163bf64d11545dcde49039bcdd07c253dd
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Introducción a Customer AI

Las guías para Customer AI requieren comprender bien los distintos servicios de Platform implicados en el uso de Customer AI. Antes de comenzar, revise los siguientes documentos:

- [Descripción general del sistema del Modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco base que permite [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, para enviar el mensaje correcto a la persona correcta, en el canal correcto, en el momento justo. La metodología en la que se basa el Experience Platform, el sistema XDM, operacionaliza los esquemas del Modelo de datos de experiencia para que los utilicen los servicios de plataforma.
- [Aspectos básicos de la composición del esquema](../../xdm/schema/composition.md): Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se van a utilizar en [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.
- [Resumen del perfil del cliente en tiempo real](../../rtcdp/overview.md): Integrado en [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform (Real-Time CDP) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes en todo el recorrido de clientes. Real-Time CDP combina varias fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para ofrecer experiencias personalizadas de cliente personalizadas y personalizadas en todos los canales y dispositivos.
- [Información general del servicio de segmentación](../../segmentation/home.md): La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que quiera una audiencia de todos los usuarios que buscaron zapatillas en los últimos 30 días, pero que no completaron una compra. Con distintos segmentos, puede centrarse en las distintas audiencias y ofrecer una experiencia de marketing más personalizada.
- [Guía del usuario del Generador de segmentos](../../segmentation/tutorials/create-a-segment.md): Platform le permite crear y acceder fácilmente a segmentos, así como utilizar diferentes componentes básicos para caracterizar aún más sus segmentos.

## Descarga de puntuaciones de Customer AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con el [guía de configuración](./user-guide/configure.md).

La descarga de puntuaciones de Customer AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en Platform, consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Pasos siguientes

Una vez que haya completado los pasos descritos en el documento anterior, visite la [Entrada y salida](./input-output.md) documentación. Este documento ofrece una breve descripción general de los tipos de datos que se utilizan y producen en Customer AI.
