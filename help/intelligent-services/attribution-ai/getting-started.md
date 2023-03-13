---
keywords: Experience Platform;introducción;inteligencia artificial aplicada a la atribución;temas populares
feature: Attribution AI
title: Introducción a Attribution AI
description: Las siguientes guías requieren una comprensión de los distintos servicios de Adobe Experience Platform relacionados con el uso de Attribution AI. Antes de comenzar los tutoriales, revise los siguientes documentos.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Introducción a Attribution AI

Las siguientes guías requieren una comprensión de las distintas [!DNL Adobe Experience Platform] servicios relacionados con el uso de Attribution AI. Antes de comenzar los tutoriales, consulte los siguientes documentos:

- [Información general del sistema del modelo de datos de experiencia (XDM)](../../xdm/home.md): XDM es el marco de trabajo básico que permite [!DNL Adobe Experience Cloud], con tecnología de Experience Platform, para enviar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se crea el Experience Platform, el sistema XDM, pone en funcionamiento los esquemas del modelo de datos de experiencia para que los utilicen los servicios de Platform.
- [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Este documento proporciona una introducción a los esquemas XDM (Experience Data Model) y a los componentes básicos, principios y prácticas recomendadas para componer esquemas que se utilizarán en [!DNL Adobe Experience Platform].
- [Creación de esquemas](../../xdm/tutorials/create-schema-ui.md): Este tutorial cubre los pasos para crear un esquema con el Editor de esquemas en Experience Platform.

Attribution AI requiere que los conjuntos de datos se ajusten al esquema de Eventos de experiencia del consumidor (CEE), que es un [Modelo de datos de experiencia (XDM)](../../xdm/home.md) grupo de campos de esquema. Póngase en contacto con el servicio de asistencia al Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de gasto en medios están presentes, puede realizar más análisis, como ingresos incrementales y ROI. Si los datos de perfil del cliente están disponibles, puede atribuir más créditos al nivel de perfil del cliente.

## Terminología

- **Evento de conversión:** Cualquier evento digital o interacción digital que los clientes realicen para indicar un hito hacia un objetivo, como los registros en la conferencia. Otros ejemplos son las conversiones de pago, los registros gratuitos en la cuenta o la calificación para un rasgo.

- **Touchpoint:** Cualquier evento digital o interacción digital que los clientes realicen en el camino hacia un objetivo. Algunos ejemplos son los esfuerzos de marketing relacionados con la compra, las impresiones publicitarias de visualización vistas y los clics en búsquedas de pago.

## Descarga de puntuaciones de Attribution AI

>[!NOTE]
>
>Si no necesita descargar puntuaciones sin procesar, puede omitir este paso y continuar con la [pasos siguientes](#next-steps).

La descarga de puntuaciones de Attribution AI se realiza mediante una combinación de llamadas de API. Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de Experience Platform están aislados para zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de Platform, consulte la [documentación general de zona protegida](../../sandboxes/home.md).

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Control de acceso {#access-control}

Al utilizar el control de acceso basado en funciones, la variable **Ver Attribution AI** y **Administrar Attribution AI** Los privilegios de conceden acceso a diferentes funcionalidades de Attribution AI. El **Administrar Attribution AI** le permite **crear**, **clonar**, **editar**, **eliminar**, **habilitar**, o **disable** una instancia mientras **Ver Attribution AI** le permite **leer** o **vista** it. El **crear**, **editar** y **eliminar** las acciones se registran mediante registros de auditoría.

Consulte la documentación para aprender [asignación de permisos para el control de acceso](../../../help/access-control/home.md) o cómo [usar registros de auditoría para monitorizar el acceso y la actividad](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Pasos siguientes {#next-steps}

Una vez que esté listo y tenga todas las credenciales y esquemas implementados, comience por seguir el [guía de interfaz de usuario de Attribution AI](./user-guide.md). Esta guía le explica cómo crear una instancia y enviarla para formación y puntuación.
