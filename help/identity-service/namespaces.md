---
keywords: Experience Platform;inicio;temas populares;Área de nombres;Área de nombres;Áreas de nombres;Áreas de nombres;Área de nombres de identidad;Área de nombres de identidad;identidad;identidad;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Información general de Área de nombres de identidad
topic: sobre validación
description: 'Las áreas de nombres de identidad son un componente de Identity Service de   que sirve de indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de "name@email.com" como dirección de correo electrónico o "443522" como ID de CRM numérico. '
translation-type: tm+mt
source-git-commit: fc493a207e305887e798238ba6883f4934c5cba5
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 2%

---


# Información general sobre la Área de nombres de identidad

Las Áreas de nombres de identidad son un componente de [[!DNL Identity Service]](./home.md) que sirve como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de &quot;name<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID de CRM numérico.

## Primeros pasos

Trabajar con Áreas de nombres de identidad requiere comprender los distintos servicios de Adobe Experience Platform involucrados. Antes de comenzar a trabajar con Áreas de nombres, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Identity Service]](./home.md):: Obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
- [[!DNL Privacy Service]](../privacy-service/home.md):: Las Áreas de nombres de identidad se utilizan para cumplir con el Reglamento General de Protección de Datos (RGPD), en el que las solicitudes del RGPD pueden hacerse en relación con una Área de nombres.

## Explicación de las Áreas de nombres de identidad

Una identidad completa incluye un valor de ID y una Área de nombres. Al hacer coincidir los datos de registro en los fragmentos de perfil, como cuando [!DNL Real-time Customer Profile] combina datos de perfil, tanto el valor de identidad como la Área de nombres deben coincidir.

Por ejemplo: dos fragmentos de perfil pueden contener ID principales diferentes pero comparten el mismo valor para la Área de nombres &quot;Correo electrónico&quot;, por lo tanto [!DNL Platform] puede ver que estos fragmentos son en realidad el mismo individuo y reúne los datos en el gráfico de identidad del individuo.

![](images/identity-service-stitching.png)

### Tipos de identidad

Los datos se pueden identificar mediante varios tipos de identidad diferentes. El tipo de identidad se especifica en el momento en que se crea la Área de nombres de identidad y controla si los datos se conservan o no en el gráfico de identidad, así como las instrucciones especiales sobre cómo se deben gestionar dichos datos.

Los siguientes tipos de identidad están disponibles en [!DNL Platform]:

| Tipo de identidad | Descripción |
| --- | --- |
| ID de cookie | Los ID de cookies identifican a los exploradores Web. Estas identidades son fundamentales para la expansión y constituyen la mayoría del gráfico de identidad. Sin embargo, por naturaleza se descienden rápidamente y pierden su valor con el tiempo. |
| ID entre dispositivos | Los ID entre dispositivos identifican a un individuo y suelen unir otros ID. Algunos ejemplos son: ID de inicio de sesión, ID de CRM e ID de lealtad. Es una indicación para [!DNL Identity Service] manejar el valor con sensibilidad. |
| ID del dispositivo | Los ID de dispositivo identifican dispositivos de hardware, como IDFA (iPhone y iPad), GAID (Android) y RIDA (Roku), y pueden ser compartidos por varias personas en los hogares. |
| Correo electrónico Dirección | Las direcciones de correo electrónico suelen estar asociadas a una sola persona y, por lo tanto, pueden utilizarse para identificar a esa persona en diferentes canales. Las identidades de este tipo incluyen información de identificación personal (PII). Es una indicación para [!DNL Identity Service] manejar el valor con sensibilidad. |
| Identificador de no personas | Los ID que no son de personas se utilizan para almacenar identificadores que requieren Áreas de nombres pero que no están conectados a un clúster de personas. Por ejemplo: un SKU de producto, datos relacionados con productos, organizaciones o tiendas. |
| Número de teléfono | Los números de teléfono se asocian a menudo con una sola persona y, por lo tanto, pueden utilizarse para identificar a esa persona en diferentes canales. Las identidades de este tipo incluyen PII. Esto indica que [!DNL Identity Service] debe manejar el valor con sensibilidad. |

### Áreas de nombres estándar

Experience Platform proporciona varias Áreas de nombres de identidad que están disponibles para todas las organizaciones. Se conocen como Áreas de nombres estándar y se pueden ver mediante la API [!DNL Identity Service] o a través de la interfaz de usuario de la plataforma.

Todas las organizaciones de la Plataforma proporcionan las siguientes Áreas de nombres estándar:

