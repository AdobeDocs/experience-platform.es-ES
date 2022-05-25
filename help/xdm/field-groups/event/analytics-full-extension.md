---
title: Grupo de campos de esquema de extensión completa de Adobe Analytics ExperienceEvent
description: Este documento proporciona una descripción general del grupo de campos de esquema de extensión completa de Adobe Analytics ExperienceEvent .
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 6%

---

# [!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent] grupo de campos de esquema

[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent] es un grupo de campos de esquema estándar para la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), que captura métricas comunes recopiladas por Adobe Analytics.

Este documento describe la estructura y el caso de uso del grupo de campos de extensión de Analytics .

>[!NOTE]
>
>Debido al tamaño y al número de elementos repetidos en este grupo de campos, muchos de los campos mostrados en esta guía se han contraído para ahorrar espacio. Para explorar la estructura completa de este grupo de campos, puede [busque en la interfaz de usuario de Platform ](../../ui/explore.md) o ver el esquema completo en la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Estructura del grupo de campo

El grupo de campos proporciona un solo `_experience` a un esquema, que contiene un único `analytics` objeto.

![Campos de nivel superior para el grupo de campos de Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `customDimensions` | Objeto | Captura dimensiones personalizadas rastreadas por Analytics. Consulte la [subsección abajo](#custom-dimensions) para obtener más información sobre el contenido de este objeto. |
| `endUser` | Objeto | Captura los detalles de interacción web del usuario final que activó el evento. Consulte la [subsección abajo](#end-user) para obtener más información sobre el contenido de este objeto. |
| `environment` | Objeto | Captura información sobre el explorador y el sistema operativo que activaron el evento. Consulte la [subsección abajo](#environment) para obtener más información sobre el contenido de este objeto. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Objeto | El grupo de campos proporciona campos de objeto para capturar hasta 1000 eventos personalizados. Consulte la [subsección abajo](#events) para obtener más información sobre estos campos. |
| `session` | Objeto | Captura información sobre la sesión que activó el evento. Consulte la [subsección abajo](#session) para obtener más información sobre el contenido de este objeto. |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` captura personalizadas [dimensiones](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=es) que Analytics rastrea.

![campo customDimensions](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `eVars` | Objeto | Un objeto que captura hasta 250 variables de conversión ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=es)). Las propiedades de este objeto tienen una clave `eVar1` a `eVar250` y solo aceptan cadenas para su tipo de datos. |
| `hierarchies` | Objeto | Un objeto que captura hasta cinco variables de jerarquía personalizada ([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=es)). Las propiedades de este objeto tienen una clave `hier1` a `hier5`, que son en sí mismos objetos con las siguientes subpropiedades:<ul><li>`delimiter`: El delimitador original utilizado para generar la lista proporcionada en `values`.</li><li>`values`: Una lista delimitada de nombres de nivel de jerarquía, representados como una cadena.</li></ul> |
| `listProps` | Objeto | Un objeto que captura hasta 75 [props de lista](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). Las propiedades de este objeto tienen una clave `prop1` a `prop75`, que son en sí mismos objetos con las siguientes subpropiedades:<ul><li>`delimiter`: El delimitador original utilizado para generar la lista proporcionada en `values`.</li><li>`values`: Una lista delimitada de valores para la prop, representados como una cadena.</li></ul> |
| `lists` | Objeto | Un objeto que captura hasta tres [listas](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). Las propiedades de este objeto tienen una clave `list1` a `list3`. Cada una de estas propiedades contiene una sola `list` matriz de [[!UICONTROL Par de valores clave]](../../data-types/key-value-pair.md) tipos de datos. |
| `props` | Objeto | Un objeto que captura hasta 75 [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). Las propiedades de este objeto tienen una clave `prop1` a `prop75` y solo aceptan cadenas para su tipo de datos. |
| `postalCode` | Cadena | Código postal proporcionado por el cliente. |
| `stateProvince` | Cadena | Ubicación de estado o provincia suministrada por el cliente. |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` captura los detalles de interacción web del usuario final que activó el evento.

![campo endUser](../../images/field-groups/analytics-full-extension/endUser.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Información web]](../../data-types/web-information.md) | La información relacionada con la página web, el vínculo y el referente del primer evento de experiencia para este usuario final. |
| `firstTimestamp` | Número entero | Una marca de tiempo Unix para el primer ExperienceEvent para este usuario final. |

## `environment` {#environment}

`environment` captura información sobre el explorador y el sistema operativo que activaron el evento.

![campo de entorno](../../images/field-groups/analytics-full-extension/environment.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `browserIDStr` | Cadena | El identificador de Adobe Analytics del explorador utilizado (también conocido como [dimensión de tipo de explorador](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | Cadena | El identificador de Adobe Analytics del sistema operativo utilizado (también conocido como [dimensión de tipo de sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Campos de eventos personalizados {#events}

El grupo de campos de extensión de Analytics proporciona diez campos de objeto que capturan hasta 100 [métricas de eventos personalizadas](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) cada una, para un total de 1000 para el grupo de campos.

Cada objeto de evento de nivel superior contiene los objetos de evento individuales para su intervalo respectivo. Por ejemplo, `event101to200` contiene los eventos desde los que se ha marcado `event101` a `event200`.

Cada objeto par utiliza la variable [[!UICONTROL Medida]](../../data-types/measure.md) tipo de datos, que proporciona un identificador único y un valor cuantificable.

![Campo de evento personalizado](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` captura información sobre la sesión que activó el evento.

![campo de sesión](../../images/field-groups/analytics-full-extension/session.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `search` | [[!UICONTROL Buscar]](../../data-types/search.md) | Captura información relacionada con la búsqueda web o móvil para la entrada de sesión. |
| `web` | [[!UICONTROL Información web]](../../data-types/web-information.md) | Captura información sobre clics en vínculos, detalles de páginas web, información del referente y detalles del explorador para la entrada de sesión. |
| `depth` | Número entero | Profundidad de la sesión actual (como el número de página) para el usuario final. |
| `num` | Número entero | Número de sesión actual del usuario final. |
| `timestamp` | Número entero | Marca de tiempo Unix para la entrada de sesión. |

## Pasos siguientes

Este documento abarcaba la estructura y el caso de uso del grupo de campos de la extensión de Analytics . Para obtener más información sobre el propio grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Si utiliza este grupo de campos para recopilar datos de Analytics mediante el SDK web de Adobe Experience Platform, consulte la guía de [configuración de un conjunto de datos](../../../edge/datastreams/overview.md) para aprender a asignar datos a XDM en el servidor.
