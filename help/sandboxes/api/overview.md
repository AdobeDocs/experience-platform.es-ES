---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de entornos limitados
solution: Experience Platform
title: Guía de la API de Sandbox
topic-legacy: developer guide
description: Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno de producción.
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Sandbox] Guía de API

La API [!DNL Sandbox] proporciona varios extremos que le permiten administrar mediante programación todos los entornos limitados disponibles para usted dentro de su organización de IMS. Estos extremos se describen a continuación. Visite las guías de puntos finales individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [[!DNL Sandbox] referencia de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml).

## Entornos aislados disponibles

El extremo de entornos limitados disponible le permite ver una lista de todos los entornos limitados disponibles para el usuario actual, incluida la información sobre el nombre, el título, el estado, el tipo y la región de cada entorno limitado. Todos los usuarios pueden acceder al extremo de los entornos limitados disponibles en la API [!DNL Sandbox], incluidos los que no tienen permisos de acceso de Administración de entornos limitados. Consulte la [guía de extremo de entornos limitados disponibles](./available.md) para obtener información sobre cómo ver los entornos limitados disponibles en la API.

## Administración de Simuladores para pruebas

Un entorno limitado es una partición virtual dentro de una sola instancia de Adobe Experience Platform, que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital. Puede crear, ver, editar, restablecer y eliminar entornos limitados de producción y desarrollo utilizando el extremo `/sandboxes` . Para aprender a utilizar este extremo, consulte la [guía de extremo de entornos limitados](./sandboxes.md).

## Tipos de Simulador para pruebas

Actualmente, los tipos de simulación de pruebas admitidos en el Experience Platform son los entornos limitados de producción y desarrollo. Una licencia predeterminada de Platform le otorga un total de cinco entornos limitados, que puede clasificar como de producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 entornos limitados hasta un máximo de 75 entornos limitados en total. Consulte la [guía de extremo de tipos de entornos limitados](./types.md) para obtener información sobre cómo ver los tipos de entornos limitados admitidos para su organización en la API.

## Pasos siguientes

Para empezar a realizar llamadas con la API [!DNL Sandbox], lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de punto final para aprender a utilizar puntos finales específicos.