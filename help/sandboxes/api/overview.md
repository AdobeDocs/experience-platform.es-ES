---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de espacios aislados
solution: Experience Platform
title: Guía de API de zona protegida
description: Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno de producción.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Guía de la API de [!DNL Sandbox]

El [!DNL Sandbox] La API proporciona varios extremos que le permiten administrar mediante programación todos los entornos limitados disponibles en su organización. Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [[!DNL Sandbox] Referencia de API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Zonas protegidas disponibles

El extremo de las zonas protegidas disponibles le permite ver una lista de todas las zonas protegidas disponibles para el usuario actual, incluida la información sobre el nombre, el título, el estado, el tipo y la región de cada zona protegida. El extremo de las zonas protegidas disponibles en la variable [!DNL Sandbox] Todos los usuarios, incluidos los que no tienen permisos de acceso de administración de zonas protegidas, pueden acceder a la API. Consulte la [guía de extremo de zonas protegidas disponibles](./available.md) para obtener información sobre cómo ver los entornos limitados disponibles en la API.

## Administración de zona protegida

Una zona protegida es una partición virtual dentro de una sola instancia de Adobe Experience Platform, que permite una integración perfecta con el proceso de desarrollo de sus aplicaciones de experiencia digital. Puede crear, ver, editar, restablecer y eliminar entornos limitados de producción y desarrollo mediante las siguientes opciones `/sandboxes` punto final. Para obtener información sobre cómo utilizar este extremo, consulte la [guía de extremo de zonas protegidas](./sandboxes.md).

## Tipos de zonas protegidas

Actualmente, los tipos de zonas protegidas admitidos en Experience Platform son zonas protegidas de producción y desarrollo. Una licencia de Platform predeterminada le concede un total de cinco zonas protegidas, que puede clasificar como producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 zonas protegidas, hasta un máximo de 75 zonas protegidas en total. Consulte la [guía de extremo de tipos de zona protegida](./types.md) para obtener información sobre cómo ver los tipos de zonas protegidas admitidos para su organización en la API.

## Pasos siguientes

Para empezar a realizar llamadas utilizando [!DNL Sandbox] API, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
