---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Información general del SDK de fuentes (Beta)
topic-legacy: overview
description: El SDK de fuentes de Adobe Experience Platform es un conjunto de API de configuración que le permiten integrar un origen basado en la API de REST mediante la API de servicio de flujo para llevar los datos al Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Información general del SDK de fuentes (Beta)

>[!IMPORTANT]
>
>El SDK de fuentes se encuentra en la versión beta y es posible que su organización no tenga acceso a él todavía. La funcionalidad descrita en esta documentación está sujeta a cambios.

El SDK de fuentes de Adobe Experience Platform es un conjunto de API de configuración que le permiten integrar un origen basado en la API de REST mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para llevar los datos al Experience Platform.

Con el SDK de fuentes, puede:

* Configure un nuevo origen en el catálogo de Platform, completo con las funcionalidades crear, leer, actualizar y eliminar usando la variable [!DNL Flow Service] API.
* Defina especificaciones para su fuente, incluida información relacionada con tipos de autenticación compatibles y cómo se recuperan los datos de los recursos.
* Cree documentación de cara al usuario para la nueva fuente.

La documentación del SDK de fuentes proporciona instrucciones para utilizar el SDK de fuentes de Adobe Experience Platform para configurar, probar y publicar una integración de fuentes basada en la API de REST con Platform, y para que su origen forme parte del catálogo de fuentes en constante crecimiento.

![catálogo](./assets/catalog.png)

## Comprender las fuentes

Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Para obtener más información sobre las fuentes y ver una lista de las diferentes fuentes admitidas actualmente en Platform, consulte [información general sobre fuentes](../home.md).

## Crear un origen

A través del SDK de fuentes, puede integrar su propio origen basado en API de REST y llevar sus datos a Platform con [!DNL Flow Service]. El SDK de fuentes le permite integrar una nueva fuente con Platform, creando y enviando una nueva especificación de conexión a través del [!DNL Flow Service] API.

Consulte la guía de [creación de una nueva especificación de conexión](./api/api-overview.md) para obtener información sobre cómo integrar una nueva fuente en Platform.

## Documentar el origen

Una vez creado el origen, consulte la [guía de documentación](./documentation/doc-overview.md) para obtener instrucciones sobre cómo documentar el origen a través de la variable [!DNL GitHub] interfaz web o a través de su propio editor de texto.

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en el Experience Platform:

* Lea el [Guía de API del SDK de fuentes](./api/api-overview.md);
   * Lea el [guía de introducción](./api/getting-started.md);
   * Siga el tutorial en [creación de una nueva especificación de conexión](./api/create.md);
   * Siga el tutorial en [actualización de la especificación de conexión](./api/update-connection-specs.md);
   * Siga el tutorial en [adición del nuevo ID de especificación de conexión a una especificación de flujo](./api/update-flow-specs.md)
   * [Enviar el nuevo origen](./api/submit.md).
* Para comprender mejor la estructura y las propiedades de una especificación de conexión, consulte la guía de [opciones de configuración del SDK de fuentes](./config/config.md);
   * Consulte la guía de [configuración de las especificaciones de autenticación](./config/authspec.md);
   * Consulte la guía de [configuración de las especificaciones de origen](./config/sourcespec.md);
   * Consulte la guía de [configuración de las especificaciones de exploración](./config/explorespec.md);
* Para empezar a documentar la fuente, consulte la [información general sobre la creación de documentación para el SDK de fuentes](./documentation/doc-overview.md)
   * Puede usar esta [plantilla de documentación de fuentes](./documentation/template.md) para estructurar la documentación;
   * Consulte la guía de [uso de la interfaz web de GitHub](./documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub;
   * Consulte la guía de [uso de un editor de texto](./documentation/text-editor.md) para ver los pasos sobre cómo crear documentación utilizando el equipo local.

