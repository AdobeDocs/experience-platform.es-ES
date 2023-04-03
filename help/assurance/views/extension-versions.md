---
title: Vista de versiones de extensiones
description: Esta guía detalla información sobre la vista Versiones de extensiones en Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Vista de versiones de extensión

La vista Extensiones Versión permite ordenar y ver rápidamente qué extensiones móviles de Adobe Experience Platform ha instalado y si están actualizadas en un cliente conectado a una sesión de Garantía.

## Introducción a las vistas de versiones de extensión

Después [configuración de Assurance](../tutorials/implement-assurance.md), en el **Página principal** ver, seleccionar **[!UICONTROL Versiones de extensión]**

![Versiones de extensión](./images/versions/versions-extension.png)

## Compruebe si su versión está actualizada

Dentro de esta vista, una tabla muestra la última versión de cada SDK móvil, así como la versión actual que ha instalado, si corresponde. Cuando una versión está sincronizada con la versión más reciente, la versión instalada mostrará un distintivo verde. De lo contrario, el distintivo se mostrará en rojo.

![Comparación de versiones de extensión](./images/versions/versions-extension-version.png)

## Exportar versiones

En la parte superior derecha de la vista, puede seleccionar **[!UICONTROL Exportar versiones]** que le proporciona una carga útil JSON con toda la información de las extensiones, así como la plataforma utilizada por el cliente. Puede elegir exportar estos datos a un archivo JSON o copiarlos en el portapapeles.

![Exportación de versiones de extensión](./images/versions/versions-extension-export.png)
