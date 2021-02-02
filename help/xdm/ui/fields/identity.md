---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;identidad;campo;
solution: Experience Platform
title: Definición de un campo de identidad en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de identidad en la interfaz de usuario del Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f5f507c2e962e2ff9f81376bfe363a6f438056cd
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Definición de un campo de identidad en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un campo de identidad representa un campo que puede utilizarse para identificar a una persona individual relacionada con un registro o evento de series temporales. Este documento explica cómo definir un campo de identidad en la interfaz de usuario de Adobe Experience Platform.

## Requisitos previos

Los campos de identidad son un componente crucial de la forma en que se construyen los gráficos de identidad del cliente en Platform, lo que en última instancia afecta a la forma en que el Perfil del cliente en tiempo real combina distintos fragmentos de datos para obtener una vista completa del cliente. Antes de definir los campos de identidad en los esquemas, consulte la siguiente documentación para conocer los servicios y conceptos clave relacionados con los campos de identidad:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Permite unir identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
   * [Áreas de nombres](../../../identity-service/namespaces.md) de identidad: Las Áreas de nombres de identidad definen los distintos tipos de información de identidad que pueden relacionarse con una sola persona y que son un componente requerido para cada campo de identidad.
* [Perfil](../../../profile/home.md) del cliente en tiempo real: Aprovecha los gráficos de identidad del cliente para proporcionar un perfil de cliente unificado basado en datos agregados de múltiples fuentes, actualizados en tiempo casi real.

## Definir un campo de identidad

Cuando [define un nuevo campo](./overview.md#define) en la interfaz de usuario, puede definirlo como un campo de identidad seleccionando la casilla **[!UICONTROL Identidad]** en el carril derecho.

![](../../images/ui/fields/special/identity.png)

Después de seleccionar la casilla de verificación, aparecen controles adicionales. Si desea que este campo sea la identidad principal del esquema, seleccione la casilla **[!UICONTROL Identidad principal]**.

>[!NOTE]
>
>Un solo esquema puede tener muchos campos de identidad definidos, pero solo puede tener una identidad principal. Todos los campos de identidad (principales o de otro tipo) contribuyen al gráfico de identidad de un cliente individual, pero el Perfil del cliente en tiempo real solo utiliza la identidad principal como fuente de verdad al combinar fragmentos de datos. Si desea habilitar un esquema para utilizarlo en Perfil, el esquema debe tener una identidad principal definida.

En **[!UICONTROL Área de nombres de identidad]**, utilice el menú desplegable para seleccionar la Área de nombres adecuada para el campo de identidad. Se muestran las Áreas de nombres estándar proporcionadas por Adobe, junto con las Áreas de nombres personalizadas definidas por su organización.

Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/identity-config.png)

El lienzo se actualiza para reflejar los cambios y el campo seleccionado obtiene un símbolo de huella (![](../../images/ui/fields/special/identity-symbol.png)) para designarlo como identidad. En el carril izquierdo, el campo de identidad aparece ahora bajo el nombre de la clase o la mezcla que proporciona el campo al esquema.

Dado que todos los campos de identidad son obligatorios de forma predeterminada, el campo ahora aparece en **[!UICONTROL Campos requeridos]** en el carril izquierdo. Si el campo de identidad está anidado dentro de la estructura de esquema, también se enumerarán todos los campos principales según sea necesario.

![](../../images/ui/fields/special/identity-applied.png)

Si ha definido una identidad principal para el esquema, ahora puede [habilitar el esquema para utilizarlo en el Perfil del cliente en tiempo real](../resources/schemas.md#profile).

## Pasos siguientes

En esta guía se explica cómo definir un campo de identidad en la interfaz de usuario. A medida que los datos se ingieren mediante este esquema, los gráficos de identidad del cliente se actualizarán para reflejar los campos de identidad del esquema. Consulte la guía del [visor de gráficos de identidad](../../../identity-service/ui/identity-graph-viewer.md) para obtener información sobre cómo explorar el gráfico privado de su organización en la interfaz de usuario.

Consulte la información general sobre [definición de campos en la interfaz de usuario](./overview.md#special) para obtener información sobre cómo definir otros tipos de campos XDM en [!DNL Schema Editor].