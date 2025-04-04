---
keywords: Experience Platform;introducción;inteligencia artificial aplicada a la atribución;temas populares
feature: Attribution AI
title: Introducción a Attribution AI
description: Las siguientes guías requieren una comprensión de los distintos servicios de Adobe Experience Platform implicados en el uso de la inteligencia artificial aplicada a la atribución. Antes de comenzar los tutoriales, revise los siguientes documentos.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 6%

---

# Introducción a Attribution AI

Las siguientes guías requieren una comprensión de los distintos servicios de [!DNL Adobe Experience Platform] relacionados con el uso de la inteligencia artificial aplicada a la atribución. Antes de comenzar los tutoriales, consulte los siguientes documentos:

- [Descripción general del sistema del modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco de trabajo básico que permite a [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, entregar el mensaje correcto a la persona correcta, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se crea Experience Platform, el sistema XDM, pone en funcionamiento los esquemas del modelo de datos de experiencia para su uso en los servicios de Experience Platform.
- [Conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md): este documento proporciona una introducción a los esquemas XDM (Experience Data Model) y a los componentes básicos, principios y prácticas recomendadas para crear esquemas que se utilizarán en [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): En este tutorial se explican los pasos para crear un esquema con el Editor de esquemas en Experience Platform.

Inteligencia artificial aplicada a la atribución requiere conjuntos de datos para ajustarse al esquema de Eventos de experiencia del consumidor (CEE), que es un grupo de campos de esquema [Modelo de datos de experiencia (XDM)](../../xdm/home.md). Póngase en contacto con el servicio de asistencia de Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de gasto en medios están presentes, puede realizar más análisis, como ingresos incrementales y ROI. Si los datos de perfil del cliente están disponibles, puede atribuir más créditos al nivel de perfil del cliente.

## Terminología

- **Evento de conversión:** Cualquier evento digital o interacción digital que los clientes hagan para indicar un hito hacia un objetivo, como registros de conferencias. Otros ejemplos son las conversiones de pago, los registros gratuitos en la cuenta o la calificación para un rasgo.

- **Punto de contacto:** Cualquier evento digital o interacción digital que los clientes realicen en la ruta hacia un objetivo. Algunos ejemplos son los esfuerzos de marketing relacionados con la compra, las impresiones publicitarias de visualización vistas y los clics en búsquedas de pago.

## Descarga de puntuaciones de Attribution AI

>[!NOTE]
>
>Si no necesita descargar las puntuaciones sin procesar, puede omitir este paso y continuar con los [pasos siguientes](#next-steps).

La descarga de puntuaciones de Inteligencia artificial aplicada a la atribución se realiza mediante una combinación de llamadas a la API. Para realizar llamadas a las API de Experience Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de Experience Platform están aislados para zonas protegidas virtuales específicas. Todas las solicitudes a las API de Experience Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas de Experience Platform.

## Control de acceso {#access-control}

Cuando se usa el control de acceso basado en roles, los privilegios **Ver inteligencia artificial aplicada a la atribución** y **Administrar inteligencia artificial aplicada a la atribución** conceden acceso a diferentes funcionalidades de inteligencia artificial aplicada a la atribución. La inteligencia artificial aplicada a la atribución **Manage** le permite **crear**, **clonar**, **editar**, **eliminar**, **habilitar** o **deshabilitar** una instancia, mientras que la inteligencia artificial aplicada a la atribución **Ver** le permite **leerla** o **verla**. Los registros de auditoría registran las acciones **create**, **edit** y **delete**.

Consulte la documentación para obtener información sobre [asignación de permisos para el control de acceso](../../../help/access-control/home.md) o cómo [usar registros de auditoría para supervisar el acceso y la actividad](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Pasos siguientes {#next-steps}

Una vez que esté listo y tenga todas sus credenciales y esquemas implementados, comience por seguir la [guía de interfaz de usuario de inteligencia artificial aplicada a la atribución](./user-guide.md). Esta guía le explica cómo crear una instancia y enviarla para formación y puntuación.
