---
title: Guía de API de Sandbox Tools
description: La función Herramientas para zonas protegidas de Adobe Experience Platform permite exportar e importar una instantánea de las configuraciones de las zonas protegidas entre zonas protegidas.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# [!DNL Sandbox] guía de API de herramientas

La API de herramientas [!DNL Sandbox] proporciona varios extremos que le permiten exportar e importar instantáneas entre zonas protegidas disponibles para usted dentro de su organización. Todas las interacciones se producen a través de puntos de conexión HTTP. Antes de exportar una instantánea, se comprueba la zona protegida de origen en busca de artefactos, que son los objetos contenidos en un paquete. Cuando se realiza una solicitud de importación, se obtiene una instantánea de [!DNL Azure Blob] que se utiliza como plantilla para producir artefactos casi similares para la zona protegida de destino. Consulte la documentación de [herramientas de espacio aislado](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) para obtener una lista de los objetos y limitaciones admitidos.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de muestra y mucho más.

## Paquetes {#packages}

El extremo de paquetes de herramientas de zona protegida permite administrar paquetes. El paquete de herramientas de zona protegida es una colección de definiciones de artefactos que incluyen el ID del paquete, el nombre, la descripción, el ID de organización y el ID de creador. Consulte la [guía de extremo de paquetes](./packages.md) para obtener más información sobre cómo trabajar con paquetes en la API.

## Herramientas {#tools}

El extremo de las herramientas de la zona protegida le permite recuperar de forma independiente los datos JSON del trabajo. Consulte la [guía de extremo de herramientas](./tools.md) para obtener más información sobre la recuperación de datos JSON del trabajo en la API.

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas mediante la API de herramientas de zona protegida, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