| Nombre para mostrar | Descripción |
| ------------ | ----------- |
| Adcloud | Área de nombres que representa Adobe AdCloud. |
| Adobe Analytics (ID heredado) | Área de nombres que representa a Adobe Analytics. Consulte el siguiente documento en [Áreas de nombres de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) para obtener más información. |
| Apple IDFA (ID para anunciantes) | Área de nombres que representa el ID de Apple para anunciantes. Consulte el siguiente documento en [anuncios basados en intereses](https://support.apple.com/en-us/HT202074) para obtener más información. |
| Servicio de notificaciones push de Apple | Área de nombres que representa las identidades recopiladas mediante el servicio de notificaciones push de Apple. Consulte el siguiente documento en [servicio de notificaciones push de Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obtener más información. |
| CORE | Área de nombres que representa a Adobe Audience Manager. A esta Área de nombres también se puede hacer referencia por su nombre heredado: &quot;Adobe AudienceManager&quot;. Consulte el siguiente documento en [ID de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) para obtener más información. |
| ECID | Una Área de nombres que representa ECID. Esta Área de nombres también puede mencionarse mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento en [ECID](./ecid.md) para obtener más información. |
| Correo electrónico | Área de nombres que representa una dirección de correo electrónico. Este tipo de Área de nombres se asocia a menudo a una sola persona y, por lo tanto, puede utilizarse para identificar a esa persona en diferentes canales. |
| Correos electrónicos (SHA256, minúscula) | Una Área de nombres para la dirección de correo electrónico preestablecida. Los valores proporcionados en esta Área de nombres se convierten en minúsculas antes de crear el hash con SHA256. Los espacios al inicio y al final deben recortarse antes de normalizar una dirección de correo electrónico. Esta configuración no se puede cambiar de forma retroactiva. Consulte el siguiente documento sobre [compatibilidad con hash SHA256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) para obtener más información. |
| Mensajería en la nube de Firebase | Área de nombres que representa las identidades recopiladas mediante Google Firebase Cloud Messaging para notificaciones push. Consulte el siguiente documento en [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obtener más información. |
| ID de publicidad de Google (GAID) | Área de nombres que representa un ID de publicidad de Google. Consulte el siguiente documento en [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obtener más información. |
| ID de clics de Google | Área de nombres que representa un ID de Google Click. Consulte el siguiente documento en [Click tracking in Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) para obtener más información. |
| Phone | Área de nombres que representa un número de teléfono. Este tipo de Área de nombres se asocia a menudo a una sola persona y, por lo tanto, puede utilizarse para identificar a esa persona en diferentes canales. |
| Teléfono (E.164) | Una Área de nombres que representa los números de teléfono sin procesar que deben tener hash en formato E.164. El formato E.164 incluye un signo más (`+`), un código internacional de llamada al país, un código de área local y un número de teléfono. Por ejemplo: `(+)(country code)(area code)(phone number)`. |
| Teléfono (SHA256) | Una Área de nombres que representa los números de teléfono que deben tener hash mediante SHA256. Debe eliminar símbolos, letras y cualquier cero inicial. También debe agregar el código de llamada de país como prefijo. |
| Teléfono (SHA256_E.164) | Una Área de nombres que representa los números de teléfono sin procesar que deben tener hash con los formatos SHA256 y E.164. |
| TNTID | Área de nombres que representa a Adobe Target. Consulte el siguiente documento en [Destinatario](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) para obtener más información. |
| AID de Windows | Área de nombres que representa un ID de publicidad de Windows. Consulte el siguiente documento en [ID de publicidad de Windows](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obtener más información. |

Para vista de Áreas de nombres estándar en la interfaz de usuario, seleccione **[!UICONTROL Identidades]** en el menú de navegación de la izquierda y, a continuación, seleccione la ficha **[!UICONTROL Examinar]** para mostrar una lista de Áreas de nombres de identidad estándar accesibles para su organización. Puede ordenar las Áreas de nombres alfabéticamente por su **[!UICONTROL nombre para mostrar]**, **[!UICONTROL símbolo de identidad]** o **[!UICONTROL Propietario]**. También puede ordenar las Áreas de nombres cronológicamente según la fecha de actualización más reciente.

Seleccione una Área de nombres para ver información más específica sobre el carril derecho.

>[!NOTE]
>
>La plataforma también proporciona Áreas de nombres con fines de integración. Estas Áreas de nombres están ocultas de forma predeterminada, ya que se utilizan para conectarse con otros sistemas y no para unir identidades. Para obtener Áreas de nombres de integración de vista, seleccione **[!UICONTROL identidades de integración de Vista]**.

![](./images/browse-namespaces.png)

## Administración de Áreas de nombres personalizadas {#manage-namespaces}

Según los datos de la organización y los casos de uso, es posible que necesite Áreas de nombres personalizadas. Las Áreas de nombres personalizadas se pueden crear mediante la API [[!DNL Identity Service]](./api/create-custom-namespace.md) o a través de la interfaz de usuario.

Para crear una Área de nombres personalizada mediante la interfaz de usuario, vaya al espacio de trabajo **[!UICONTROL Identidades]**, seleccione **[!UICONTROL Examinar]** y, a continuación, seleccione **[!UICONTROL Crear Área de nombres de identidad]**.

![](./images/create.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear Área de nombres de identidad]**. Proporcione un **[!UICONTROL nombre único]** y **[!UICONTROL símbolo de identidad]** y, a continuación, seleccione el tipo de identidad que desee crear. También puede agregar una descripción opcional para obtener más información sobre la Área de nombres. Cuando termine, seleccione **[!UICONTROL Crear]**.

>[!IMPORTANT]
>
>Las Áreas de nombres que defina son privadas para su organización y requieren un símbolo de identidad único para poder crearlas correctamente.

![](./images/create-namespace.png)

De forma similar a las Áreas de nombres estándar, puede seleccionar una Área de nombres personalizada en la ficha **[!UICONTROL Examinar]** para vista de sus detalles. Sin embargo, con una Área de nombres personalizada también puede editar su nombre para mostrar y su descripción desde el área de detalles.

>[!NOTE]
>
>Una vez creada una Área de nombres, no se puede eliminar y no se puede cambiar su símbolo de identidad ni su tipo.

## Áreas de nombres en los datos de identidad

El suministro de la Área de nombres de una identidad depende del método que se utilice para proporcionar datos de identidad. Para obtener más información sobre cómo proporcionar datos de identidad de datos, consulte la sección sobre [suministro de datos de identidad](./home.md#supplying-identity-data-to-identity-service) en la [!DNL Identity Service] información general.

## Pasos siguientes

Ahora que comprende los conceptos clave de las Áreas de nombres de identidad, puede empezar a aprender a trabajar con el gráfico de identidad utilizando el [visor de gráficos de identidad](./ui/identity-graph-viewer.md).
