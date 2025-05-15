---
title: Información general de área de nombres
description: Obtenga información sobre áreas de nombres de identidad en Identity Service.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 17%

---

# Información general de espacio de nombres

Lea el siguiente documento para obtener más información sobre lo que puede hacer con las áreas de nombres de identidad en el servicio de identidad de Adobe Experience Platform.

## Introducción

Áreas de nombres de identidad requiere una comprensión de varios servicios de Adobe Experience Platform. Antes de empezar a trabajar con áreas de nombres, revise la documentación de los servicios siguientes:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [[!DNL Identity Service]](../home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Privacy Service]](../../privacy-service/home.md): las áreas de nombres de identidad se utilizan en solicitudes de cumplimiento de regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD). Cada solicitud de privacidad se realiza en relación con un área de nombres para identificar qué datos de consumidores deben verse afectados.

## Explicación de los espacios de nombres de identidad {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Espacios de nombres de identidad"
>abstract="Un espacio de nombres de identidad es el contexto de una identidad determinada. Por ejemplo, un área de nombres de `Email` podría corresponder con **name<span>@acme.com**. Del mismo modo, un área de nombres de `Phone` podría corresponder con `555-555-1234`."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valores de identidad"
>abstract="Un valor de identidad es un identificador que representa a un particular, organización o recurso únicos. El contexto o tipo de identidad que representa el valor se define mediante un espacio de nombres de identidad correspondiente. Al hacer coincidir los datos de los registros en los fragmentos del perfil, el área de nombres y el valor de identidad deben coincidir. Al hacer coincidir los datos de los registros en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidir."
>text="Learn more in documentation"

Una identidad completa incluye dos componentes: un **valor de identidad** y un **área de nombres de identidad**. Por ejemplo, si el valor de una identidad es `scott@acme.com`, un área de nombres proporciona contexto a este valor distinguiéndolo como una dirección de correo electrónico. Del mismo modo, un área de nombres puede distinguir `555-123-456` como número de teléfono y `3126ABC` como CRMID. Básicamente, **un área de nombres proporciona contexto a una identidad determinada**. Al hacer coincidir datos de registro en fragmentos de perfil, como cuando [!DNL Real-Time Customer Profile] combina datos de perfil, tanto el valor de identidad como el área de nombres deben coincidir.

Por ejemplo, dos fragmentos de perfil pueden contener ID principales diferentes, pero comparten el mismo valor para el área de nombres &quot;Correo electrónico&quot;, por lo que Experience Platform puede ver que estos fragmentos son en realidad la misma persona y reúne los datos en el gráfico de identidades de dicha persona.

>[!BEGINSHADEBOX]

**Área de nombres de identidad explicada**

Otra manera de entender mejor el concepto de área de nombres es considerar ejemplos del mundo real como las ciudades y sus estados correspondientes. Por ejemplo, Portland, Maine y Portland, Oregón, son dos lugares diferentes en Estados Unidos. Aunque las ciudades comparten el mismo nombre, el estado funciona como un área de nombres y proporciona el contexto necesario que distingue a las dos ciudades entre sí.

Aplicación de la misma lógica al servicio de identidad:

* De un vistazo, el valor de identidad de: `1-234-567-8900` puede parecer un número de teléfono. Sin embargo, desde la perspectiva del sistema, este valor podría haberse configurado como CRMID. El servicio de identidad no tendría forma de aplicar el contexto necesario a este valor de identidad sin un área de nombres correspondiente.
* Otro ejemplo es el valor de identidad de: `john@gmail.com`. Aunque se puede suponer fácilmente que este valor de identidad es un correo electrónico, es totalmente posible que esté configurado como un CRMID de área de nombres personalizado. Con el área de nombres, puede distinguir `Email:john@gmail.com` de `CRMID:john@gmail.com`.

>[!ENDSHADEBOX]

### Componentes de un área de nombres

Un área de nombres consta de los siguientes componentes:

* **Nombre para mostrar**: El nombre descriptivo de un área de nombres determinada.
* **Símbolo de identidad**: código utilizado internamente por el servicio de identidad para representar un área de nombres.
* **Tipo de identidad**: La clasificación de un área de nombres determinada.
* **Descripción**: (Opcional) cualquier información adicional que pueda proporcionar con respecto a un área de nombres determinada.

### Tipo de identidad {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Especificar el tipo de identidad"
>abstract="El tipo de identidad controla si los datos se almacenan o no en el gráfico de identidad. Los gráficos de identidad no se generan para los siguientes tipos de identidad: identificadores de no persona e ID de socio."
>text="Learn more in documentation"

Un elemento de un área de nombres de identidad es **tipo de identidad**. El tipo de identidad determina:

