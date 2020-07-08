---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Introducción a la API del cliente
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Introducción a la API del cliente

Las guías para la API del cliente requieren una comprensión práctica de los distintos servicios de Platform que intervienen en el uso de la API del cliente. Antes de su inicio, consulte los siguientes documentos:

- [Descripción general](../../xdm/home.md)del sistema del modelo de datos de experiencia (XDM): XDM es el marco fundamental que permite [!DNL Adobe Experience Cloud], con la ayuda de un Experience Platform, entregar el mensaje correcto a la persona correcta, en el canal correcto, en el momento preciso. La metodología en la que se crea el Experience Platform, Sistema XDM, hace operativos los esquemas del modelo de datos de experiencia para su uso por los servicios de Platform.
- [Conceptos básicos de la composición](../../xdm/schema/composition.md)de esquemas: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en [!DNL Adobe Experience Platform].
- [esquemas](../../xdm/tutorials/create-schema-ui.md)de creación: En este tutorial se explican los pasos para crear un esquema con el Editor de Esquemas en Experience Platform.
- [Información general](../../rtcdp/overview.md)sobre el Perfil del cliente en tiempo real: Integrada en [!DNL Adobe Experience Platform]el [!DNL Adobe Real-time Customer Data Platform] (CDP en tiempo real), ayuda a las compañías a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes durante todo el viaje del cliente. CDP en tiempo real combina múltiples fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para proporcionar experiencias personalizadas de uno a uno en todos los canales y dispositivos.
- [Descripción general](../../segmentation/home.md)del servicio de segmentación: La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles de su almacén de perfiles para distinguir un grupo de personas comercializables de su base de clientes. Por ejemplo: en una campaña por correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que desee una audiencia de todos los usuarios que buscaron zapatos deportivos en los últimos 30 días, pero que no completaron una compra. Con diferentes segmentos, puede centrarse en sus distintas audiencias y ofrecer una experiencia de marketing más personalizada.
- [Guía](../../segmentation/tutorials/create-a-segment.md)de usuario del Generador de segmentos: Platform le permite crear segmentos y acceder a ellos fácilmente, así como utilizar diferentes componentes básicos para seguir caracterizándolos.

## Descarga de puntuaciones de AI del cliente

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con la guía [de](./user-guide/configure.md)configuración.

La descarga de puntuaciones de AI del cliente se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de Platform, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Pasos siguientes

Una vez que haya completado los pasos descritos en el documento anterior, visite la documentación de [entrada y salida](./input-output.md) . Este documento ofrece una breve descripción general de los tipos de datos que se utilizan y producen en la API del cliente.