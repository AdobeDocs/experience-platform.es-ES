---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
solution: Experience Platform
title: Definición de un campo obligatorio en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo XDM requerido en la interfaz de usuario del Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 48025fc11558bf6773ce5c48054483758c7e993f
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 1%

---


# Definición de un campo obligatorio en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo obligatorio indica que debe proporcionarse un valor válido para que se acepte un registro o evento de serie temporal concreto durante la ingestión de datos. Entre los casos de uso comunes de los campos obligatorios se incluyen la información de identidad del usuario y las marcas de hora.

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede configurarlo como un campo requerido seleccionando la casilla **[!UICONTROL Requerido]** en el carril derecho. Seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/required.png)

Una vez aplicado el campo, su ruta aparece en **[!UICONTROL Campos requeridos]** en el carril izquierdo. Si el campo está anidado, también aparecerán los campos principales según sea necesario.

![](../../images/ui/fields/special/required-applied.png)

## Pasos siguientes

En esta guía se explica cómo definir un campo obligatorio en la interfaz de usuario. Consulte la información general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para obtener información sobre cómo definir otros tipos de campos XDM en [!DNL Schema Editor].