* Si se generará un gráfico de identidad:
   * Los gráficos de identidad no se generan para los siguientes tipos de identidad: identificadores de no persona e ID de socio.
   * Los gráficos de identidad se generan para todos los demás tipos de identidad.
* Qué identidades se eliminan del gráfico de identidades cuando se alcanzan los límites del sistema. Para obtener más información, lea las [protecciones para los datos de identidad](../guardrails.md).

Los siguientes tipos de identidad están disponibles en Experience Platform:

| Tipo de identidad | Descripción |
| --- | --- |
| ID de cookies | Los ID de cookie identifican los navegadores web. Estas identidades son críticas para la expansión y constituyen la mayoría del gráfico de identidades. Sin embargo, por naturaleza se descomponen rápidamente y pierden su valor con el tiempo. |
| ID entre dispositivos | Los ID entre dispositivos identifican a un individuo y, por lo general, vinculan otros ID. Algunos ejemplos son un ID de inicio de sesión, CRMID y un ID de fidelidad. Esto es una indicación para que [!DNL Identity Service] gestione el valor de forma confidencial. |
| ID de dispositivo | Los ID de dispositivo identifican dispositivos de hardware, como IDFA (iPhone y iPad), GAID (Android) y RIDA (Roku), y pueden compartirse por varias personas en hogares. |
| Dirección de correo electrónico | Las direcciones de correo electrónico suelen estar asociadas a una sola persona y, por lo tanto, se pueden utilizar para identificarla en diferentes canales. Las identidades de este tipo incluyen información de identificación personal (PII). Esto es una indicación para que [!DNL Identity Service] gestione el valor de forma confidencial. |
| Identificador de no personas | Los ID que no son personas se utilizan para almacenar identificadores que requieren espacios de nombres, pero no están conectados a un clúster de personas. Por ejemplo, un SKU de producto, datos relacionados con productos, organizaciones o tiendas. |
| ID de socio | <ul><li>Los ID de socio son identificadores utilizados por los socios de datos para representar a personas. Los ID de socio suelen ser seudónimos para no revelar la verdadera identidad de una persona y pueden ser probabilísticos. En Real-Time Customer Data Platform, los ID de socio se utilizan principalmente para ampliar la activación de audiencias y el enriquecimiento de datos, y no para crear vínculos de gráficos de identidad.</li><li>Los gráficos de identidad no se generan al ingerir una identidad que incluye un área de nombres de identidad especificada como tipo de ID de socio.</li><li>Si no se incorporan datos del socio mediante el tipo de identidad del ID de socio, podrían alcanzarse las limitaciones del gráfico del sistema en el servicio de identidad, así como la combinación no deseada de perfiles.</li><ul> |
| Número de teléfono | Los números de teléfono suelen estar asociados a una sola persona y, por lo tanto, se pueden utilizar para identificarla en diferentes canales. Las identidades de este tipo incluyen PII. Esto es una indicación para que [!DNL Identity Service] gestione el valor de forma confidencial. |

{style="table-layout:auto"}

### Áreas de nombres estándar {#standard}

Experience Platform proporciona varias áreas de nombres de identidad disponibles para todas las organizaciones. Se conocen como áreas de nombres estándar y son visibles mediante la API [!DNL Identity Service] o a través de la interfaz de usuario de Experience Platform.

Se proporcionan las siguientes áreas de nombres estándar para su uso por todas las organizaciones dentro de Experience Platform:

| Nombre para mostrar | Descripción |
| ------------ | ----------- |
| Adcloud | Un área de nombres que representa Adobe AdCloud. |
| Adobe Analytics (ID heredado) | Un área de nombres que representa Adobe Analytics. Consulte el siguiente documento sobre [Áreas de nombres de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces) para obtener más información. |
| Apple IDFA (ID para anunciantes) | Área de nombres que representa el Apple ID para anunciantes. Consulte el siguiente documento sobre [anuncios basados en intereses](https://support.apple.com/en-us/HT202074) para obtener más información. |
| Servicio de notificaciones push de Apple | Un área de nombres que representa las identidades recopiladas mediante el servicio de notificaciones push de Apple. Consulte el siguiente documento en [Servicio de notificaciones push de Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obtener más información. |
| ECID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](./ecid.md) para obtener más información. |
| Correo electrónico | Un área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificarla en diferentes canales. |
| Correos electrónicos (SHA256, en minúsculas) | Un área de nombres para las direcciones de correo electrónico con hash previo. Los valores proporcionados en este área de nombres se convierten a minúsculas antes de crear valores hash con SHA256. Los espacios iniciales y finales deben recortarse antes de normalizar una dirección de correo electrónico. Esta configuración no se puede cambiar de forma retroactiva. Consulte el siguiente documento sobre la compatibilidad con hash [SHA256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) para obtener más información. |
| Firebase Cloud Messaging | Un área de nombres que representa las identidades recopiladas mediante Google Firebase Cloud Messaging para las notificaciones push. Consulte el siguiente documento sobre [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obtener más información. |
| ID de anuncio de Google (GAID) | Un área de nombres que representa un Google Advertising ID. Consulte el siguiente documento sobre [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obtener más información. |
| Teléfono | Área de nombres que representa un número de teléfono. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificarla en diferentes canales. |
| Teléfono (E.164) | Un espacio de nombres que representa los números de teléfono sin procesar que deben tener un cifrado hash en formato E.164. El formato E.164 incluye un signo más (`+`), un código de llamada de país internacional, un código de área local y un número de teléfono. Por ejemplo: `(+)(country code)(area code)(phone number)`. |
| Teléfono (SHA256) | Un área de nombres que representa los números de teléfono que deben tener un cifrado hash con SHA256. Debe quitar los símbolos, las letras y los ceros a la izquierda. También debe agregar el código de llamada de país como prefijo. |
| Teléfono (SHA256_E.164) | Un espacio de nombres que representa los números de teléfono sin procesar que deben llevar un hash con los formatos SHA256 y E.164. |
| TNTID | Un área de nombres que representa Adobe Target. Consulte el siguiente documento sobre [Target](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) para obtener más información. |
| Windows AID | Área de nombres que representa un Advertising ID de Windows. Consulte el siguiente documento en [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obtener más información. |

### Ver espacios de nombres de identidad {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Ver identidades de integración"
>abstract="Las identidades de integración son áreas de nombres que se utilizan para conectarse con otros sistemas y que no se utilizan en la resolución de identidades ni para unir identidades. <br> Estas identidades están ocultas de forma predeterminada. Utilice el conmutador para ver las áreas de nombres de integración."

Para ver áreas de nombres de identidad en la interfaz de usuario, selecciona **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, selecciona **[!UICONTROL Examinar]**.

Aparece un directorio de áreas de nombres en su organización, que muestra información sobre sus nombres, símbolos de identidad, fechas de última actualización, tipos de identidad correspondientes y descripción.

![Directorio de áreas de nombres de identidad personalizadas de su organización.](../images/namespace/browse.png)

## Crear áreas de nombres personalizadas {#create-namespaces}

Según los datos de organización y los casos de uso, puede requerir áreas de nombres personalizadas. Se pueden crear áreas de nombres personalizadas mediante la API [[!DNL Identity Service]](../api/create-custom-namespace.md) o mediante la interfaz de usuario.

Para crear un área de nombres personalizada, seleccione **[!UICONTROL Crear área de nombres de identidad]**.

>[!TIP]
>
>Las identidades de integración son áreas de nombres que se utilizan para conectarse con otros sistemas. No se utilizan para resolver identidades ni para vincular identidades. Seleccione **[!UICONTROL Ver identidades de integración]** para actualizar la lista e incluir identidades de integración. Sin embargo, las identidades de integración están ocultas de forma predeterminada porque son de solo vista y no es necesario configurarlas.

![Botón Crear área de nombres de identidad en el área de trabajo de identidades.](../images/namespace/create-identity-namespace.png)

Aparece la ventana [!UICONTROL Crear área de nombres de identidad]. En primer lugar, debe proporcionar un nombre para mostrar y un símbolo de identidad para el área de nombres personalizada que desea crear. Si lo desea, también puede proporcionar una descripción para agregar más contexto al área de nombres personalizada que está creando.

![Ventana emergente en la que puede escribir información sobre el área de nombres de identidad personalizada.](../images/namespace/name-and-symbol.png)

A continuación, seleccione el tipo de identidad que desea asignar al área de nombres personalizada. Cuando termine, seleccione **[!UICONTROL Crear]**.

![Una selección de tipos de identidad que puede elegir y asignar a su área de nombres de identidad personalizada.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Las áreas de nombres que defina son privadas para su organización y requieren un símbolo de identidad único para crearse correctamente.
>
>* Una vez creado un área de nombres, no se puede eliminar y no se puede cambiar su símbolo de identidad y tipo.
>
>* No se admiten áreas de nombres duplicadas. No se puede utilizar un nombre para mostrar y un símbolo de identidad existentes al crear un área de nombres nueva.

## Áreas de nombres en datos de identidad

El suministro del área de nombres para una identidad depende del método que utilice para proporcionar los datos de identidad. Para obtener más información sobre cómo proporcionar datos de identidad, lea la [[!DNL Identity Service] guía de implementación](../implementation.md).

## Pasos siguientes

Ahora que comprende los conceptos clave de las áreas de nombres de identidad, puede empezar a aprender a trabajar con su gráfico de identidad usando el [visor de gráficos de identidad](../features/identity-graph-viewer.md).
