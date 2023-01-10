---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;telecomunicaciones;suscripción;telecomunicaciones;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de suscripción de telecomunicaciones
description: Este documento proporciona una descripción general del grupo de campos de esquema de suscripción a telecomunicaciones.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 7%

---

# [!UICONTROL Suscripción a Telecom] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Suscripción a Telecom] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que describe el plan de suscripción de telecomunicaciones de un cliente, incluidos los precios, paquetes y suscripciones a productos individuales.

El grupo de campos proporciona un único campo de tipo objeto, `telecomSubscription`, cuyas propiedades se describen a continuación.

![Estructura de suscripción de telecomunicaciones](../../images/field-groups/telecom-subscription/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `internetSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción a Internet, como el límite de datos, el tipo de conexión y los detalles de velocidad. Consulte la [sección inferior](#internetSubscription) para obtener más información. |
| `landlineSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción de línea fija, incluidas las características seleccionadas, los minutos y los planes de marcado. Consulte la [sección inferior](#landlineSubscription) para obtener más información. |
| `mediaSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción de medios, incluido el número de canales y los servicios de flujo incluidos. Consulte la [sección inferior](#mediaSubscription) para obtener más información. |
| `mobileSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción móvil, incluido el número de líneas, las tasas de datos, el coste, etc. Consulte la [sección inferior](#mobileSubscription) para obtener más información. |
| `primarySubscriber` | [[!UICONTROL Persona]](../../data-types/person.md) | Describe el propietario de la suscripción. |
| `bundleName` | Cadena | Captura el nombre de cualquier tipo de paquete de suscripción en el que esté inscrito el cliente, como `Internet + Media`. |
| `primaryPartyID` | Cadena | Un identificador de la persona principal responsable de la suscripción, que normalmente podría ser su número de teléfono del dispositivo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Suscripción a Telecom]](../../data-types/telecom-subscription.md) | Describe detalles generales sobre la suscripción, como la longitud de la suscripción, las tarifas, el estado, etc. Describe detalles generales sobre la suscripción, como la longitud de la suscripción, las tarifas, el estado, etc. |
| `connectionType` | Cadena | Tipo de conexión de la suscripción. |
| `dataCap` | Número entero | Límite de límite de datos para la cuenta, en megabytes (MB). |
| `downloadSpeed` | Número entero | Velocidad máxima de descarga disponible para la suscripción, en megabytes (MB). |
| `selfSetup` | Booleano | Indica si un cliente es elegible para la configuración de Internet sin la visita de un técnico. |
| `uploadSpeed` | Número entero | Velocidad máxima de carga disponible para la suscripción, en megabytes (MB). |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL N.º de teléfono]](../../data-types/telecom-subscription.md) | El número de teléfono asignado a esta suscripción. |
| `subscriptionDetails` | [[!UICONTROL Suscripción a Telecom]](../../data-types/telecom-subscription.md) | Describe detalles generales sobre la suscripción, como la longitud de la suscripción, las tarifas, el estado, etc. |
| `callBlocking` | Booleano | Indica si las características de suscripción de línea fija incluyen el bloqueo de llamadas. |
| `callForwarding` | Booleano | Indica si las funciones de suscripción de línea fija incluyen el reenvío de llamadas. |
| `callWaiting` | Booleano | Indica si las características de suscripción de línea fija incluyen llamada en espera. |
| `callerID` | Booleano | Indica si las funciones de suscripción de línea fija incluyen el ID de llamador. |
| `internationalCalling` | Booleano | Indica si las características de suscripción de línea fija incluyen llamadas internacionales. |
| `minutes` | Número entero | Número de minutos mensuales disponibles dentro de la suscripción. |
| `threeWayCalling` | Booleano | Indica si las funciones de suscripción de línea fija incluyen llamadas tridireccionales. |
| `unlimitedDomesticLongDistance` | Booleano | Indica si las funciones de suscripción de línea fija incluyen llamadas de larga distancia domésticas ilimitadas. |
| `unlimitedLocalCalling` | Booleano | Indica si las funciones de suscripción de línea fija incluyen llamadas locales ilimitadas. |
| `voicemail` | Booleano | Indica si las funciones de suscripción de línea fija incluyen el correo de voz. |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `streamingServices` | Matriz de objetos | Una lista de todos los servicios de flujo continuo incluidos en la suscripción. Cada elemento de matriz incluye las siguientes propiedades: <ul><li>`promotionLength`: Duración de la promoción, en meses, si el servicio de transmisión se ha añadido como parte de una promoción.</li><li>`promotionalAddition`: Indica si el servicio de flujo continuo se agregó como parte de una promoción.</li><li>`serviceName`: Nombre del servicio de flujo continuo.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Suscripción a Telecom]](../../data-types/telecom-subscription.md) | Describe detalles generales sobre la suscripción, como la longitud de la suscripción, las tarifas, el estado, etc. |
| `channels` | Número entero | Número de canales incluidos con la suscripción de contenido. |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL N.º de teléfono]](../../data-types/telecom-subscription.md) | El número de teléfono asignado a esta suscripción. |
| `subscriptionDetails` | [[!UICONTROL Suscripción a Telecom]](../../data-types/telecom-subscription.md) | Describe detalles generales sobre la suscripción, como la longitud de la suscripción, las tarifas, el estado, etc. |
| `earlyUpgradeEnrollment` | Booleano | Indica si el cliente decide realizar actualizaciones anticipadas. |
| `planLevel` | Cadena | Nombre del plan móvil asignado a esta suscripción. |
| `portedNumber` | Booleano | Indica si el cliente transfiere su número desde otro operador. |

{style=&quot;table-layout:auto&quot;}
