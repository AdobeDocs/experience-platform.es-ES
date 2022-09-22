---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;enumeración;campo
solution: Experience Platform
title: Definir campos de enumeración en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de enumeración en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 878d99d9eb45f40ff76e5e90116abf032be1c93f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# Definir campos de enumeración en la interfaz de usuario {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="enumeraciones y valores sugeridos"
>abstract="Una enumeración restringe un campo de cadena para permitir solo la ingesta de datos que coincidan con un conjunto predefinido de valores. También puede definir un conjunto de valores sugeridos para el campo que no restrinjan la ingesta, sino que definan los atributos que puede elegir en la segmentación. Consulte la Documentación para obtener más información."

En el Modelo de datos de experiencia (XDM), un campo de enumeración representa un campo restringido a una lista predefinida de valores aceptables.

When [definición de un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede definirlo como un campo de enumeración seleccionando la **[!UICONTROL Enum]** en el carril derecho.

![](../../images/ui/fields/special/enum.png)

Después de seleccionar la casilla de verificación, aparecen controles adicionales que permiten especificar las restricciones de valor de la enumeración. En el **[!UICONTROL Valor]** , debe proporcionar el valor exacto al que desea restringir el campo. Este valor debe cumplir con la [!UICONTROL Tipo] ha seleccionado para el campo enumeración . Opcionalmente, puede proporcionar un **[!UICONTROL Etiqueta]** también para la restricción.

Para añadir restricciones adicionales a la enumeración, seleccione **[!UICONTROL Añadir fila]**.

![](../../images/ui/fields/special/enum-add-row.png)

Siga agregando las restricciones deseadas y las etiquetas opcionales a la enumeración. Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar los cambios al esquema.

![](../../images/ui/fields/special/enum-configured.png)

El lienzo se actualiza para reflejar los cambios. Cuando explore este esquema en el futuro, puede ver y editar las restricciones del campo de enumeración dentro del carril derecho.

![](../../images/ui/fields/special/enum-applied.png)

## Pasos siguientes

Esta guía explica cómo definir un campo de enumeración en la interfaz de usuario. Consulte la descripción general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en la [!DNL Schema Editor].
