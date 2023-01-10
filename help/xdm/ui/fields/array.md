---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;matriz;campo
solution: Experience Platform
title: Definir campos de matriz en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de matriz en la interfaz de usuario del Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# Definir campos de matriz en la interfaz de usuario

Al definir un campo Modelo de datos de experiencia (XDM) en la interfaz de usuario de Adobe Experience Platform, puede designar ese campo como una matriz.

El contenido de la matriz depende del [!UICONTROL Tipo] seleccionado para ese campo. Por ejemplo, si un campo [!UICONTROL Tipo] se configura como &quot;[!UICONTROL Cadena]&quot;, si se establece ese campo como una matriz, el campo se designará como una matriz de cadenas. Si el campo [!UICONTROL Tipo] se establece en un tipo de datos de varios campos como &quot;[!UICONTROL Dirección postal]&quot;, entonces se convertiría en una matriz de objetos de dirección postal que se ajustan al tipo de datos.

Después de [se ha definido un nuevo campo en la interfaz de usuario](./overview.md#define), puede definirlo como un campo de matriz seleccionando la variable **[!UICONTROL Matriz]** en el carril derecho.

![](../../images/ui/fields/special/array.png)

Una vez seleccionada la casilla de verificación, aparecen controles adicionales en el carril derecho que permiten restringir la matriz aún más. Si no desea aplicar una restricción determinada, deje el campo en blanco.

Los controles de configuración adicionales para matrices son los siguientes:

| Propiedad Field | Descripción |
| --- | --- |
| [!UICONTROL Longitud mínima] | El número mínimo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Longitud máxima] | El número máximo de elementos que debe contener la matriz para que la ingesta se realice correctamente. |
| [!UICONTROL Solo elementos únicos] | Si se configura como &quot;[!UICONTROL True]&quot;, cada elemento de la matriz debe ser único para que la ingesta se realice correctamente. |

{style=&quot;table-layout:auto&quot;}

Una vez que haya terminado de configurar el campo, seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/array-config.png)

El lienzo se actualiza para reflejar los cambios realizados en el campo. Tenga en cuenta que el tipo de datos que se muestra al lado del nombre del campo en el lienzo se anexa con un par de corchetes (`[]`), indicando que el campo representa una matriz de ese tipo de datos.

![](../../images/ui/fields/special/array-applied.png)

## Pasos siguientes

Esta guía explica cómo definir un campo de matriz en la interfaz de usuario. Consulte la descripción general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en la [!DNL Schema Editor].
