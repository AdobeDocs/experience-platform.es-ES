---
title: Extensión de conversiones mejoradas de Google Ads
description: Obtenga información sobre la extensión de conversiones mejoradas de Google Ads para el reenvío de eventos en Adobe Experience Platform.
source-git-commit: a279c44ef9df3aa9bfc7763b153b87bde0015d57
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 1%

---

# [!DNL Google Ads] Extensión de conversiones mejorada

Al usar la variable [!DNL Google Ads] API, puede aprovechar [conversiones mejoradas](https://support.google.com/google-ads/answer/9888656) enviando datos de clientes de origen en forma de ajustes de conversión. Google utiliza estos datos adicionales para mejorar los informes de las conversiones en línea impulsadas por las interacciones de publicidad.

La variable [[!DNL Google Ads] Extensión de reenvío de eventos de conversiones mejorada](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (en lo sucesivo, &quot;el [!DNL Enhanced Conversions] ) proporciona una plantilla fácil de usar para implementar fácilmente conversiones mejoradas para la variable [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Las conversiones mejoradas solo funcionan para tipos de conversión en los que hay datos de clientes presentes, como suscripciones, suscripciones y compras. Debe estar disponible una o más de las siguientes partes de datos de clientes, ya que son necesarias cuando [configuración de una acción de conversión](#conversion-action-event-forwarding) para una regla de reenvío de eventos:
>
>* Dirección de correo electrónico (preferida)
>* Nombre y dirección de inicio (dirección de calle, ciudad, estado/región y código postal)
>* Número de teléfono (debe facilitarse además de uno de los otros dos datos anteriores)


## Información general sobre la implementación

Las conversiones mejoradas aprovechan el [!DNL Google Ads] para agregar datos de origen a una conversión que se produjo en un dispositivo cliente, normalmente un sitio web. Esto significa que existen dos pasos para implementar conversiones mejoradas:

1. Envíe una conversión desde el cliente.
1. Utilice el reenvío de eventos para enviar datos de origen adicionales que mejoren los datos de conversión enviados desde el cliente.

>[!TIP]
>
>Para asociar el evento de conversión del lado del cliente con los datos de origen enviados desde el reenvío de eventos, la variable `transaction_ID` debe ser el mismo en ambas llamadas. Para obtener más información sobre dónde se debe proporcionar este valor para cada servicio, consulte las secciones sobre la configuración de acciones de conversión para [etiquetas](#conversion-action-tags) y [reenvío de eventos](#conversion-action-event-forwarding), respectivamente.

Dado que el envío de eventos de conversión implica una implementación del lado del cliente y del lado del servidor, este documento cubre los pasos previos para configurar el lado del cliente [[!DNL Google Global Site Tag] Extensión (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) además de [!DNL Enhanced Conversions] extensión para el reenvío de eventos.

## Enviar una conversión mediante etiquetas

Para enviar un evento de conversión desde un sitio web, [!DNL Google Global Site Tag] (gtag) debe implementarse. Puede conseguirlo mediante etiquetas configurando e instalando el [!DNL Google Global Site Tag] (gtag) .

### Configure e instale el [!DNL Google Global Site Tag] Extensión

Vaya a la [!UICONTROL Recopilación de datos] IU o IU de Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Seleccione la propiedad tag en la que desea instalar la extensión y, a continuación, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , busque [!UICONTROL Etiqueta del sitio global de Google (gtag)] extensión y seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Etiqueta del sitio global de Google (gtag)] extensión seleccionada en la sección [!UICONTROL Extensiones] en la [!UICONTROL Recopilación de datos] IU.](../../../images/extensions/google-ads-enhanced-conversions/install-gtag-extension.png)

Aparecerá el cuadro de diálogo de instalación. Desde aquí, seleccione **[!UICONTROL Agregar cuenta]** y proporcione los siguientes valores cuando se le pida:

| Propiedad de la cuenta | Descripción |
| --- | --- |
| Nombre de la cuenta | Un nombre único para la cuenta. Este nombre solo se utiliza en la interfaz de usuario de etiquetas. |
| ID de cuenta | Su [!DNL Google Ads] ID de cuenta. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y vaya a: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La cadena del ID de la cuenta se puede encontrar en la ventana de fragmento de código que comienza con `AW-` o `d`. |
| Producto | Select **[!UICONTROL Publicidades de Google (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Cuando termine, seleccione **[!UICONTROL Agregar cuenta]** y, a continuación, seleccione **[!UICONTROL Guardar]**.

### Añadir una acción de conversión de envío {#conversion-action-tags}

Después de instalar la extensión, puede empezar a incluir acciones de conversión en las reglas de etiquetas. Al crear o editar una regla que escuche la conversión que desee mejorar, seleccione **[!UICONTROL Agregar]** under [!UICONTROL Acciones]. En el cuadro de diálogo siguiente, seleccione **[!UICONTROL Etiqueta del sitio global de Google (gtag)]** de la variable [!UICONTROL Extensión] lista desplegable y, a continuación, seleccione **[!UICONTROL Enviar un evento]** under [!UICONTROL Tipo de acción].

![La variable [!UICONTROL Enviar un evento] tipo de acción que se está seleccionando dentro de la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/google-ads-enhanced-conversions/select-client-action.png)

Aparecen controles adicionales que le permiten configurar la variable [!DNL gtag] evento. Como mínimo, se deben rellenar los campos siguientes:

1. **[!UICONTROL Nombre del evento (acción)]**: Entrar `conversion` como valor.
1. Añada un nuevo campo donde la clave sea `transaction_id` y el valor es un [elemento de datos](../../../ui/managing-resources/data-elements.md) que contiene el [ID de transacción](https://support.google.com/google-ads/answer/6386790) valor.
1. **[!UICONTROL Etiqueta de conversión]**: Introduzca la etiqueta de conversión adecuada en su [!DNL Google Ads] cuenta. Para encontrar este valor, inicie sesión en Google Ads y navegue hasta **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. La etiqueta de conversión se encuentra en [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Mientras se encuentra en el área de configuración de etiquetas de su [!DNL Google Ads] asegúrese de que las conversiones mejoradas están habilitadas. Para ello, revise y acepte las Condiciones de servicio y, a continuación, seleccione **[!DNL Turn on enhanced conversions]** y **[!DNL API]** como método de implementación.

Después de configurar la acción, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publique una nueva [versión](../../../ui/publishing/builds.md) para activar los cambios en la biblioteca.

## Envío de datos de origen mediante el reenvío de eventos

Una vez que pueda enviar eventos de conversión desde el lado del cliente, puede mejorar estas conversiones mediante el [!DNL Enhanced Conversions] extensión de reenvío de eventos.

### Crear un secreto de Google OAuth 2 y un elemento de datos {#create-secret-data-element}

Antes de configurar la extensión, debe crear un token de acceso en el reenvío de eventos para autenticarse en [!DNL Google Ads] API.

Consulte la guía de [creación de secretos de reenvío de eventos](../../../ui/event-forwarding/secrets.md) para ver los pasos detallados. Asegúrese de seleccionar **[!UICONTROL Google OAuth 2]** como tipo secreto. Siga las indicaciones y, cuando se le pida que seleccione un perfil de cuenta de Google, seleccione la cuenta que tenga acceso a la acción de conversión que está configurando.

Una vez creado el secreto, [crear un nuevo elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) y seleccione **[!UICONTROL Secreto]** para el tipo de elemento de datos. Seleccione el secreto de Google OAuth 2 apropiado para cada entorno y seleccione **[!UICONTROL Guardar en biblioteca]**.

### Configure e instale el [!DNL Enhanced Conversions] Extensión {#install-enhanced-conversions}

Busque la [!UICONTROL Conversiones mejoradas de Google Ads] en el catálogo de reenvío de eventos y seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Conversiones mejoradas de Google Ads] extensión seleccionada en la sección [!UICONTROL Extensiones] en la [!UICONTROL Recopilación de datos] IU.](../../../images/extensions/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar la extensión, debe rellenar los dos campos obligatorios:

1. **[!UICONTROL ID de cliente]**: El ID que identifica de forma exclusiva su [!DNL Google Ads] cuenta. Para encontrar este valor, inicie sesión en [!DNL Google Ads] y vaya a **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento de datos de token de acceso]**: Seleccione el icono del elemento de datos (![Icono de elemento de datos](../../../images/extensions/google-ads-enhanced-conversions/data-element-icon.png)) y elija el elemento de datos secreto de Google OAuth 2 que [configurado en el paso anterior](#create-secret-data-element) del menú .

Cuando termine, seleccione **[!UICONTROL Guardar]** para instalar la extensión de .

### Agregue un [!UICONTROL Enviar conversión] acción a una regla {#conversion-action-event-forwarding}

Una vez instalada la extensión, puede empezar a incluir [!UICONTROL Enviar conversión] en las reglas de reenvío de eventos. Al crear o editar una regla que escuche la conversión que desee mejorar, seleccione **[!UICONTROL Agregar]** under [!UICONTROL Acciones]. En el cuadro de diálogo siguiente, seleccione **[!UICONTROL Conversiones mejoradas de Google Ads]** de la variable [!UICONTROL Extensión] lista desplegable y, a continuación, seleccione **[!UICONTROL Enviar conversión]** under [!UICONTROL Tipo de acción].

![La variable [!UICONTROL Enviar conversión] tipo de acción que se está seleccionando dentro de la vista de configuración de acción del flujo de trabajo de edición de reglas.](../../../images/extensions/google-ads-enhanced-conversions/select-server-action.png)

Aparecen nuevos controles en el panel derecho que permiten configurar la conversión. Como mínimo, se deben completar los campos siguientes:

**Información de conversión**

| Entrada | Descripción |
| --- | --- |
| Customer ID | Su [!DNL Google Ads] ID de cliente. El valor predeterminado es el ID de cliente que introdujo al [instalación de la extensión](#install-enhanced-conversions). |
| ID de conversión o etiqueta de conversión | Valores de seguimiento obtenidos de [!DNL Google Ads] al configurar el seguimiento de conversión. Los valores comienzan con `AW-`.<br><br>Para obtener más información sobre cómo encontrar estos valores, consulte la [[!DNL Google Ads] documentación](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| El ID de transacción | Seleccione un elemento de datos que tenga el mismo valor de ID de transacción que [enviado desde el lado del cliente](#conversion-action-tags) usando la variable [!DNL Google Global Site Tag] extensión. |

**Identificación de usuario**

* Se debe incluir al menos uno de los tres identificadores de usuario:
   * Correo electrónico
   * N.º de teléfono
   * Dirección completa

>[!TIP]
>
>Los datos de identificación del usuario deben tener un cifrado hash antes de enviarse a Google. Si los datos no están hash cuando el reenvío de eventos los recibe, seleccione la opción **[!UICONTROL Normalizar y hash]** active un campo determinado para solicitar a la extensión que hash el valor.
>
>![La variable [!UICONTROL Normalizar y hash] alternancia habilitada para [!UICONTROL Correo electrónico] dentro de la variable [!UICONTROL Enviar conversión] formulario de configuración de acción.](../../../images/extensions/google-ads-enhanced-conversions/hash-user-id-values.png)

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publicar un nuevo reenvío de eventos [versión](../../../ui/publishing/builds.md) para activar los cambios en la biblioteca.

## Pasos siguientes

Esta guía explica cómo enviar eventos de conversión a [!DNL Google Ads] usando la variable [!DNL Enhanced Conversions] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [información general sobre el reenvío de eventos](../../../ui/event-forwarding/overview.md).
