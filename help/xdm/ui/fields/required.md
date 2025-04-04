---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;obligatorio;campo;
title: Definición de campos obligatorios en la IU
description: Obtenga información sobre cómo definir un campo XDM requerido en la interfaz de usuario de Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definición de los campos obligatorios en la IU

En el modelo de datos de experiencia (XDM), un campo obligatorio indica que se debe proporcionar un valor válido para que se acepte un registro o evento de serie temporal determinado durante la ingesta de datos. Los casos de uso comunes de los campos obligatorios incluyen información de identidad del usuario y marcas de tiempo.

>[!IMPORTANT]
>
>Independientemente de si un campo de esquema es obligatorio o no, Experience Platform no acepta `null` o valores vacíos para ningún campo ingerido. Si no hay ningún valor para un campo en particular en un registro o evento, la clave de ese campo debe excluirse de la carga útil de ingesta.

Al [definir un nuevo campo](./overview.md#define) en la interfaz de usuario de Adobe Experience Platform, puede establecerlo como un campo obligatorio si selecciona la casilla de verificación **[!UICONTROL Obligatorio]** en el carril derecho. Seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![Casilla de verificación requerida](../../images/ui/fields/required/root.png)

Si el campo es un atributo de nivel raíz bajo el objeto de ID de inquilino, su ruta aparece inmediatamente bajo **[!UICONTROL Campos obligatorios]** en el carril izquierdo.

![Campo obligatorio de nivel raíz](../../images/ui/fields/required/applied.png)

Sin embargo, si un campo obligatorio está anidado en un objeto que no está marcado como obligatorio, el campo anidado no aparece en **[!UICONTROL Campos obligatorios]** en el carril izquierdo.

En el ejemplo siguiente, el campo `internalSKU` está establecido como obligatorio, pero su objeto principal `SKUs` no lo está. En este caso, no se producirían errores de validación si `SKUs` se excluye al ingerir datos, aunque el campo secundario `internalSKU` esté marcado como obligatorio. En otras palabras, mientras que `SKUs` es opcional, debe contener un campo `internalSKU` en el evento de que se incluya.

![Campo obligatorio anidado](../../images/ui/fields/required/nested.png)

Si desea que un campo anidado siempre sea obligatorio en un esquema, también debe establecer todos los campos principales como obligatorios (con la excepción del objeto de ID de inquilino).

![Campos obligatorios para principal y secundario](../../images/ui/fields/required/parent-and-child.png)

## Pasos siguientes

En esta guía se explica cómo definir un campo obligatorio en la interfaz de usuario. Consulte la descripción general de [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
