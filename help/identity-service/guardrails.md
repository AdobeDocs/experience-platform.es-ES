---
keywords: Experience Platform;identidad;servicio de identidad;resolución de problemas;protecciones;directrices;límite;
title: Protecciones del servicio de identidad
description: Este documento proporciona información sobre los límites de uso y tasa de los datos del servicio de identidad para ayudarle a optimizar su uso del gráfico de identidad.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 1%

---

# Protecciones para datos de [!DNL Identity Service]

Este documento proporciona información sobre los límites de uso y tasa de datos de [!DNL Identity Service] para ayudarle a optimizar el uso del gráfico de identidad. Al revisar las siguientes protecciones, se da por hecho que los datos se han modelado correctamente. Si tiene preguntas sobre cómo modelar los datos, póngase en contacto con su representante de servicio de atención al cliente.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

## Introducción 

Los siguientes servicios de Experience Platform participan en el modelado de datos de identidad:

* [Identidades](home.md): identidades de Bridge de diferentes fuentes de datos a medida que se incorporan en Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): cree perfiles de consumidor unificados con datos de varios orígenes.

## Límites del modelo de datos

Las tablas siguientes proporcionan directrices sobre protecciones para límites estáticos, así como reglas de validación que se deben tener en cuenta para áreas de nombres de identidad.

### Límites estáticos

En la tabla siguiente se describen los límites estáticos aplicados a los datos de identidad.

