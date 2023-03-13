---
keywords: Experience Platform;inicio;temas populares;api;control de acceso basado en atributos;Control de acceso basado en atributos
solution: Experience Platform
title: Guía de API de control de acceso basado en atributos
description: La API de control de acceso basada en atributos le permite administrar mediante programación las funciones y las directivas de acceso dentro de Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 5%

---

# Guía de API de control de acceso basado en atributos

El control de acceso basado en atributos es una capacidad de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funcionalidades basadas en atributos. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo o segmento de esquema. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios.

La API de control de acceso basada en atributos se utiliza para acceder a funciones, productos, categorías de permisos y conjuntos de permisos dentro de Adobe Experience Platform, lo que proporciona una interfaz de usuario y una API RESTful desde las que se puede acceder a todos los recursos de biblioteca disponibles.

>[!IMPORTANT]
>
>El control de acceso basado en atributos no se debe confundir con las capacidades de control de datos de Experience Platform, que le permiten utilizar etiquetas y directivas para controlar cómo se utilizan los datos en Platform en lugar de qué usuarios de su organización tienen acceso a ellos. Consulte la [Guía de API del servicio de directivas](../../../data-governance/api/overview.md) para ver los pasos sobre cómo aprovechar estas capacidades mediante programación.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

## Funciones

Las funciones definen el acceso que un administrador, un especialista o un usuario final tiene a los recursos de su organización. En un entorno de control de acceso basado en funciones, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el ámbito de acceso de visualización o escritura que necesiten. Consulte la [guía de extremo de funciones](./roles.md) para obtener más información sobre cómo trabajar con funciones en la API.

## Políticas

Las políticas son declaraciones que unen atributos para establecer acciones permisibles e inadmisibles. Las directivas pueden ser locales o globales, y pueden anular otras directivas. El `/policies` el punto de conexión le permite administrar directivas mediante programación en su organización. Consulte la [guía de extremo de directivas](./policies.md) para obtener más información sobre cómo trabajar con directivas en la API.

## Productos

El `/products` Este extremo de la API de control de acceso basado en atributos le permite administrar mediante programación productos, así como categorías de permisos y conjuntos de permisos asociados a productos de su organización. Consulte la [guía de extremo de productos](./products.md) para obtener más información sobre cómo trabajar con productos y sus categorías de permisos y conjuntos de permisos correspondientes en la API.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de control de acceso basada en atributos, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
