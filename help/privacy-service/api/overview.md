---
title: Guía de API del Privacy Service
description: Aprenda a utilizar la API de Privacy Service para administrar mediante programación los trabajos de privacidad de aplicaciones de Adobe Experience Cloud compatibles.
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Guía de la API de [!DNL Privacy Service]

La API de Privacy Service proporciona varios extremos que le permiten administrar mediante programación los trabajos de privacidad de su organización. Estos extremos se describen a continuación. Visite las guías de puntos de conexión individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

>[!NOTE]
>
>Esta guía explica cómo usar la variable [!DNL Privacy Service] API. Para obtener más información sobre cómo utilizar la interfaz de usuario, consulte la [Información general sobre la IU de Privacy Service](../ui/overview.md).

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Referencia de la API del Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Trabajos de privacidad

Cuando el Privacy Service recibe una solicitud para acceder a los datos personales de un asunto o eliminarlos, el sistema crea trabajos de privacidad para satisfacer dicha solicitud. Cada trabajo de privacidad contiene información de identidad relacionada con el interesado, metadatos sobre el producto de Adobe Experience Cloud al que se aplica el trabajo y el estado de procesamiento del trabajo.

La variable `/jobs` El punto final le permite crear y recuperar trabajos de privacidad para su organización. Para aprender a utilizar este extremo, consulte la [guía de extremo sobre trabajos de privacidad](./privacy-jobs.md).

## Consentimiento

Algunas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. La variable `/consent` permite procesar solicitudes de consentimiento del cliente e integrarlas en su flujo de trabajo de privacidad. Consulte la [guía de extremo de consentimiento](./consent.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del Privacy Service, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos.
