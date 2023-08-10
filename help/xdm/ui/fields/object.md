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

Cuándo [definición de un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, utilice el **[!UICONTROL Tipo]** y seleccione &quot;[!UICONTROL Objeto]&quot; de la lista.

![](../../images/ui/fields/special/object.png)

Seleccionar **[!UICONTROL Aplicar]** para añadir el objeto al esquema. El lienzo se actualiza para mostrar el nuevo campo con [!UICONTROL Objeto] tipo de datos aplicado, incluidos los controles para editar y añadir subcampos al objeto.

![](../../images/ui/fields/special/object-applied.png)

Para añadir un subcampo, seleccione la **más (+)** junto al campo de objeto en el lienzo. Aparece un nuevo campo debajo del objeto, con controles para configurar el subcampo en el carril derecho.

![](../../images/ui/fields/special/object-add-field.png)

Una vez configurado el subcampo y seleccionado **[!UICONTROL Aplicar]** Sin embargo, puede seguir agregando campos al objeto mediante el mismo proceso. También puede añadir subcampos que sean objetos, lo que le permite anidar campos lo más profundamente posible.

Una vez que haya terminado de construir el objeto, es posible que desee reutilizar su estructura en diferentes clases y grupos de campos. En este caso, puede elegir convertir el objeto en un tipo de datos. Consulte la sección sobre [convertir objetos en tipos de datos](../resources/data-types.md#convert) en la guía de la interfaz de usuario sobre tipos de datos para obtener más información.

## Pasos siguientes

En esta guía se explica cómo definir un campo de objeto en la interfaz de usuario. Consulte la información general sobre [definición de campos en la IU](./overview.md#special) para aprender a definir otros tipos de campos XDM en la variable [!DNL Schema Editor].
