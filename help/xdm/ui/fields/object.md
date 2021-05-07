---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;objeto;campo
solution: Experience Platform
title: Definir campos de objeto en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de tipo de objeto en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Definir campos de objeto en la interfaz de usuario

Adobe Experience Platform le permite personalizar completamente la estructura de las clases, los grupos de campos de esquema y los tipos de datos personalizados del Modelo de datos de experiencia (XDM). Para organizar y anidar campos relacionados en recursos XDM personalizados, puede definir campos de tipo objeto que pueden contener subcampos adicionales.

Cuando [defina un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, utilice la lista desplegable **[!UICONTROL Type]** y seleccione &quot;[!UICONTROL Object]&quot; en la lista.

![](../../images/ui/fields/special/object.png)

Seleccione **[!UICONTROL Apply]** para añadir el objeto al esquema. El lienzo se actualiza para mostrar el nuevo campo con el tipo de datos [!UICONTROL Object] aplicado, incluidos los controles para editar y agregar subcampos al objeto.

![](../../images/ui/fields/special/object-applied.png)

Para añadir un subcampo, seleccione el icono **plus (+)** situado junto al campo de objeto en el lienzo. Aparece un nuevo campo debajo del objeto, con controles para configurar el subcampo en el carril derecho.

![](../../images/ui/fields/special/object-add-field.png)

Una vez configurado el subcampo y seleccionado **[!UICONTROL Apply]**, puede continuar agregando campos al objeto con el mismo proceso. También puede añadir subcampos que sean objetos en sí, lo que le permite anidar campos tan profundamente como desee.

![](../../images/ui/fields/special/object-nested.png)

Cuando haya terminado de construir el objeto, es posible que desee reutilizar su estructura en diferentes clases y grupos de campos. En este caso, puede elegir convertir el objeto en un tipo de datos. Consulte la sección sobre [conversión de objetos a tipos de datos](../resources/data-types.md#convert) en la guía de interfaz de usuario de tipos de datos para obtener más información.

## Pasos siguientes

Esta guía explica cómo definir un campo de objeto en la interfaz de usuario. Consulte la descripción general sobre la [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
