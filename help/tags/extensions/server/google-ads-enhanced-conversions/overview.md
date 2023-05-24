---
title: Extensión de conversiones mejoradas de Google Ads
description: Obtenga información acerca de la extensión de conversiones mejoradas de Google Ads para el reenvío de eventos en Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] Extensión de conversiones mejoradas

Uso del [!DNL Google Ads] API, puede aprovechar [conversiones mejoradas](https://support.google.com/google-ads/answer/9888656) enviando datos de clientes de origen en forma de ajustes de conversión. Google utiliza estos datos adicionales para mejorar los informes de las conversiones en línea impulsadas por las interacciones publicitarias.

El [[!DNL Google Ads] Extensión de reenvío de eventos de conversiones mejoradas](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (antes denominado &quot;el [!DNL Enhanced Conversions] extensión) proporciona una plantilla fácil de usar para implementar fácilmente conversiones mejoradas para [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Las conversiones mejoradas solo funcionan para tipos de conversión en los que hay datos de clientes presentes, como suscripciones, suscripciones y compras. Uno o más de los siguientes datos de clientes deben estar disponibles, ya que son necesarios cuando [configuración de una acción de conversión](#conversion-action-event-forwarding) para una regla de reenvío de eventos:
>
>* Correo electrónico (preferido)
>* Nombre y dirección postal (dirección postal, ciudad, estado/región y código postal)
>* Número de teléfono (debe proporcionarse además de uno de los otros dos datos anteriores)


## Información general sobre la implementación

Las conversiones mejoradas aprovechan las [!DNL Google Ads] API para añadir datos de origen a una conversión que se produjo en un dispositivo cliente, normalmente un sitio web. Esto significa que hay dos pasos para implementar conversiones mejoradas:

1. Envíe una conversión desde el cliente.
1. Utilice el reenvío de eventos para enviar datos de origen adicionales que mejoren los datos de conversión enviados desde el cliente.

>[!TIP]
>
>Para asociar el evento de conversión del lado del cliente con los datos de origen enviados desde el reenvío de eventos, la variable `transaction_ID` debe ser el mismo en ambas llamadas. Para obtener más información sobre dónde se debe proporcionar este valor para cada servicio, consulte las secciones sobre configuración de acciones de conversión para [etiquetas](#conversion-action-tags) y [reenvío de eventos](#conversion-action-event-forwarding), respectivamente.

Dado que el envío de eventos de conversión implica una implementación del lado del cliente y del lado del servidor, este documento cubre los pasos previos para configurar el lado del cliente [[!DNL Google Global Site Tag] Extensión (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) además de las [!DNL Enhanced Conversions] extensión para el reenvío de eventos.

El siguiente vídeo ofrece una introducción a la [!DNL Enhanced Conversions] extensión de y recorre los pasos de implementación en un nivel superior:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Envío de una conversión mediante etiquetas

Para enviar un evento de conversión desde en un sitio web, [!DNL Google Global Site Tag] (gtag) debe implementarse. Puede conseguirlo utilizando etiquetas configurando e instalando el [!DNL Google Global Site Tag] Extensión de (gtag).

### Configurar e instalar el [!DNL Google Global Site Tag] extensión

Vaya a [!UICONTROL Recopilación de datos] IU o IU del Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Seleccione la propiedad de etiqueta en la que desea instalar la extensión y, a continuación, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , busque la pestaña [!UICONTROL Etiqueta de sitio global de Google (gtag)] extensión y seleccione **[!UICONTROL Instalar]**.

![El [!UICONTROL Etiqueta de sitio global de Google (gtag)] extensión seleccionada en la sección [!UICONTROL Extensiones] ver en la [!UICONTROL Recopilación de datos] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Aparecerá el cuadro de diálogo de instalación. Desde aquí, seleccione **[!UICONTROL Agregar cuenta]** y proporcione los siguientes valores cuando se le solicite:

| Propiedad de cuenta | Descripción |
| --- | --- |
| Nombre de cuenta | Un nombre único para la cuenta. Este nombre solo se utiliza en la interfaz de usuario de etiquetas. |
| ID de cuenta | Su [!DNL Google Ads] ID de cuenta. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y vaya a: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La cadena del ID de cuenta se puede encontrar en la ventana del fragmento de código que comienza con `AW-` o `d`. |
| Producto | Seleccionar **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Agregar cuenta]**, luego seleccione **[!UICONTROL Guardar]**.

### Agregar una acción de conversión de envío {#conversion-action-tags}

Después de instalar la extensión, puede empezar a incluir acciones de conversión en las reglas de etiquetas. Al crear o editar una regla que escucha la conversión que desea mejorar, seleccione **[!UICONTROL Añadir]** bajo [!UICONTROL Acciones]. En el siguiente cuadro de diálogo, seleccione **[!UICONTROL Etiqueta de sitio global de Google (gtag)]** desde el [!UICONTROL Extensión] y, a continuación, seleccione **[!UICONTROL Enviar un evento]** bajo [!UICONTROL Tipo de acción].

![El [!UICONTROL Enviar un evento] tipo de acción seleccionado en la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Aparecen controles adicionales que le permiten configurar el [!DNL gtag] evento. Como mínimo, se deben rellenar los campos siguientes:

1. **[!UICONTROL Nombre del evento (acción)]**: Entrar `conversion` como el valor.
1. Añada un nuevo campo donde la clave sea `transaction_id` y el valor es un [elemento de datos](../../../ui/managing-resources/data-elements.md) que contiene el [ID de transacción](https://support.google.com/google-ads/answer/6386790) valor.
1. **[!UICONTROL Etiqueta de conversión]**: Introduzca la etiqueta de conversión adecuada desde el [!DNL Google Ads] cuenta. Para encontrar este valor, inicie sesión en Google Ads y navegue hasta **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. La etiqueta de conversión se encuentra en [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Mientras se encuentra en el área de configuración de etiquetas de su [!DNL Google Ads] , asegúrese de que la opción conversiones mejoradas está activada. Para ello, revise y acepte los Términos de servicio y, a continuación, seleccione **[!DNL Turn on enhanced conversions]** y **[!DNL API]** como método de implementación.

Una vez configurada la acción, seleccione **[!UICONTROL Conservar cambios]** para añadir la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo [generar](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Envío de datos de origen mediante el reenvío de eventos

Una vez que pueda enviar eventos de conversión desde el lado del cliente, puede mejorar estas conversiones mediante el [!DNL Enhanced Conversions] extensión de reenvío de eventos.

### Crear un secreto y un elemento de datos de Google OAuth 2 {#create-secret-data-element}

Antes de configurar la extensión, debe crear un token de acceso en el reenvío de eventos para autenticarse en [!DNL Google Ads] API.

Consulte la guía de [crear secretos de reenvío de eventos](../../../ui/event-forwarding/secrets.md) para ver los pasos detallados. Asegúrese de seleccionar **[!UICONTROL Google OAuth 2]** como el tipo secreto. Siga las indicaciones y, cuando se le pida que seleccione un perfil de cuenta de Google, seleccione la cuenta que tenga acceso a la acción de conversión que está configurando.

Una vez creado el secreto, [crear un nuevo elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) y seleccione **[!UICONTROL Secreto]** para el tipo de elemento de datos. Seleccione el secreto de Google OAuth 2 apropiado para cada entorno y seleccione **[!UICONTROL Guardar en biblioteca]**.

### Configurar e instalar el [!DNL Enhanced Conversions] extensión {#install-enhanced-conversions}

Busque el [!UICONTROL Conversiones mejoradas de Google Ads] en el catálogo del reenvío de eventos y seleccione **[!UICONTROL Instalar]**.

![El [!UICONTROL Conversiones mejoradas de Google Ads] extensión seleccionada en la sección [!UICONTROL Extensiones] ver en la [!UICONTROL Recopilación de datos] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar la extensión, debe rellenar los dos campos obligatorios:

1. **[!UICONTROL ID de cliente]**: ID que identifica de forma exclusiva su [!DNL Google Ads] cuenta. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y vaya a **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento de datos de token de acceso]**: seleccione el icono de elemento de datos (![Icono de elemento de datos](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) y elija el elemento de datos secretos OAuth 2 de Google que desee [configurado en el paso anterior](#create-secret-data-element) en el menú.

Cuando termine, seleccione **[!UICONTROL Guardar]** para instalar la extensión de.

### Añadir un [!UICONTROL Enviar conversión] acción a una regla {#conversion-action-event-forwarding}

Una vez instalada la extensión de, puede empezar a incluir [!UICONTROL Enviar conversión] acciones en las reglas de reenvío de eventos. Al crear o editar una regla que escucha la conversión que desea mejorar, seleccione **[!UICONTROL Añadir]** bajo [!UICONTROL Acciones]. En el siguiente cuadro de diálogo, seleccione **[!UICONTROL Conversiones mejoradas de Google Ads]** desde el [!UICONTROL Extensión] y, a continuación, seleccione **[!UICONTROL Enviar conversión]** bajo [!UICONTROL Tipo de acción].

![El [!UICONTROL Enviar conversión] tipo de acción seleccionado en la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Aparecen nuevos controles en el panel derecho que le permiten configurar la conversión. Como mínimo, se deben completar los campos siguientes:

**Información de conversión**

| Entrada | Descripción |
| --- | --- |
| Customer ID | Su [!DNL Google Ads] ID de cliente. El valor predeterminado es el ID de cliente que especificó al [instalación de la extensión](#install-enhanced-conversions). |
| ID de conversión o etiqueta de conversión | Valores de seguimiento obtenidos de [!DNL Google Ads] al configurar el seguimiento de conversión. Los valores comienzan por `AW-`.<br><br>Para obtener más información sobre cómo encontrar estos valores, consulte la [[!DNL Google Ads] documentación](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| El ID de transacción | Seleccione un elemento de datos que tenga el mismo valor de ID de transacción que [enviado desde el lado del cliente](#conversion-action-tags) uso del [!DNL Google Global Site Tag] extensión. |

**Identificación de usuario**

* Se debe incluir al menos uno de los tres identificadores de usuario:
   * Correo electrónico
   * N.º de teléfono
   * Dirección completa

>[!TIP]
>
>Los datos de identificación del usuario deben tener un cifrado hash para poder enviarlos a Google. Si los datos no tienen hash cuando el reenvío de eventos los recibe, seleccione la opción **[!UICONTROL Normalizar y hash]** active un campo determinado para indicar a la extensión que hash el valor.
>
>![El [!UICONTROL Normalizar y hash] alternancia habilitada para [!UICONTROL Correo electrónico] entrada dentro de [!UICONTROL Enviar conversión] formulario de configuración de acción.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para añadir la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo reenvío de eventos [generar](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Google Ads] uso del [!DNL Enhanced Conversions] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).
