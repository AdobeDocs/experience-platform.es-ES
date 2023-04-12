---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de entornos limitados
solution: Experience Platform
title: Guía de la API de Sandbox
description: Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno de producción.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# Guía de la API de [!DNL Sandbox]

La variable [!DNL Sandbox] La API de proporciona varios extremos que le permiten administrar mediante programación todos los entornos limitados disponibles para su organización. Estos extremos se describen a continuación. Visite las guías de puntos de conexión individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y todas las operaciones de CRUD, visite [[!DNL Sandbox] Referencia de API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Entornos aislados disponibles

El extremo de entornos limitados disponible le permite ver una lista de todos los entornos limitados disponibles para el usuario actual, incluida la información sobre el nombre, el título, el estado, el tipo y la región de cada entorno limitado. El extremo de entornos limitados disponible en la variable [!DNL Sandbox] Todos los usuarios pueden acceder a la API, incluidos los que no tienen permisos de acceso de Administración de espacio aislado. Consulte la [guía de extremo de entornos limitados disponibles](./available.md) para obtener información sobre cómo ver los entornos limitados disponibles en la API.

## Administración de Simuladores para pruebas

Un entorno limitado es una partición virtual dentro de una sola instancia de Adobe Experience Platform, que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital. Puede crear, ver, editar, restablecer y eliminar entornos limitados de producción y desarrollo utilizando la variable `/sandboxes` punto final. Para aprender a utilizar este extremo, consulte la [guía de extremo de entornos limitados](./sandboxes.md).

## Tipos de Simulador para pruebas

Actualmente, los tipos de simulación de pruebas admitidos en el Experience Platform son los entornos limitados de producción y desarrollo. Una licencia predeterminada de Platform le otorga un total de cinco entornos limitados, que puede clasificar como de producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 entornos limitados hasta un máximo de 75 entornos limitados en total. Consulte la [guía de extremo de tipos de entorno limitado](./types.md) para aprender a ver los tipos de entornos limitados admitidos para su organización en la API.

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Sandbox] API, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos.
