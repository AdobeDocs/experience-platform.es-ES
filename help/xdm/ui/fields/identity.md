---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;workspace;identity;field;
solution: Experience Platform
title: Definición de campos de identidad en la IU
description: Obtenga información sobre cómo definir un campo de identidad en la interfaz de usuario del Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 6%

---

# Definición de campos de identidad en la IU

En el Modelo de datos de experiencia (XDM), un campo de identidad representa un campo que se puede utilizar para identificar a una persona individual relacionada con un registro o un evento de serie temporal. Este documento explica cómo definir un campo de identidad en la interfaz de usuario de Adobe Experience Platform.

## Requisitos previos

Los campos de identidad son un componente crucial en la forma en que se construyen los gráficos de identidad de los clientes en Platform, lo que en última instancia afecta a la forma en que el Perfil del cliente en tiempo real combina fragmentos de datos dispares para obtener una vista completa del cliente. Antes de definir los campos de identidad en los esquemas, consulte la siguiente documentación para obtener más información sobre los servicios y conceptos clave relacionados con los campos de identidad:

* [Servicio de identidad de Adobe Experience Platform](../../../identity-service/home.md): vincula identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
   * [Áreas de nombres de identidad](../../../identity-service/namespaces.md): las áreas de nombres de identidad definen los diferentes tipos de información de identidad que pueden relacionarse con una sola persona y son un componente requerido para cada campo de identidad.
* [Perfil del cliente en tiempo real](../../../profile/home.md): aprovecha los gráficos de identidad de los clientes para proporcionar un perfil de consumidor unificado en función de los datos agregados de varias fuentes, actualizados en tiempo casi real.

## Definición de un campo de identidad {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restricciones a la identidad principal"
>abstract="Este esquema utiliza un grupo de campos destinado a utilizarse en una conexión de origen específica. La conexión requiere que identityMap se utilice como identidad principal y la ha establecido automáticamente."

Cuándo [definición de un nuevo campo](./overview.md#define) en la interfaz de usuario de, puede establecerla como un campo de identidad seleccionando la variable **[!UICONTROL Identidad]** en el carril derecho.

![](../../images/ui/fields/special/identity.png)

Aparecerán controles adicionales después de seleccionar la casilla de verificación. Si desea que este campo sea la identidad principal del esquema, seleccione la **[!UICONTROL Identidad principal]** casilla de verificación

>[!NOTE]
>
>Un solo esquema puede tener muchos campos de identidad definidos, pero solo puede tener una identidad principal. Todos los campos de identidad (principales o de otro tipo) contribuyen al gráfico de identidad de un cliente individual, pero el Perfil del cliente en tiempo real solo utiliza la identidad principal como fuente fiable al combinar fragmentos de datos. Si desea habilitar un esquema para utilizarlo en el perfil, el esquema debe tener definida una identidad principal.

En **[!UICONTROL Área de nombres de identidad]**, utilice el menú desplegable para seleccionar el área de nombres adecuada para el campo de identidad. Se muestran las áreas de nombres estándar proporcionadas por Adobe, junto con cualquier área de nombres personalizada definida por su organización.

Cuando termine, seleccione **[!UICONTROL Aplicar]** para aplicar el cambio al esquema.

![](../../images/ui/fields/special/identity-config.png)

El lienzo se actualiza para reflejar los cambios, y el campo seleccionado obtiene un símbolo de huella digital (![](../../images/ui/fields/special/identity-symbol.png)) para designarla como identidad. En el carril izquierdo, el campo de identidad ahora aparece bajo el nombre de la clase o grupo de campos de esquema que proporciona el campo al esquema.

Si el campo también se estableció como identidad principal, también se enumerará en **[!UICONTROL Campos obligatorios]** en el carril izquierdo. Si el campo de identidad está anidado en la estructura de esquema, todos los campos principales también se enumerarán como obligatorios.

![](../../images/ui/fields/special/identity-applied.png)

Si ha definido una identidad principal para el esquema, ahora puede continuar con [habilitar el esquema para utilizarlo en el perfil del cliente en tiempo real](../resources/schemas.md#profile).

## Pasos siguientes

En esta guía se explica cómo definir un campo de identidad en la interfaz de usuario. A medida que los datos se incorporan mediante este esquema, los gráficos de identidad de los clientes se actualizarán para reflejar los campos de identidad del esquema. Consulte la guía en la [visor de gráficos de identidad](../../../identity-service/ui/identity-graph-viewer.md) para aprender a explorar el gráfico privado de su organización en la interfaz de usuario.

Consulte la información general sobre [definición de campos en la IU](./overview.md#special) para aprender a definir otros tipos de campos XDM en la variable [!DNL Schema Editor].
