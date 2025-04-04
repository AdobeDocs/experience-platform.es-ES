---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
solution: Experience Platform
title: Resumen de Fuentes de Autoservicio (SDK por Lotes)
description: Fuentes de autoservicio de Adobe Experience Platform (SDK por lotes) es un conjunto de API de configuración que le permiten integrar una fuente basada en la API de REST mediante la API de Flow Service para llevar los datos a Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# Resumen de fuentes de autoservicio (SDK por lotes)

Fuentes de autoservicio de Adobe Experience Platform (SDK por lotes) es un módulo que le permite integrar una fuente basada en API de REST en el catálogo de fuentes de Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Fuentes de autoservicio (SDK por lotes) proporciona un conjunto de API de configuración para crear su propia fuente y llevar los datos por lotes a Experience Platform.

Con las fuentes de autoservicio (SDK por lotes), puede:

* Configure e integre un nuevo origen al catálogo de Experience Platform mediante la API [!DNL Flow Service].
* Defina especificaciones para su fuente, incluida la información perteneciente a los tipos de autenticación admitidos y cómo se recuperan los datos de recursos.
* Cree documentación orientada al usuario para la nueva fuente.

La documentación de fuentes de autoservicio proporciona instrucciones para configurar, probar y publicar una integración de fuente basada en la API de REST con Experience Platform, y hacer que su fuente forme parte del creciente catálogo de fuentes.

![catálogo](./assets/catalog.png)

## Explicación de las fuentes

Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Para obtener más información sobre las fuentes y ver una lista de las diferentes fuentes admitidas actualmente en Experience Platform, consulte la [descripción general de las fuentes](../home.md).

## Crear un origen

A través de las fuentes de autoservicio, puede integrar su propia fuente basada en la API de REST y llevar sus datos a Experience Platform con [!DNL Flow Service]. Puede integrar un origen al catálogo de orígenes de Experience Platform creando, configurando y enviando una nueva especificación de conexión mediante la API [!DNL Flow Service].

Consulte la guía sobre [creación de una nueva especificación de conexión](./api/api-overview.md) para obtener información sobre cómo integrar una nueva fuente en Experience Platform.

## Documente su origen

Una vez creado el origen, consulte la [guía de documentación](./documentation/doc-overview.md) para obtener instrucciones sobre cómo documentar el origen a través de la interfaz web de [!DNL GitHub] o a través de su propio editor de texto.

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en Experience Platform:

* Lea la [guía de API de fuentes de autoservicio (SDK por lotes)](./api/api-overview.md).
   * Lea la [guía de introducción](./api/getting-started.md).
   * Siga el tutorial de [creación de una nueva especificación de conexión](./api/create.md).
   * Siga el tutorial de [actualización de la especificación de conexión](./api/update-connection-specs.md).
   * Siga el tutorial de [adición de su nuevo identificador de especificación de conexión a una especificación de flujo](./api/update-flow-specs.md)
   * [Envíe su nuevo origen](./api/submit.md).
* Para comprender mejor la estructura y las propiedades de una especificación de conexión, lea la guía de [opciones de configuración para orígenes de autoservicio (SDK por lotes)](./config/config.md).
   * Lea la guía sobre [configuración de las especificaciones de autenticación](./config/authspec.md) para comprender mejor los distintos tipos de autenticación que puede usar para su origen.
   * Lea la guía sobre [configuración de las especificaciones de origen](./config/sourcespec.md) para obtener información sobre los diferentes tipos de paginación, formatos de programación y esquemas personalizados que se pueden configurar para su origen.
   * Lea la guía sobre [configuración de las especificaciones de exploración](./config/explorespec.md) para obtener información sobre cómo definir los parámetros necesarios para explorar e inspeccionar los objetos contenidos en su origen.
* Para empezar a documentar el origen, lea la [descripción general sobre la creación de documentación para orígenes de autoservicio](./documentation/doc-overview.md)
   * Puede usar esta [plantilla de documentación de API de orígenes](./documentation/template.md) para estructurar su documentación de API.
   * Puede usar esta [plantilla de documentación de IU de orígenes](./documentation/ui-template.md) para estructurar su documentación de IU.
   * Consulte la guía sobre [uso de la interfaz web de GitHub](./documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub.
   * Consulte la guía sobre [uso de un editor de texto](./documentation/text-editor.md) para ver los pasos sobre cómo crear documentación con el equipo local.