| Barrera | Límite | Notas |
| --- | --- | --- |
| Número de identidades en un gráfico | 50 | Cuando se actualiza un gráfico con 50 identidades vinculadas, el servicio de identidad aplicará el mecanismo de &quot;primero en entrar, primero en salir&quot; y eliminará la identidad más antigua para dejar espacio a la identidad más reciente para este gráfico (**Nota**: El perfil del cliente en tiempo real no se ve afectado). La eliminación se basa en el tipo de identidad y la marca de tiempo. El límite se aplica en el nivel de zona protegida. Para obtener más información, lea la sección sobre [comprensión de la lógica de eliminación](#deletion-logic). |
| Número de vínculos a una identidad para una sola ingesta por lotes | 50 | Un solo lote podría contener identidades anómalas que causan combinaciones de gráficos no deseadas. Para evitarlo, el servicio de identidad no ingerirá identidades que ya estén vinculadas a 50 o más identidades. |
| Número de identidades en un registro XDM | 20 | El número mínimo de registros XDM necesarios es de dos. |
| Número de áreas de nombres personalizadas | Ninguna | No hay límites en el número de áreas de nombres personalizadas que puede crear. |
| Número de caracteres de un nombre para mostrar o un símbolo de identidad | Ninguna | No hay límites en el número de caracteres de un nombre para mostrar o un símbolo de identidad. |

{style="table-layout:auto"}

### Validación del valor de identidad

En la tabla siguiente se describen las reglas existentes que debe seguir para garantizar una validación correcta del valor de identidad.

| Área de nombres | Regla de validación | Comportamiento del sistema cuando se infringe la regla |
| --- | --- | --- |
| ECID | <ul><li>El valor de identidad de un ECID debe ser exactamente de 38 caracteres.</li><li>El valor de identidad de un ECID debe constar solo de números.</li></ul> | <ul><li>Si el valor de identidad de ECID no es exactamente de 38 caracteres, se omite el registro.</li><li>Si el valor de identidad de ECID contiene caracteres no numéricos, se omite el registro.</li></ul> |
| No ECID | <ul><li>El valor de identidad no puede superar los 1024 caracteres.</li><li>Los valores de identidad no pueden ser &quot;null&quot;, &quot;anonymous&quot;, &quot;invalid&quot; ni ser una cadena vacía (por ejemplo: &quot;&quot;, &quot;&quot;, &quot; &quot;).</li></ul> | <ul><li>Si el valor de identidad supera los 1024 caracteres, se omite el registro.</li><li>Se bloqueará la ingesta de la identidad.</li></ul> |

{style="table-layout:auto"}

### Ingesta del área de identidad

A partir del 31 de marzo de 2023, el servicio de identidad bloqueará la ingesta de Adobe Analytics ID (AAID) para nuevos clientes. Esta identidad se incorpora generalmente a través de [Adobe Analytics source](../sources/connectors/adobe-applications/analytics.md) y [Adobe Audience Manager source](../sources//connectors/adobe-applications/audience-manager.md), y es redundante porque el ECID representa el mismo explorador web. Si desea cambiar esta configuración predeterminada, póngase en contacto con el equipo de la cuenta de Adobe.

## Explicación de la lógica de eliminación cuando se actualiza un gráfico de identidades en capacidad {#deletion-logic}

Cuando se actualiza un gráfico de identidad completo, el servicio de identidad elimina la identidad más antigua del gráfico antes de añadir la identidad más reciente. El objetivo de esto es mantener la precisión y la relevancia de los datos de identidad. Este proceso de eliminación sigue dos reglas principales:

### La eliminación del #1 de reglas se prioriza según el tipo de identidad de un área de nombres

La prioridad de eliminación es la siguiente:

1. ID de cookies
2. ID de dispositivo
3. ID entre dispositivos, correo electrónico y teléfono

### La eliminación del #2 de reglas se basa en la marca de tiempo almacenada en la identidad

Cada identidad vinculada en un gráfico tiene su propia marca de tiempo correspondiente. Cuando se actualiza un gráfico completo, el servicio de identidad elimina la identidad con la marca de tiempo más antigua.

Cuando se actualiza un gráfico completo con una nueva identidad, estas dos reglas funcionan en conjunto para designar qué identidad anterior se eliminará. El servicio de identidad elimina primero el ID de cookie más antiguo, después el ID de dispositivo más antiguo y, por último, el ID, el correo electrónico o el teléfono entre dispositivos más antiguos.

>[!NOTE]
>
>Si la identidad designada para eliminarse está vinculada a varias otras identidades en el gráfico, los vínculos que conectan esa identidad también se eliminarán.

### Implicaciones en la implementación

En las siguientes secciones se describen las implicaciones que la lógica de eliminación tiene para el servicio de identidad, el perfil del cliente en tiempo real y el SDK web.

#### Servicio de identidad: cambios en el tipo de identidad del área de nombres personalizada

Póngase en contacto con el equipo de su cuenta de Adobe para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene:

* Un área de nombres personalizada en la que los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.
* Un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.

Una vez que esta función esté disponible, los gráficos que excedan el límite de 50 identidades se reducirán hasta 50 identidades. Para Real-Time CDP B2C Edition, esto podría provocar un aumento mínimo en el número de perfiles aptos para una audiencia, ya que estos perfiles se ignoraban anteriormente en Segmentación y Activación.

#### Perfil del cliente en tiempo real: impacto en las audiencias a las que se puede dirigir

La eliminación solo se produce en los datos del servicio de identidad y no en el perfil del cliente en tiempo real.

* Por lo tanto, este comportamiento podría crear más perfiles con un solo ECID, ya que el ECID ya no forma parte del gráfico de identidad.
* Para mantenerse dentro de los números de derechos de audiencia a los que se puede dirigir, se recomienda habilitar la [caducidad de datos de perfil seudónimos](../profile/pseudonymous-profiles.md) para eliminar los perfiles antiguos.

#### Perfil del cliente en tiempo real y SDK web: eliminación de identidad principal

Si desea conservar los eventos autenticados con el ID de CRM, se recomienda cambiar los ID principales de ECID a ID de CRM. Lea los siguientes documentos para ver los pasos necesarios para implementar este cambio:

* [Configuración del mapa de identidad para las etiquetas de Experience Platform](../tags/extensions/client/web-sdk/data-element-types.md#identity-map).
* [Datos de identidad en el SDK web de Experience Platform](../web-sdk/identity/overview.md#using-identitymap)

### Casos de ejemplo

#### Ejemplo 1: gráfico grande típico

*Notas de diagrama:*

* `t` = marca de tiempo.
* El valor de una marca de tiempo corresponde a la actualización de una identidad determinada. Por ejemplo, `t1` representa la primera identidad vinculada (la más antigua) y `t51` representaría la identidad vinculada más reciente.

En este ejemplo, antes de poder actualizar el gráfico de la izquierda con una nueva identidad, el servicio de identidad elimina primero la identidad existente con la marca de tiempo más antigua. Sin embargo, como la identidad más antigua es un ID de dispositivo, el servicio de identidad omite esa identidad hasta que llega al área de nombres con un tipo que se encuentra más arriba en la lista de prioridades de eliminación, que en este caso es `ecid-3`. Una vez eliminada la identidad más antigua con un tipo de prioridad de eliminación más alta, el gráfico se actualiza con un nuevo vínculo, `ecid-51`.

* En el improbable caso de que haya dos identidades con la misma marca de tiempo y el mismo tipo de identidad, el servicio de identidad ordenará los identificadores en función de [XID](./api/list-native-id.md) y realizará la eliminación.

![Ejemplo de la identidad más antigua que se está eliminando para dar cabida a la identidad más reciente](./images/graph-limits-v3.png)

#### Ejemplo 2: &quot;división de gráficos&quot;

>[!BEGINTABS]

>[!TAB Evento entrante]

*Notas de diagrama:*

* El diagrama siguiente supone que en `timestamp=50` existen 50 identidades en el gráfico de identidades.
* `(...)` significa las otras identidades que ya están vinculadas en el gráfico.

En este ejemplo, ECID:32110 se ingiere y se vincula a un gráfico grande en `timestamp=51`, por lo tanto se supera el límite de 50 identidades.

![](./images/guardrails/before-split.png)

>[!TAB Proceso de eliminación]

Como resultado, el servicio de identidad elimina la identidad más antigua en función de la marca de tiempo y el tipo de identidad. En este caso, ECID:35577 solo se elimina del gráfico de identidades.

![](./images/guardrails/during-split.png)

>[!TAB Salida de gráfico]

Como resultado de la eliminación de ECID:35577, también se eliminan los extremos que vinculaban CRM ID:60013 y CRM ID:25212 con el ahora eliminado ECID:35577. Este proceso de eliminación hace que el gráfico se divida en dos gráficos más pequeños.

![](./images/guardrails/after-split.png)

>[!ENDTABS]

#### Ejemplo 3: &quot;radial&quot;

>[!BEGINTABS]

>[!TAB Evento entrante]

*Notas de diagrama:*

* El diagrama siguiente supone que en `timestamp=50` existen 50 identidades en el gráfico de identidades.
* `(...)` significa las otras identidades que ya están vinculadas en el gráfico.

En virtud de la lógica de eliminación, algunas identidades &quot;hub&quot; también se pueden eliminar. Estas identidades de concentrador hacen referencia a nodos que están vinculados a varias identidades individuales que, de lo contrario, se desvincularían.

En el ejemplo siguiente, ECID:21011 se ingiere y se vincula al gráfico en `timestamp=51`, por lo tanto se supera el límite de 50 identidades.

![](./images/guardrails/hub-and-spoke-start.png)

>[!TAB Proceso de eliminación]

Como resultado, el servicio de identidad elimina la identidad más antigua solo del gráfico de identidad, que en este caso es ECID:35577. La eliminación de ECID:35577 también provoca la eliminación de lo siguiente:

* El vínculo entre CRM ID: 60013 y el ahora eliminado ECID:35577, lo que da como resultado un escenario de división de gráficos.
* IDFA: 32110, IDFA: 02383 y las identidades restantes representadas por `(...)`. Estas identidades se eliminan porque, individualmente, no están vinculadas a ninguna otra identidad y, por lo tanto, no se pueden representar en un gráfico.

![](./images/guardrails/hub-and-spoke-process.png)

>[!TAB Salida de gráfico]

Por último, el proceso de eliminación genera dos gráficos más pequeños.

![](./images/guardrails/hub-and-spoke-result.png)

>[!ENDTABS]

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre [!DNL Identity Service]:

* [Información general de [!DNL Identity Service]](home.md)
* [Visualizador de gráficos de identidad](features/identity-graph-viewer.md)

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-time Customer Data Platform (edición B2C - paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (paquetes B2B - Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
