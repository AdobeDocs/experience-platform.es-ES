---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;identidad;campo
solution: Experience Platform
title: Definición de campos de identidad en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de identidad en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Definición de campos de identidad en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo de identidad representa un campo que puede utilizarse para identificar a una persona individual relacionada con un registro o un evento de serie temporal. Este documento explica cómo definir un campo de identidad en la interfaz de usuario de Adobe Experience Platform.

## Requisitos previos

Los campos de identidad son un componente crucial de la forma en que se construyen los gráficos de identidad de los clientes en Platform, que en última instancia afecta a cómo el perfil del cliente en tiempo real combina distintos fragmentos de datos para obtener una vista completa del cliente. Antes de definir los campos de identidad en los esquemas, consulte la siguiente documentación para conocer los servicios clave y los conceptos relacionados con los campos de identidad:

* [Servicio de identidad de Adobe Experience Platform](../../../identity-service/home.md): Agrupa identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
   * [Espacios de nombres](../../../identity-service/namespaces.md) de identidad: Las áreas de nombres de identidad definen los diferentes tipos de información de identidad que puede relacionarse con una sola persona y que son un componente requerido para cada campo de identidad.
* [Perfil](../../../profile/home.md) del cliente en tiempo real: Utiliza los gráficos de identidad de los clientes para proporcionar un perfil de cliente unificado basado en datos agregados de varias fuentes, actualizados en tiempo casi real.

## Definir un campo de identidad

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario, puede definirlo como un campo de identidad seleccionando la casilla **[!UICONTROL Identity]** en el carril derecho.

![](../../images/ui/fields/special/identity.png)

Después de seleccionar la casilla de verificación, aparecen controles adicionales. Si desea que este campo sea la identidad principal para el esquema, active la casilla de verificación **[!UICONTROL Primary identity]**.

>[!NOTE]
>
>Un esquema único puede tener muchos campos de identidad definidos, pero solo puede tener una identidad principal. Todos los campos de identidad (principales o de otro tipo) contribuyen al gráfico de identidad de un cliente individual, pero Perfil del cliente en tiempo real solo utiliza la identidad principal como fuente de verdad al combinar fragmentos de datos. Si desea habilitar un esquema para utilizarlo en Perfil, el esquema debe tener una identidad principal definida.

En **[!UICONTROL Identity namespace]**, utilice el menú desplegable para seleccionar el área de nombres adecuada para el campo de identidad. Se muestran las áreas de nombres estándar proporcionadas por Adobe, junto con las áreas de nombres personalizadas definidas por su organización.

Cuando termine, seleccione **[!UICONTROL Apply]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/identity-config.png)

El lienzo se actualiza para reflejar los cambios, con el campo seleccionado obteniendo un símbolo de huella (![](../../images/ui/fields/special/identity-symbol.png)) para designarlo como identidad. En el carril izquierdo, el campo de identidad se muestra ahora bajo el nombre del grupo de campos de clase o esquema que proporciona el campo al esquema.

Dado que todos los campos de identidad son obligatorios de forma predeterminada, el campo aparece ahora bajo **[!UICONTROL Required fields]** en el carril izquierdo. Si el campo de identidad está anidado dentro de la estructura del esquema, todos los campos principales también se enumerarán como necesarios.

![](../../images/ui/fields/special/identity-applied.png)

Si ha definido una identidad principal para el esquema, ahora puede [habilitar el esquema para utilizarlo en el perfil del cliente en tiempo real](../resources/schemas.md#profile).

## Pasos siguientes

Esta guía explica cómo definir un campo de identidad en la interfaz de usuario. A medida que los datos se incorporen mediante este esquema, los gráficos de identidad del cliente se actualizarán para reflejar los campos de identidad del esquema. Consulte la guía del [visor de gráficos de identidad](../../../identity-service/ui/identity-graph-viewer.md) para aprender a explorar el gráfico privado de su organización en la interfaz de usuario.

Consulte la descripción general sobre la [definición de campos en la interfaz de usuario](./overview.md#special) para aprender a definir otros tipos de campos XDM en [!DNL Schema Editor].
