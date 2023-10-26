---
title: Guía de API de Sandbox Tools
description: La función Herramientas para zonas protegidas de Adobe Experience Platform permite exportar e importar una instantánea de las configuraciones de las zonas protegidas entre zonas protegidas.
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# [!DNL Sandbox] Guía de API de herramientas

El [!DNL Sandbox] La API de herramientas proporciona varios extremos que le permiten exportar e importar instantáneas entre entornos limitados disponibles en su organización. Todas las interacciones se producen a través de puntos de conexión HTTP. Antes de exportar una instantánea, se comprueba la zona protegida de origen en busca de artefactos, que son los objetos contenidos en un paquete. Cuando se realiza una solicitud de importación, una [!DNL Azure Blob] la instantánea se obtiene y utiliza como plantilla para producir artefactos casi similares para la zona protegida de destino. Consulte la [herramientas de zona protegida](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) para obtener una lista de los objetos compatibles y las limitaciones.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

## Paquetes {#packages}

El extremo de paquetes de herramientas de zona protegida permite administrar paquetes. El paquete de herramientas de zona protegida es una colección de definiciones de artefactos que incluyen el ID del paquete, el nombre, la descripción, el ID de organización y el ID de creador. Consulte la [guía de extremo de paquetes](./packages.md) para obtener más información sobre cómo trabajar con paquetes en la API.

## Herramientas {#tools}

El extremo de las herramientas de la zona protegida le permite recuperar de forma independiente los datos JSON del trabajo. Consulte la [guía de extremo de herramientas](./tools.md) para obtener más información sobre la recuperación de datos JSON del trabajo en la API.

## Pasos siguientes {#next-steps}

Para empezar a realizar llamadas mediante la API de herramientas de entorno limitado, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
