---
title: Extensión de conversiones mejoradas de Google Ads
description: Obtenga información acerca de la extensión de conversiones mejoradas de Google Ads para el reenvío de eventos en Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# Extensión de conversiones mejoradas de [!DNL Google Ads]

Con la API [!DNL Google Ads], puede aprovechar [conversiones mejoradas](https://support.google.com/google-ads/answer/9888656) enviando datos de clientes de origen en forma de ajustes de conversión. Google utiliza estos datos adicionales para mejorar los informes de las conversiones en línea impulsadas por las interacciones publicitarias.

La extensión de reenvío de eventos [[!DNL Google Ads] Conversiones mejoradas](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (antes conocida como la extensión [!DNL Enhanced Conversions]) proporciona una plantilla fácil de usar para implementar fácilmente conversiones mejoradas para la API [!DNL Google Ads].

>[!IMPORTANT]
>
>Las conversiones mejoradas solo funcionan para tipos de conversión en los que hay datos de clientes presentes, como suscripciones, suscripciones y compras. Uno o más de los siguientes datos de clientes deben estar disponibles, ya que son necesarios al [configurar una acción de conversión](#conversion-action-event-forwarding) para una regla de reenvío de eventos:
>
>* Correo electrónico (preferido)
>* Nombre y dirección postal (dirección postal, ciudad, estado/región y código postal)
>* Número de teléfono (debe proporcionarse además de uno de los otros dos datos anteriores)

## Resumen de implementación

Las conversiones mejoradas aprovechan la API [!DNL Google Ads] para agregar datos de origen a una conversión que se produjo en un dispositivo cliente, normalmente un sitio web. Esto significa que hay dos pasos para implementar conversiones mejoradas:

1. Envíe una conversión desde el cliente.
1. Utilice el reenvío de eventos para enviar datos de origen adicionales que mejoren los datos de conversión enviados desde el cliente.

>[!TIP]
>
>Para asociar el evento de conversión del lado del cliente con los datos de origen enviados desde el reenvío de eventos, `transaction_ID` debe ser el mismo en ambas llamadas. Para obtener más información sobre dónde se debe proporcionar este valor para cada servicio, consulte las secciones sobre configuración de acciones de conversión para [tags](#conversion-action-tags) y [reenvío de eventos](#conversion-action-event-forwarding), respectivamente.

Dado que el envío de eventos de conversión implica una implementación del lado del cliente y del lado del servidor, este documento cubre los pasos previos para configurar la extensión [[!DNL Google Global Site Tag] (gtag) del lado del cliente ](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag), además de la extensión [!DNL Enhanced Conversions] para el reenvío de eventos.

El siguiente vídeo proporciona una introducción a la extensión [!DNL Enhanced Conversions] y explica los pasos de implementación en un nivel superior:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Envío de una conversión mediante etiquetas

Para enviar un evento de conversión desde un sitio web, [!DNL Google Global Site Tag] (gtag) debe implementarse. Puede conseguirlo utilizando etiquetas configurando e instalando la extensión [!DNL Google Global Site Tag] (gtag).

### Configurar e instalar la extensión [!DNL Google Global Site Tag]

Vaya a la interfaz de usuario de [!UICONTROL Recopilación de datos] o a la interfaz de usuario de Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Seleccione la propiedad de etiqueta en la que desea instalar la extensión y, a continuación, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, busque la extensión [!UICONTROL Google Global Site Tag (gtag)] y seleccione **[!UICONTROL Instalar]**.

![La extensión [!UICONTROL Google Global Site Tag (gtag)] se está seleccionando en la vista [!UICONTROL Extensiones] de la interfaz de usuario de [!UICONTROL Recopilación de datos].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Aparecerá el cuadro de diálogo de instalación. Desde aquí, seleccione **[!UICONTROL Agregar cuenta]** y proporcione los siguientes valores cuando se le solicite:

| Propiedad de cuenta | Descripción |
| --- | --- |
| Nombre de la cuenta | Un nombre único para la cuenta. Este nombre solo se utiliza en la interfaz de usuario de etiquetas. |
| ID de cuenta | Su ID de cuenta de [!DNL Google Ads]. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y navegue hasta: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La cadena del identificador de cuenta se encuentra en la ventana del fragmento de código que comienza con `AW-` o `d`. |
| Producto | Seleccione **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Cuando termine, selecciona **[!UICONTROL Agregar cuenta]** y luego selecciona **[!UICONTROL Guardar]**.

### Agregar una acción de conversión de envío {#conversion-action-tags}

Después de instalar la extensión, puede empezar a incluir acciones de conversión en las reglas de etiquetas. Al crear o editar una regla que escucha la conversión que desea mejorar, seleccione **[!UICONTROL Agregar]** en [!UICONTROL Acciones]. En el siguiente cuadro de diálogo, selecciona **[!UICONTROL Etiqueta de sitio global de Google (gtag)]** en el menú desplegable [!UICONTROL Extensión], luego selecciona **[!UICONTROL Enviar un evento]** en [!UICONTROL Tipo de acción].

![El tipo de acción [!UICONTROL Enviar un evento] está seleccionado en la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Aparecen controles adicionales que le permiten configurar el evento [!DNL gtag]. Como mínimo, se deben rellenar los campos siguientes:

1. **[!UICONTROL Nombre del evento (Acción)]**: escriba `conversion` como valor.
1. Agregue un nuevo campo donde la clave sea `transaction_id` y el valor sea un [elemento de datos](../../../ui/managing-resources/data-elements.md) que contenga el valor [ID de transacción](https://support.google.com/google-ads/answer/6386790).
1. **[!UICONTROL Etiqueta de conversión]**: escribe la etiqueta de conversión adecuada desde tu cuenta de [!DNL Google Ads]. Para encontrar este valor, inicie sesión en Google Ads y vaya a **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. La etiqueta de conversión se encuentra en [!DNL Instructions].

   >[!IMPORTANT]
   >
   >Mientras se encuentra en el área de configuración de etiquetas de su cuenta de [!DNL Google Ads], asegúrese de que las conversiones mejoradas estén habilitadas. Para ello, revise y acepte los Términos de servicio y, a continuación, seleccione **[!DNL Turn on enhanced conversions]** y **[!DNL API]** como método de implementación.

Una vez configurada la acción, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique una nueva [compilación](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Envío de datos de origen mediante el reenvío de eventos

Una vez que pueda enviar eventos de conversión desde el lado del cliente, puede mejorar estas conversiones mediante la extensión de reenvío de eventos [!DNL Enhanced Conversions].

### Crear un secreto y un elemento de datos de Google OAuth 2 {#create-secret-data-element}

Antes de configurar la extensión, debe crear un token de acceso en el reenvío de eventos para autenticarse en la API [!DNL Google Ads].

Consulte la guía sobre [creación de secretos de reenvío de eventos](../../../ui/event-forwarding/secrets.md) para ver los pasos detallados. Asegúrese de seleccionar **[!UICONTROL Google OAuth 2]** como tipo secreto. Siga las indicaciones y, cuando se le pida que seleccione un perfil de cuenta de Google, seleccione la cuenta que tenga acceso a la acción de conversión que está configurando.

Una vez creado el secreto, [cree un nuevo elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) y seleccione **[!UICONTROL Secreto]** para el tipo de elemento de datos. Seleccione el secreto de Google OAuth 2 apropiado para cada entorno y seleccione **[!UICONTROL Guardar en biblioteca]**.

### Configurar e instalar la extensión [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Busque la extensión [!UICONTROL Conversiones mejoradas de Google Ads] en el catálogo de reenvío de eventos y seleccione **[!UICONTROL Instalar]**.

![La extensión [!UICONTROL Conversiones mejoradas de Google Ads] se está seleccionando en la vista [!UICONTROL Extensiones] de la interfaz de usuario de [!UICONTROL Recopilación de datos].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar la extensión, debe rellenar los dos campos obligatorios:

1. **[!UICONTROL ID de cliente]**: El ID que identifica de forma exclusiva su cuenta de [!DNL Google Ads]. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y navegue hasta **[!DNL Help]** > **[!DNL Customer ID]**.
2. **[!UICONTROL Elemento de datos de token de acceso]**: seleccione el icono de elemento de datos (![icono de elemento de datos](/help/images/icons/database.png)) y elija el elemento de datos secreto de OAuth 2 de Google que [configuró en el paso anterior](#create-secret-data-element) del menú.

Cuando termine, seleccione **[!UICONTROL Guardar]** para instalar la extensión.

### Agregar una acción [!UICONTROL Enviar conversión] a una regla {#conversion-action-event-forwarding}

Una vez instalada la extensión, puede empezar a incluir las acciones [!UICONTROL Enviar conversión] en las reglas de reenvío de eventos. Al crear o editar una regla que escucha la conversión que deseas mejorar, selecciona **[!UICONTROL Agregar]** en [!UICONTROL Acciones]. En el siguiente cuadro de diálogo, selecciona **[!UICONTROL Conversiones mejoradas de Google Ads]** en el menú desplegable [!UICONTROL Extensión], luego selecciona **[!UICONTROL Enviar conversión]** en [!UICONTROL Tipo de acción].

![El tipo de acción [!UICONTROL Enviar conversión] se está seleccionando en la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Aparecen nuevos controles en el panel derecho que le permiten configurar la conversión. Como mínimo, se deben completar los campos siguientes:

**Información de conversión**

| Entrada | Descripción |
| --- | --- |
| ID de cliente | Su ID de cliente [!DNL Google Ads]. El valor predeterminado es el ID de cliente que especificó al [instalar la extensión](#install-enhanced-conversions). |
| ID de conversión o etiqueta de conversión | Valores de seguimiento obtenidos de [!DNL Google Ads] al configurar el seguimiento de conversión. Los valores comienzan con `AW-`.<br><br>Para obtener más información sobre cómo encontrar estos valores, consulte la [[!DNL Google Ads] documentación](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| El ID de transacción | Seleccione un elemento de datos que tenga el mismo valor de ID de transacción [enviado desde el lado del cliente](#conversion-action-tags) con la extensión [!DNL Google Global Site Tag]. |

**Identificación de usuario**

* Se debe incluir al menos uno de los tres identificadores de usuario:
   * Correo electrónico
   * Número de teléfono
   * Dirección completa

>[!TIP]
>
>Los datos de identificación del usuario deben tener un cifrado hash para poder enviarlos a Google. Si los datos no tienen hash cuando el reenvío de eventos los recibe, seleccione el botón de alternancia **[!UICONTROL Normalizar y hash]** en un campo determinado para indicar a la extensión que aplique hash al valor.
>
>![Se ha habilitado la opción [!UICONTROL Normalizar y hash] para la entrada de [!UICONTROL Correo electrónico] en el formulario de configuración de acción [!UICONTROL Enviar conversión].](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo reenvío de eventos [build](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Google Ads] mediante la extensión de reenvío de eventos [!DNL Enhanced Conversions]. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
