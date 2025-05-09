---
keywords: Experience Platform;inicio;temas populares;api;control de acceso basado en atributos;Control de acceso basado en atributos
solution: Experience Platform
title: Guía de API de control de acceso basado en atributos
description: La API de control de acceso basada en atributos le permite administrar mediante programación las funciones y las directivas de acceso dentro de Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 11%

---

# Guía de API de control de acceso basado en atributos

El control de acceso basado en atributos es una capacidad de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funcionalidades basadas en atributos. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo o segmento de esquema. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios.

La API de control de acceso basada en atributos se utiliza para acceder a funciones, productos, categorías de permisos y conjuntos de permisos dentro de Adobe Experience Platform, lo que proporciona una interfaz de usuario y una API RESTful desde las que se puede acceder a todos los recursos de biblioteca disponibles.

>[!IMPORTANT]
>
>El control de acceso basado en atributos no se debe confundir con las funcionalidades de control de datos de Experience Platform, que le permiten utilizar etiquetas y políticas para controlar cómo se utilizan los datos en Experience Platform en lugar de qué usuarios de su organización tienen acceso a ellos. Consulte la [guía de API del servicio de directivas](../../../data-governance/api/overview.md) para ver los pasos que debe seguir para aprovechar estas capacidades mediante programación.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de muestra y mucho más.

## Funciones

Las funciones definen el acceso que un administrador, un especialista o un usuario final tiene a los recursos de su organización. En un entorno de control de acceso basado en funciones, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el ámbito de acceso de visualización o escritura que necesiten. Consulte la [guía de extremo de funciones](./roles.md) para obtener más información sobre cómo trabajar con funciones en la API.

## Políticas

Las directivas son declaraciones que reúnen atributos para establecer acciones permitidas y no permitidas. Las directivas pueden ser locales o globales, y pueden anular otras directivas. El extremo `/policies` le permite administrar directivas mediante programación en su organización. Consulte la [guía de extremo de directivas](./policies.md) para obtener más información sobre cómo trabajar con directivas en la API.

## Productos

El extremo `/products` de la API de control de acceso basado en atributos le permite administrar mediante programación productos, así como categorías de permisos y conjuntos de permisos asociados a productos de su organización. Consulte la [guía de extremo de productos](./products.md) para obtener más información sobre cómo trabajar con productos y sus categorías de permisos y conjuntos de permisos correspondientes en la API.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de control de acceso basada en atributos, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
