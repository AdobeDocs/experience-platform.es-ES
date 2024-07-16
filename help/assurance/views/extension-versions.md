---
title: Vista de versiones de las extensiones
description: Esta guía detalla información sobre la vista Extensiones y las versiones en Adobe Experience Platform Assurance.
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%

---

# Vista Versión de extensiones

La vista Versión de extensiones le permite solicitar y ver rápidamente qué extensiones móviles de Adobe Experience Platform se han instalado y si están actualizadas en un cliente conectado a una sesión de Assurance.

## Introducción a la vista Versión de extensiones

Después de [configurar Assurance](../tutorials/implement-assurance.md), en la vista **Inicio**, seleccione **[!UICONTROL Versión de extensiones]**

![Versión de extensiones](./images/versions/versions-extension.png)

## Compruebe si su versión está actualizada

Dentro de esta vista, una tabla muestra la última versión de cada SDK móvil, así como la versión actual que haya instalado, si corresponde. Cuando una versión está sincronizada con la versión más reciente, la versión instalada muestra un distintivo verde. De lo contrario, el distintivo se muestra en rojo.

![Comparación de las versiones de extensiones](./images/versions/versions-extension-version.png)

## Exportar versiones

En la parte superior derecha de la vista, puede seleccionar **[!UICONTROL Exportar versiones]** que le proporciona una carga útil JSON con toda la información de las extensiones, así como la plataforma utilizada por el cliente. Puede elegir exportar estos datos a un archivo JSON o copiarlos en el portapapeles.

![Exportación de versiones de extensiones](./images/versions/versions-extension-export.png)
