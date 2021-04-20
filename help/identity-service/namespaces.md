---
keywords: Experience Platform;inicio;temas populares;área de nombres;área de nombres;espacios de nombres;área de nombres;área de nombres de identidad;área de nombres de identidad;identidad;identidad;servicio de identidad
solution: Experience Platform
title: Información general sobre el área de nombres de identidad
topic: overview
description: 'Las áreas de nombres de identidad son un componente de Identity Service de   que sirve de indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de "name@email.com" como dirección de correo electrónico o "443522" como ID de CRM numérico. '
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 2%

---


# Información general del área de nombres de identidad

Las áreas de nombres de identidad son un componente de [[!DNL Identity Service]](./home.md) que sirve como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de &quot;name<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como un ID de CRM numérico.

## Primeros pasos

El trabajo con áreas de nombres de identidad requiere comprender los distintos servicios de Adobe Experience Platform implicados. Antes de comenzar a trabajar con áreas de nombres, revise la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Identity Service]](./home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
- [[!DNL Privacy Service]](../privacy-service/home.md): Las áreas de nombres de identidad se utilizan para cumplir con el Reglamento General de Protección de Datos (RGPD), donde las solicitudes de RGPD se pueden realizar en relación con un área de nombres.

## Explicación de las áreas de nombres de identidad

Una identidad completa incluye un valor de ID y un área de nombres. Al hacer coincidir datos de registro en fragmentos de perfil, como cuando [!DNL Real-time Customer Profile] combina datos de perfil, tanto el valor de identidad como el espacio de nombres deben coincidir.

Por ejemplo, dos fragmentos de perfil pueden contener ID principales diferentes, pero comparten el mismo valor para el espacio de nombres &quot;Correo electrónico&quot;. Por lo tanto, [!DNL Platform] puede ver que estos fragmentos son en realidad el mismo individuo y reúne los datos en el gráfico de identidad para el individuo.

![](images/identity-service-stitching.png)

### Tipos de identidad

Los datos se pueden identificar mediante varios tipos de identidad diferentes. El tipo de identidad se especifica en el momento en que se crea el área de nombres de identidad y controla si los datos se mantienen en el gráfico de identidad y cualquier instrucción especial para cómo se deben administrar esos datos.

Los siguientes tipos de identidad están disponibles en [!DNL Platform]:

| Tipo de identidad | Descripción |
| --- | --- |
| ID de cookie | Los ID de cookie identifican a los navegadores web. Estas identidades son críticas para la expansión y constituyen la mayoría del gráfico de identidad. Sin embargo, por naturaleza se descienden rápidamente y pierden su valor con el tiempo. |
| ID entre dispositivos | Los ID entre dispositivos identifican a un individuo y suelen unir otros ID. Algunos ejemplos son: ID de inicio de sesión, ID de CRM e ID de fidelidad. Esto indica que [!DNL Identity Service] debe administrar el valor con sensibilidad. |
| ID del dispositivo | Los ID de dispositivo identifican dispositivos de hardware, como IDFA (iPhone y iPad), GAID (Android) y RIDA (Roku), y pueden compartirlos varias personas en los hogares. |
| Correo electrónico Dirección | Las direcciones de correo electrónico suelen estar asociadas a una sola persona y, por lo tanto, se pueden utilizar para identificar a esa persona en diferentes canales. Las identidades de este tipo incluyen información de identificación personal (PII). Esto indica que [!DNL Identity Service] debe administrar el valor con sensibilidad. |
| Identificador de no personas | Los ID que no son de personas se utilizan para almacenar identificadores que requieren áreas de nombres pero que no están conectados a un clúster de personas. Por ejemplo, un SKU de producto, datos relacionados con productos, organizaciones o tiendas. |
| Número de teléfono | Los números de teléfono a menudo se asocian con una sola persona y, por lo tanto, se pueden utilizar para identificar a esa persona en diferentes canales. Las identidades de este tipo incluyen PII. Esto indica [!DNL Identity Service] que debe administrar el valor con sensibilidad. |

### Espacios de nombres estándar

Experience Platform proporciona varios espacios de nombres de identidad disponibles para todas las organizaciones. Estos se conocen como áreas de nombres estándar y son visibles mediante la API [!DNL Identity Service] o a través de la interfaz de usuario de Platform.

Las siguientes áreas de nombres estándar se proporcionan para su uso por todas las organizaciones dentro de Platform:

| Nombre para mostrar | Descripción |
| ------------ | ----------- |
| Adcloud | Área de nombres que representa Adobe AdCloud. |
| Adobe Analytics (ID heredado) | Área de nombres que representa Adobe Analytics. Consulte el siguiente documento en [Áreas de nombres de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) para obtener más información. |
| Apple IDFA (ID para anunciantes) | Un espacio de nombres que representa el ID de Apple para anunciantes. Consulte el siguiente documento sobre [anuncios basados en intereses](https://support.apple.com/en-us/HT202074) para obtener más información. |
| Servicio de notificaciones push de Apple | Un espacio de nombres que representa las identidades recopiladas mediante el servicio de notificaciones push de Apple. Consulte el siguiente documento sobre el [servicio de notificaciones push de Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obtener más información. |
| CORE | Área de nombres que representa Adobe Audience Manager. Este espacio de nombres también puede ser referenciado por su nombre heredado: &quot;Adobe AudienceManager&quot;. Consulte el siguiente documento sobre [Audience Manager IDs](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) para obtener más información. |
| ECID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](./ecid.md) para obtener más información. |
| Correo electrónico | Área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificar a esa persona en diferentes canales. |
| Correos electrónicos (SHA256, en minúsculas) | Un espacio de nombres para direcciones de correo electrónico premarcadas. Los valores proporcionados en este área de nombres se convierten a minúsculas antes de utilizar el hash con SHA256. Los espacios al inicio y al final deben recortarse antes de normalizar una dirección de correo electrónico. Esta configuración no se puede cambiar de forma retroactiva. Consulte el siguiente documento sobre [SHA256 hashing support](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) para obtener más información. |
| Firebase Cloud Messaging | Un espacio de nombres que representa las identidades recopiladas mediante Google Firebase Cloud Messaging para notificaciones push. Consulte el siguiente documento en [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obtener más información. |
| Google Ad ID (GAID) | Área de nombres que representa un ID de publicidad de Google. Consulte el siguiente documento en [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obtener más información. |
| ID de clic de Google | Área de nombres que representa un ID de clic de Google. Consulte el siguiente documento sobre [Seguimiento de clics en Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) para obtener más información. |
| Phone | Área de nombres que representa un número de teléfono. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificar a esa persona en diferentes canales. |
| Teléfono (E.164) | Un espacio de nombres que representa los números de teléfono sin procesar que deben tener un hash en formato E.164. El formato E.164 incluye un signo más (`+`), un código de país internacional, un código de área local y un número de teléfono. Por ejemplo: `(+)(country code)(area code)(phone number)`. |
| Teléfono (SHA256) | Área de nombres que representa los números de teléfono que deben tener un hash con SHA256. Debe eliminar símbolos, letras y cualquier cero inicial. También debe añadir el código de llamada al país como prefijo. |
| Teléfono (SHA256_E.164) | Área de nombres que representa los números de teléfono sin procesar que deben tener un hash con los formatos SHA256 y E.164. |
| TNTID | Un espacio de nombres que representa Adobe Target. Consulte el siguiente documento en [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) para obtener más información. |
| AID de Windows | Área de nombres que representa un ID de publicidad de Windows. Consulte el siguiente documento en [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obtener más información. |

Para ver las áreas de nombres estándar en la interfaz de usuario, seleccione **[!UICONTROL Identities]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Browse]** para mostrar una lista de áreas de nombres de identidad estándar accesibles para su organización. Puede ordenar los espacios de nombres alfabéticamente por su **[!UICONTROL Nombre para mostrar]**, **[!UICONTROL Símbolo de identidad]** o **[!UICONTROL Propietario]**. Alternativamente, puede ordenar los espacios de nombres cronológicamente según la fecha de actualización más reciente.

Seleccione un espacio de nombres para ver información más específica en el carril derecho.

>[!NOTE]
>
>Platform también proporciona áreas de nombres para fines de integración. Estas áreas de nombres están ocultas de forma predeterminada, ya que se utilizan para conectarse con otros sistemas y no para unir identidades. Para ver los espacios de nombres de integración, seleccione **[!UICONTROL View integration identities]**.

![](./images/browse-namespaces.png)

## Administración de áreas de nombres personalizadas {#manage-namespaces}

Según los datos organizativos y los casos de uso, es posible que necesite espacios de nombres personalizados. Las áreas de nombres personalizadas se pueden crear utilizando la API [[!DNL Identity Service]](./api/create-custom-namespace.md) o a través de la interfaz de usuario.

Para crear un área de nombres personalizada mediante la interfaz de usuario, vaya al espacio de trabajo **[!UICONTROL Identities]**, seleccione **[!UICONTROL Browse]** y, a continuación, seleccione **[!UICONTROL Create identity namespace]**.

![](./images/create.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear área de nombres de identidad]**. Proporcione un **[!UICONTROL Display name]** y un **[!UICONTROL Identity *]** únicos y, a continuación, seleccione el tipo de identidad que desea crear. También puede agregar una descripción opcional para obtener más información sobre el área de nombres. Cuando termine, seleccione **[!UICONTROL Crear]**.

>[!IMPORTANT]
>
>Los espacios de nombres que defina son privados para su organización y requieren un símbolo de identidad único para poder crearlos correctamente.

![](./images/create-namespace.png)

Al igual que las áreas de nombres estándar, puede seleccionar un área de nombres personalizada en la pestaña **[!UICONTROL Browse]** para ver sus detalles. Sin embargo, con un espacio de nombres personalizado también puede editar su nombre para mostrar y su descripción desde el área de detalles.

>[!NOTE]
>
>Una vez creado un espacio de nombres, no se puede eliminar y su símbolo de identidad y tipo no se pueden cambiar.

## Espacios de nombres en datos de identidad

El suministro del área de nombres para una identidad depende del método que utilice para proporcionar datos de identidad. Para obtener más información sobre cómo proporcionar datos de identidad de datos, consulte la sección sobre [suministro de datos de identidad](./home.md#supplying-identity-data-to-identity-service) en la [!DNL Identity Service] descripción general.

## Pasos siguientes

Ahora que comprende los conceptos clave de los áreas de nombres de identidad, puede empezar a aprender a trabajar con el gráfico de identidad utilizando el [visor de gráficos de identidad](./ui/identity-graph-viewer.md).
