---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;obligatorio;campo;
solution: Experience Platform
title: Definición de campos requeridos en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo XDM requerido en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Defina los campos obligatorios en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo obligatorio indica que debe proporcionarse un valor válido para que se acepte un registro o un evento de serie temporal concreto durante el consumo de datos. Los casos de uso comunes de los campos obligatorios incluyen información de identidad de usuario y marcas de tiempo.

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede definirlo como un campo obligatorio seleccionando la casilla **[!UICONTROL Required]** en el carril derecho. Seleccione **[!UICONTROL Apply]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/required.png)

Una vez aplicado el campo, su ruta aparece en **[!UICONTROL Required fields]** en el carril izquierdo. Si el campo está anidado, también aparecerán los campos principales según sea necesario.

![](../../images/ui/fields/special/required-applied.png)

## Pasos siguientes

Esta guía explica cómo definir un campo obligatorio en la interfaz de usuario. Consulte la descripción general sobre la [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
