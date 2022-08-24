---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Información general sobre las fuentes de autoservicio (SDK por lotes)
topic-legacy: overview
description: Las fuentes de autoservicio de Adobe Experience Platform (SDK por lotes) son un conjunto de API de configuración que le permiten integrar un origen basado en la API de REST mediante la API de servicio de flujo para llevar los datos al Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Información general sobre fuentes de autoservicio (SDK por lotes)

Las fuentes de autoservicio de Adobe Experience Platform (SDK por lotes) son un marco que le permite integrar un origen basado en la API de REST en el catálogo de fuentes de Experience Platform mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Las fuentes de autoservicio (SDK por lotes) proporcionan un conjunto de API de configuración para crear su propio origen y llevar los datos por lotes al Experience Platform.

Con las fuentes de autoservicio (SDK por lotes), puede:

* Configure e integre un nuevo origen en el catálogo de Experience Platform mediante el [!DNL Flow Service] API.
* Defina especificaciones para su fuente, incluida información relacionada con tipos de autenticación compatibles y cómo se recuperan los datos de los recursos.
* Cree documentación de cara al usuario para la nueva fuente.

La documentación de fuentes de autoservicio proporciona instrucciones para configurar, probar y publicar una integración de fuentes basada en API de REST con Experience Platform, y para que su fuente forme parte del catálogo de fuentes en constante crecimiento.

![catálogo](./assets/catalog.png)

## Comprender las fuentes

El Experience Platform puede ingerir datos de fuentes externas, mientras que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Experience Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Para obtener más información sobre las fuentes y ver una lista de las diferentes fuentes admitidas actualmente en el Experience Platform, consulte [información general sobre fuentes](../home.md).

## Crear un origen

A través de fuentes de autoservicio, puede integrar su propia fuente basada en API de REST y llevar sus datos al Experience Platform con [!DNL Flow Service]. Puede integrar una fuente en el catálogo de fuentes del Experience Platform creando, configurando y enviando la nueva especificación de conexión a través del [!DNL Flow Service] API.

Consulte la guía de [creación de una nueva especificación de conexión](./api/api-overview.md) para obtener información sobre cómo integrar una nueva fuente en Experience Platform.

## Documentar el origen

Una vez creado el origen, consulte la [guía de documentación](./documentation/doc-overview.md) para obtener instrucciones sobre cómo documentar el origen a través de la variable [!DNL GitHub] interfaz web o a través de su propio editor de texto.

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en el Experience Platform:

* Lea el [Guía de API de fuentes de autoservicio (SDK por lotes)](./api/api-overview.md).
   * Lea el [guía de introducción](./api/getting-started.md).
   * Siga el tutorial en [creación de una nueva especificación de conexión](./api/create.md).
   * Siga el tutorial en [actualización de la especificación de conexión](./api/update-connection-specs.md).
   * Siga el tutorial en [adición del nuevo ID de especificación de conexión a una especificación de flujo](./api/update-flow-specs.md)
   * [Enviar el nuevo origen](./api/submit.md).
* Para comprender mejor la estructura y las propiedades de una especificación de conexión, lea la guía sobre [opciones de configuración para orígenes de autoservicio (SDK por lotes)](./config/config.md).
   * Lea la guía de [configuración de las especificaciones de autenticación](./config/authspec.md) para comprender mejor los distintos tipos de autenticación que puede utilizar para su fuente.
   * Lea la guía de [configuración de las especificaciones de origen](./config/sourcespec.md) para obtener información sobre los distintos tipos de paginación, formatos de programación y esquemas personalizados que se pueden configurar para el origen.
   * Lea la guía de [configuración de las especificaciones de exploración](./config/explorespec.md) para obtener información sobre cómo definir los parámetros necesarios para explorar e inspeccionar los objetos contenidos en el origen.
* Para empezar a documentar su fuente, lea la [información general sobre la creación de documentación para fuentes de autoservicio](./documentation/doc-overview.md)
   * Puede usar esta [plantilla de documentación de la API de fuentes](./documentation/template.md) para estructurar la documentación de la API.
   * Puede usar esta [plantilla de documentación de la interfaz de usuario de fuentes](./documentation/ui-template.md) para estructurar la documentación de la interfaz de usuario.
   * Consulte la guía de [uso de la interfaz web de GitHub](./documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub.
   * Consulte la guía de [uso de un editor de texto](./documentation/text-editor.md) para ver los pasos sobre cómo crear documentación utilizando el equipo local.
