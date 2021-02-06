---
keywords: Experience Platform;introducción;atribución ai;temas populares
solution: Experience Platform, Intelligent Services
title: Introducción a Attribution AI
topic: Getting started
description: Las siguientes guías requieren comprender los distintos servicios de Adobe Experience Platform que se utilizan para utilizar Attribution AI. Antes de comenzar los tutoriales, revise los siguientes documentos.
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Introducción a Attribution AI

Las siguientes guías requieren comprender los distintos [!DNL Adobe Experience Platform] servicios que se utilizan en el uso de Attribution AI. Antes de comenzar los tutoriales, revise los siguientes documentos:

- [Descripción general](../../xdm/home.md) del sistema del modelo de datos de experiencia (XDM): XDM es el marco fundamental que permite  [!DNL Adobe Experience Cloud], con la ayuda de un Experience Platform, entregar el mensaje correcto a la persona correcta, en el canal correcto, en el momento preciso. La metodología en la que se crea el Experience Platform, Sistema XDM, hace operativos los esquemas del modelo de datos de experiencia para que los utilicen los servicios de plataforma.
- [Conceptos básicos de la composición](../../xdm/schema/composition.md) de esquemas: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en  [!DNL Adobe Experience Platform].
- [Esquemas](../../xdm/tutorials/create-schema-ui.md) de creación: Este tutorial trata los pasos para crear un esquema con el Editor de Esquemas en Experience Platform.

Attribution AI requiere que los conjuntos de datos cumplan el esquema Eventos de experiencias del consumidor (CEE), que es una mezcla en el [Modelo de datos de experiencia](../../xdm/home.md) (XDM). Póngase en contacto con la asistencia de Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de inversión de medios están presentes, puede realizar más análisis, como por ejemplo ingresos incrementales y retorno de la inversión. Si los datos de perfil del cliente están disponibles, puede atribuir créditos adicionales al nivel de perfil del cliente.

## Terminología

- **Evento de conversión:** cualquier evento digital o interacción digital que los clientes realicen para indicar un hito hacia un objetivo, como los registros de conferencias. Algunos ejemplos adicionales son: conversiones de pago, suscripciones a cuentas gratuitas o requisitos para una característica.

- **Touchpoint:** cualquier evento digital o interacción digital que los clientes realicen en el camino hacia un objetivo. Algunos ejemplos son los esfuerzos de mercadotecnia antes de la compra, las impresiones de publicidad de visualización vistas y los clics de búsqueda paga.

## Descarga de puntuaciones de Attribution AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con los [pasos siguientes](#next-steps).

La descarga de puntuaciones de Attribution AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de plataforma, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en la plataforma, consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Pasos siguientes {#next-steps}

Una vez que esté listo y tenga todas sus credenciales y esquemas en su lugar, inicio siguiendo la [guía de la interfaz de usuario de Attribution AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia y enviarla para capacitación y puntuación.