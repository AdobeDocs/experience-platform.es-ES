---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;objeto;campo;
solution: Experience Platform
title: Definición de campos de objeto en la IU
description: Obtenga información sobre cómo definir un campo de tipo de objeto en la interfaz de usuario del Experience Platform.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Definición de campos de objeto en la IU

Adobe Experience Platform permite personalizar completamente la estructura de las clases personalizadas del modelo de datos de experiencia (XDM), los grupos de campos de esquema y los tipos de datos. Para organizar y anidar campos relacionados en recursos XDM personalizados, puede definir campos de tipo objeto que pueden contener subcampos adicionales.

Cuando [defina un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, utilice la lista desplegable **[!UICONTROL Tipo]** y seleccione &quot;[!UICONTROL Objeto]&quot; de la lista.

![](../../images/ui/fields/special/object.png)

Seleccione **[!UICONTROL Aplicar]** para agregar el objeto al esquema. El lienzo se actualiza para mostrar el nuevo campo con el tipo de datos [!UICONTROL Object] aplicado, incluidos los controles para editar y agregar subcampos al objeto.

![](../../images/ui/fields/special/object-applied.png)

Para agregar un subcampo, seleccione el icono **más (+)** junto al campo de objeto en el lienzo. Aparece un nuevo campo debajo del objeto, con controles para configurar el subcampo en el carril derecho.

![](../../images/ui/fields/special/object-add-field.png)

Una vez que haya configurado el subcampo y haya seleccionado **[!UICONTROL Aplicar]**, puede seguir agregando campos al objeto mediante el mismo proceso. También puede añadir subcampos que sean objetos, lo que le permite anidar campos lo más profundamente posible.

Una vez que haya terminado de construir el objeto, es posible que desee reutilizar su estructura en diferentes clases y grupos de campos. En este caso, puede elegir convertir el objeto en un tipo de datos. Consulte la sección sobre [conversión de objetos a tipos de datos](../resources/data-types.md#convert) en la guía de la interfaz de usuario de tipos de datos para obtener más información.

## Pasos siguientes

En esta guía se explica cómo definir un campo de objeto en la interfaz de usuario. Consulte la descripción general de [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
