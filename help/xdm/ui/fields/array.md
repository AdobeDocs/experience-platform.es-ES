---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;matriz;campo;
solution: Experience Platform
title: Definición de campos de matriz en la IU
description: Obtenga información sobre cómo definir un campo de matriz en la interfaz de usuario del Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definición de campos de matriz en la IU

Al definir un campo de Modelo de datos de experiencia (XDM) en la interfaz de usuario de Adobe Experience Platform, puede designar ese campo como una matriz.

El contenido de la matriz depende del [!UICONTROL Tipo] seleccionado para ese campo. Por ejemplo, si el [!UICONTROL Tipo] de un campo está establecido en &quot;[!UICONTROL Cadena]&quot;, al establecer ese campo como una matriz, se designará el campo como una matriz de cadenas. Si el [!UICONTROL Tipo] del campo está establecido en un tipo de datos de varios campos como &quot;[!UICONTROL Dirección postal]&quot;, se convertirá en una matriz de objetos de dirección postal que se ajusten al tipo de datos.

Una vez que haya [definido un nuevo campo en la interfaz de usuario](./overview.md#define), puede establecerlo como un campo de matriz al seleccionar la casilla de verificación **[!UICONTROL Matriz]** en el carril derecho.

![](../../images/ui/fields/special/array.png)

Una vez seleccionada la casilla de verificación, aparecen controles adicionales en el carril derecho que le permiten restringir aún más la matriz. Si no desea aplicar una restricción determinada, deje el campo en blanco.

Los controles de configuración adicionales para matrices son los siguientes:

| Propiedad de campo | Descripción |
| --- | --- |
| [!UICONTROL Longitud mínima] | El número mínimo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Longitud máxima] | El número máximo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Solo elementos únicos] | Si se establece en &quot;[!UICONTROL True]&quot;, cada elemento de la matriz debe ser único para que la ingesta se realice correctamente. |

{style="table-layout:auto"}

Una vez que haya terminado de configurar el campo, seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/array-config.png)

El lienzo se actualiza para reflejar los cambios realizados en el campo. Tenga en cuenta que el tipo de datos que se muestra junto al nombre del campo en el lienzo se anexa con un par de corchetes (`[]`), lo que indica que el campo representa una matriz de ese tipo de datos.

![](../../images/ui/fields/special/array-applied.png)

## Pasos siguientes

En esta guía se explica cómo definir un campo de matriz en la interfaz de usuario. Consulte la descripción general de [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
