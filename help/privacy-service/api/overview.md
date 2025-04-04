---
title: Guía de API de Privacy Service
description: Aprenda a utilizar la API de Privacy Service para administrar mediante programación los trabajos de privacidad para las aplicaciones de Adobe Experience Cloud admitidas.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---

# Guía de la API de [!DNL Privacy Service]

La API de Privacy Service proporciona varios extremos que le permiten administrar mediante programación los trabajos de privacidad de su organización. Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de muestra y mucho más.

>[!NOTE]
>
>Esta guía explica cómo usar la API [!DNL Privacy Service]. Para obtener más información sobre cómo usar la interfaz de usuario, consulte la [descripción general de la interfaz de usuario del Privacy Service](../ui/overview.md).

Para ver todos los extremos disponibles y las operaciones de CRUD, visite [Referencia de API de Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Trabajos de privacidad

Cuando el Privacy Service recibe una solicitud para acceder a los datos personales de un sujeto o eliminarlos, el sistema crea trabajos de privacidad para cumplir con esa solicitud. Cada trabajo de privacidad contiene información de identidad relacionada con el interesado, metadatos sobre el producto de Adobe Experience Cloud al que se aplica el trabajo y el estado de procesamiento del trabajo.

El extremo `/jobs` le permite crear y recuperar trabajos de privacidad para su organización. Para obtener información sobre cómo utilizar este extremo, consulte la [guía de extremo de trabajos de privacidad](./privacy-jobs.md).

## Consentimiento

Ciertas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. El punto de conexión `/consent` le permite procesar las solicitudes de consentimiento de los clientes e integrarlas en el flujo de trabajo de privacidad. Consulte la [guía de extremo de consentimiento](./consent.md) para obtener más información.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Privacy Service, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
