---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enumeración;campo;
solution: Experience Platform
title: Definición de un campo de enumeración en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de enumeración en la interfaz de usuario del Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Definición de un campo de enumeración en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo enumeración representa un campo restringido a una lista predefinida de valores aceptables.

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede definirlo como un campo enumeración seleccionando la casilla **[!UICONTROL Enum]** en el carril derecho.

![](../../images/ui/fields/special/enum.png)

Después de seleccionar la casilla de verificación, aparecen controles adicionales que permiten especificar las restricciones de valor de la enumeración. En la columna **[!UICONTROL Valor]**, debe proporcionar el valor exacto al que desee restringir el campo. Este valor debe cumplir con el [!UICONTROL Tipo] seleccionado para el campo enumeración. Opcionalmente, también puede proporcionar una **[!UICONTROL etiqueta]** descriptiva para la restricción.

Para agregar restricciones adicionales a la enumeración, seleccione **[!UICONTROL Añadir fila]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continúe agregando las restricciones y etiquetas opcionales deseadas a la enumeración. Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![](../../images/ui/fields/special/enum-configured.png)

El lienzo se actualiza para reflejar los cambios. Al explorar este esquema en el futuro, puede realizar vistas y editar las restricciones del campo de enumeración dentro del carril derecho.

![](../../images/ui/fields/special/enum-applied.png)

## Pasos siguientes

En esta guía se explica cómo definir un campo de enumeración en la interfaz de usuario. Consulte la información general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para obtener información sobre cómo definir otros tipos de campos XDM en [!DNL Schema Editor].