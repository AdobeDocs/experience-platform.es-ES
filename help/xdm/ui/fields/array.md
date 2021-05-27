---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;matriz;campo
solution: Experience Platform
title: Definir campos de matriz en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de matriz en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# Definir campos de matriz en la interfaz de usuario

Al definir un campo Modelo de datos de experiencia (XDM) en la interfaz de usuario de Adobe Experience Platform, puede designar ese campo como una matriz.

El contenido de la matriz depende del [!UICONTROL Type] seleccionado para ese campo. Por ejemplo, si el valor [!UICONTROL Type] de un campo se define como &quot;[!UICONTROL String]&quot;, si se configura ese campo como una matriz, se designará el campo como una matriz de cadenas. Si el [!UICONTROL Type] del campo se configura en un tipo de datos de varios campos como &quot;[!UICONTROL Postal address]&quot;, se convertirá en una matriz de objetos de dirección postal que se ajusten al tipo de datos.

Una vez que haya [definido un nuevo campo en la interfaz de usuario](./overview.md#define), puede definirlo como un campo de matriz seleccionando la casilla **[!UICONTROL Array]** en el carril derecho.

![](../../images/ui/fields/special/array.png)

Una vez seleccionada la casilla de verificación, aparecen controles adicionales en el carril derecho que permiten restringir la matriz aún más. Si no desea aplicar una restricción determinada, deje el campo en blanco.

Los controles de configuración adicionales para matrices son los siguientes:

| Propiedad Field | Descripción |
| --- | --- |
| [!UICONTROL Longitud mínima] | El número mínimo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Longitud máxima] | El número máximo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Solo elementos únicos] | Si se configura como &quot;[!UICONTROL True]&quot;, cada elemento de la matriz debe ser único para que la ingesta se realice correctamente. |

{style=&quot;table-layout:auto&quot;}

Una vez que haya terminado de configurar el campo, seleccione **[!UICONTROL Apply]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/array-config.png)

El lienzo se actualiza para reflejar los cambios realizados en el campo. Tenga en cuenta que el tipo de datos que se muestra al lado del nombre del campo en el lienzo se anexa con un par de corchetes (`[]`), indicando que el campo representa una matriz de ese tipo de datos.

![](../../images/ui/fields/special/array-applied.png)

## Pasos siguientes

Esta guía explica cómo definir un campo de matriz en la interfaz de usuario. Consulte la descripción general sobre la [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
