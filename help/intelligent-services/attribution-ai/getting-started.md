---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Introducción a la API de atribución
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Introducción a la API de atribución

Las siguientes guías requieren comprender los distintos [!DNL Adobe Experience Platform] servicios relacionados con el uso de Atribución AI. Antes de comenzar los tutoriales, revise los siguientes documentos:

- [Descripción general](../../xdm/home.md)del sistema del modelo de datos de experiencia (XDM): XDM es el marco fundamental que permite [!DNL Adobe Experience Cloud], con la ayuda de un Experience Platform, entregar el mensaje correcto a la persona correcta, en el canal correcto, en el momento preciso. La metodología en la que se crea el Experience Platform, Sistema XDM, hace operativos los esquemas del modelo de datos de experiencia para su uso por los servicios de Platform.
- [Conceptos básicos de la composición](../../xdm/schema/composition.md)de esquemas: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en [!DNL Adobe Experience Platform].
- [esquemas](../../xdm/tutorials/create-schema-ui.md)de creación: En este tutorial se explican los pasos para crear un esquema con el Editor de Esquemas en Experience Platform.

La API de atribución requiere que los conjuntos de datos se ajusten al esquema de Eventos de experiencias del consumidor (CEE), que es una mezcla en el Modelo [de datos de](../../xdm/home.md) experiencia (XDM). Póngase en contacto con el servicio de asistencia de Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de inversión de medios están presentes, puede realizar más análisis, como por ejemplo ingresos incrementales y retorno de la inversión. Si los datos de perfil del cliente están disponibles, puede atribuir créditos adicionales al nivel de perfil del cliente.

## Terminología

- **evento de conversión:** Cualquier evento digital o interacción digital que los clientes realicen para indicar un hito hacia un objetivo, como los registros de conferencias. Algunos ejemplos adicionales son: conversiones de pago, suscripciones a cuentas gratuitas o requisitos para una característica.

- **Touchpoint:** Cualquier evento digital o interacción digital que los clientes realicen en el camino hacia un objetivo. Algunos ejemplos son los esfuerzos de mercadotecnia antes de la compra, las impresiones de publicidad de visualización vistas y los clics de búsqueda paga.

## Descarga de puntuaciones de Atribución-AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con los [siguientes pasos](#next-steps).

La descarga de puntuaciones de Atribución de AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

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

## Pasos siguientes {#next-steps}

Una vez que esté listo y tenga todas sus credenciales y esquemas en su lugar, inicio siguiendo la guía de la interfaz de usuario de [Atribución de archivos AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia y enviarla para capacitación y puntuación.