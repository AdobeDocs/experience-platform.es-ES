---
keywords: Experience Platform;introducción;ai de atribución;temas populares
solution: Experience Platform, Intelligent Services
title: Introducción a Attribution AI
topic-legacy: Getting started
description: Las siguientes guías requieren comprender los distintos servicios de Adobe Experience Platform implicados en el uso de Attribution AI. Antes de comenzar los tutoriales, revise los siguientes documentos.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Introducción a Attribution AI

Las siguientes guías requieren comprender los distintos servicios [!DNL Adobe Experience Platform] implicados en el uso de Attribution AI. Antes de comenzar los tutoriales, revise los siguientes documentos:

- [Descripción general del sistema del Modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco fundamental que permite  [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. La metodología en la que se basa el Experience Platform, el sistema XDM, operacionaliza los esquemas del Modelo de datos de experiencia para que los utilicen los servicios de plataforma.
- [Aspectos básicos de la composición](../../xdm/schema/composition.md) del esquema: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se van a utilizar en  [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial trata los pasos para crear un esquema con el Editor de esquemas en Experience Platform.

Attribution AI requiere que los conjuntos de datos se ajusten al esquema de Eventos de experiencias del consumidor (EEC), que es un grupo de campos de esquema [Modelo de datos de experiencia (XDM)](../../xdm/home.md) . Póngase en contacto con el servicio de asistencia al Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de gasto de medios están presentes, puede realizar más análisis, como ingresos incrementales y ROI. Si los datos de perfil del cliente están disponibles, puede atribuir créditos al nivel de perfil del cliente.

## Terminología

- **Evento de conversión:**  cualquier evento digital o interacción digital que los clientes realicen para indicar un hito hacia un objetivo, como los registros de conferencia. Otros ejemplos son las conversiones de pago, los registros de cuenta gratuitos o la calificación para un rasgo.

- **Touchpoint:** cualquier evento digital o interacción digital que los clientes realicen en la ruta hacia un objetivo. Algunos ejemplos son los esfuerzos de marketing relacionados con las compras previas, las impresiones publicitarias de visualización vistas y los clics de búsqueda pagada.

## Descarga de puntuaciones de Attribution AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con los [siguientes pasos](#next-steps).

La descarga de puntuaciones de Attribution AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

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

## Pasos siguientes {#next-steps}

Una vez que esté listo y tenga todas sus credenciales y esquemas en su lugar, comience por seguir la [guía de la interfaz de usuario de Attribution AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia y la envía para formación y puntuación.
