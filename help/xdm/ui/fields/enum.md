---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enumeración;campo
solution: Experience Platform
title: Definir campos de enumeración en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de enumeración en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Definir campos de enumeración en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo de enumeración representa un campo restringido a una lista predefinida de valores aceptables.

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede definirlo como un campo de enumeración seleccionando la casilla **[!UICONTROL Enum]** en el carril derecho.

![](../../images/ui/fields/special/enum.png)

Después de seleccionar la casilla de verificación, aparecen controles adicionales que permiten especificar las restricciones de valor de la enumeración. En la columna **[!UICONTROL Value]** debe proporcionar el valor exacto al que desea restringir el campo. Este valor debe cumplir con el [!UICONTROL Type] seleccionado para el campo de enumeración. Opcionalmente, también puede proporcionar una **[!UICONTROL Label]** compatible con el ser humano para la restricción.

Para agregar restricciones adicionales a la enumeración, seleccione **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Siga agregando las restricciones deseadas y las etiquetas opcionales a la enumeración. Cuando termine, seleccione **[!UICONTROL Apply]** para aplicar los cambios al esquema.

![](../../images/ui/fields/special/enum-configured.png)

El lienzo se actualiza para reflejar los cambios. Cuando explore este esquema en el futuro, puede ver y editar las restricciones del campo de enumeración dentro del carril derecho.

![](../../images/ui/fields/special/enum-applied.png)

## Pasos siguientes

Esta guía explica cómo definir un campo de enumeración en la interfaz de usuario. Consulte la descripción general sobre la [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
