---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;objeto;campo;
solution: Experience Platform
title: Definición de campos de objeto en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de tipo de objeto en la interfaz de usuario del Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Definición de campos de objeto en la interfaz de usuario

Adobe Experience Platform permite personalizar completamente la estructura de las clases, mezclas y tipos de datos personalizados del Modelo de datos de experiencia (XDM). Para organizar y anidar campos relacionados en recursos XDM personalizados, puede definir campos de tipo de objeto que pueden contener subcampos adicionales.

Cuando [defina un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, utilice la lista desplegable **[!UICONTROL Tipo]** y seleccione &quot;[!UICONTROL Objeto]&quot; en la lista.

![](../../images/ui/fields/special/object.png)

Seleccione **[!UICONTROL Aplicar]** para agregar el objeto al esquema. El lienzo se actualiza para mostrar el nuevo campo con el tipo de datos [!UICONTROL Object] aplicado, incluidos los controles para editar y agregar subcampos al objeto.

![](../../images/ui/fields/special/object-applied.png)

Para agregar un subcampo, seleccione el icono **más (+)** junto al campo de objeto en el lienzo. Aparece un nuevo campo debajo del objeto, con controles para configurar el subcampo en el carril derecho.

![](../../images/ui/fields/special/object-add-field.png)

Una vez configurado el subcampo y seleccionado **[!UICONTROL Aplicar]**, puede continuar agregando campos al objeto mediante el mismo proceso. También puede agregar subcampos que sean objetos en sí mismos, lo que le permite anidar los campos tan profundamente como desee.

![](../../images/ui/fields/special/object-nested.png)

Una vez que haya terminado de construir el objeto, es posible que desee reutilizar su estructura en diferentes clases y mezclas. En este caso, puede elegir convertir el objeto en un tipo de datos. Consulte la sección sobre [conversión de objetos a tipos de datos](../resources/data-types.md#convert) en la guía UI de tipos de datos para obtener más información.

## Pasos siguientes

En esta guía se explica cómo definir un campo de objeto en la interfaz de usuario. Consulte la información general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para obtener información sobre cómo definir otros tipos de campos XDM en [!DNL Schema Editor].
