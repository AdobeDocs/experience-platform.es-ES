---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;esquemas;telecomunicaciones;suscripción;telecomunicaciones;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de suscripción de telecomunicaciones
description: Obtenga información acerca del grupo de campos Esquema de suscripción de telecomunicaciones.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 6%

---

# [!UICONTROL Suscripción de telecomunicaciones] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Suscripción de telecomunicaciones] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que describe el plan de suscripción de telecomunicaciones de un cliente, incluidos precios, paquetes y suscripciones a productos individuales.

El grupo de campos proporciona un único campo de tipo de objeto, `telecomSubscription`, cuyas propiedades se describen a continuación.

![Estructura de suscripción de telecomunicaciones](../../images/field-groups/telecom-subscription/structure.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `internetSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción a Internet, como límite de datos, tipo de conexión y detalles de velocidad. Consulte la [sección siguiente](#internetSubscription) para obtener más información. |
| `landlineSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción de teléfono fijo, incluidas las funciones seleccionadas, los minutos y los planes de marcación. Consulte la [sección siguiente](#landlineSubscription) para obtener más información. |
| `mediaSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción de medios, incluido el número de canales y los servicios de streaming incluidos. Consulte la [sección siguiente](#mediaSubscription) para obtener más información. |
| `mobileSubscription` | Matriz de objetos | Describe los detalles del plan de suscripción móvil, incluida la cantidad de líneas, las tarifas de datos, el coste, etc. Consulte la [sección siguiente](#mobileSubscription) para obtener más información. |
| `primarySubscriber` | [[!UICONTROL Persona]](../../data-types/person.md) | Describe el propietario de la suscripción. |
| `bundleName` | Cadena | Registra el nombre de cualquier tipo de paquete de suscripción al que esté suscrito el cliente, como `Internet + Media`. |
| `primaryPartyID` | Cadena | Identificador de la persona principal responsable de la suscripción, que por lo general podría ser el número de teléfono de su dispositivo. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Suscripción de telecomunicaciones]](../../data-types/telecom-subscription.md) | Describe los detalles generales de la suscripción, incluida la duración, las tarifas, el estado y mucho más. Describe los detalles generales de la suscripción, incluida la duración, las tarifas, el estado y mucho más. |
| `connectionType` | Cadena | Tipo de conexión de la suscripción. |
| `dataCap` | Número entero | Límite máximo de datos para la cuenta, en megabytes (MB). |
| `downloadSpeed` | Número entero | Velocidad máxima de descarga disponible con la suscripción, en megabytes (MB). |
| `selfSetup` | Booleano | Indica si un cliente es elegible para la configuración de Internet sin la visita de un técnico. |
| `uploadSpeed` | Número entero | Velocidad máxima de carga disponible con la suscripción, en megabytes (MB). |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de teléfono]](../../data-types/telecom-subscription.md) | Número de teléfono asignado a esta suscripción. |
| `subscriptionDetails` | [[!UICONTROL Suscripción de telecomunicaciones]](../../data-types/telecom-subscription.md) | Describe los detalles generales de la suscripción, incluida la duración, las tarifas, el estado y mucho más. |
| `callBlocking` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen bloqueo de llamadas. |
| `callForwarding` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen desvío de llamadas. |
| `callWaiting` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen llamadas en espera. |
| `callerID` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen el ID de llamante. |
| `internationalCalling` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen llamadas internacionales. |
| `minutes` | Número entero | La cantidad de minutos mensuales disponibles dentro de la suscripción. |
| `threeWayCalling` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen llamadas en tres direcciones. |
| `unlimitedDomesticLongDistance` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen llamadas nacionales a larga distancia ilimitadas. |
| `unlimitedLocalCalling` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen llamadas locales ilimitadas. |
| `voicemail` | Booleano | Indica si las funciones de suscripción de teléfono fijo incluyen buzón de voz. |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `streamingServices` | Matriz de objetos | Una lista de todos los servicios de streaming incluidos con la suscripción. Cada elemento de matriz incluye las siguientes propiedades: <ul><li>`promotionLength`: Duración de la promoción, en meses, si el servicio de streaming se añadió como parte de una promoción.</li><li>`promotionalAddition`: indica si el servicio de streaming se añadió como parte de una promoción.</li><li>`serviceName`: Nombre del servicio de streaming.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Suscripción de telecomunicaciones]](../../data-types/telecom-subscription.md) | Describe los detalles generales de la suscripción, incluida la duración, las tarifas, el estado y mucho más. |
| `channels` | Número entero | El número de canales incluidos con la suscripción de medios. |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de teléfono]](../../data-types/telecom-subscription.md) | Número de teléfono asignado a esta suscripción. |
| `subscriptionDetails` | [[!UICONTROL Suscripción de telecomunicaciones]](../../data-types/telecom-subscription.md) | Describe los detalles generales de la suscripción, incluida la duración, las tarifas, el estado y mucho más. |
| `earlyUpgradeEnrollment` | Booleano | Indica si el cliente acepta actualizaciones tempranas. |
| `planLevel` | Cadena | El nombre del plan móvil asignado a esta suscripción. |
| `portedNumber` | Booleano | Indica si el cliente transfiere su número a otro operador. |

{style="table-layout:auto"}
