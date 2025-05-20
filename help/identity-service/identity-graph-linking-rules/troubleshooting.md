---
title: Guía de resolución de problemas para reglas de vinculación de gráficos de identidad
description: Obtenga información sobre cómo solucionar problemas comunes en Reglas de vinculación de gráficos de identidad.
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 28eab3488dccdcc6239b9499e875c31ff132fd48
workflow-type: tm+mt
source-wordcount: '3285'
ht-degree: 0%

---

# Guía de solución de problemas para [!DNL Identity Graph Linking Rules]

A medida que prueba y valida [!DNL Identity Graph Linking Rules], puede encontrar algunos problemas relacionados con la ingesta de datos y el comportamiento de gráficos. Lea este documento para aprender a solucionar algunos problemas comunes que podrían producirse al trabajar con [!DNL Identity Graph Linking Rules].

## Resumen del flujo de ingesta {#data-ingestion-flow-overview}

El diagrama siguiente es una representación simplificada de cómo fluyen los datos a Adobe Experience Platform y aplicaciones. Utilice este diagrama como referencia para comprender mejor el contenido de esta página.

![Diagrama de cómo fluye la ingesta de datos en el servicio de identidad.](../images/troubleshooting/dataflow_in_identity.png)

Es importante tener en cuenta los siguientes factores:

* Para la transmisión de datos, el perfil del cliente en tiempo real, el servicio de identidad y el lago de datos empezarán a procesar los datos cuando se envíen. Sin embargo, la latencia para completar el procesamiento de los datos depende del servicio. Normalmente, el procesamiento del lago de datos tardará más tiempo en compararse con el perfil y la identidad.
   * Si los datos no aparecen al ejecutar una consulta con un conjunto de datos incluso después de un par de horas, es probable que los datos no se hayan introducido en Experience Platform.
* Para los datos por lotes, todos los datos fluirán primero al lago de datos y, a continuación, los datos se propagarán a Perfil e Identidad si el conjunto de datos está habilitado para Perfil e Identidad.
* Para los problemas relacionados con la ingesta, es importante que el problema esté aislado en el nivel de servicio para una depuración y solución de problemas precisos. Hay tres tipos de problemas potenciales a considerar:

| Tipo de problema de ingesta | ¿Los datos se incorporan en el lago de datos? | ¿Los datos se incorporan en el perfil? | ¿Los datos se incorporan en el servicio de identidad? |
| --- | --- | --- | --- |
| Problema general de ingesta | No | No | No |
| Problema de gráfico | Sí | Sí | No |
| Problema de fragmento de perfil | Sí | No | Sí |

## Problemas de ingesta de datos {#data-ingestion-issues}

>[!NOTE]
>
>* En esta sección se da por hecho que los datos se han introducido correctamente en el lago de datos y que no hubo errores de sintaxis o de otro tipo que impidieran la ingesta de los datos en Experience Platform.
>
>* Los ejemplos utilizan ECID como el área de nombres de la cookie y CRMID como el área de nombres de la persona.

### Mis identidades no se están introduciendo en el servicio de identidad{#my-identities-are-not-getting-ingested-into-identity-service}

Esto puede deberse a varios motivos, entre los que se incluyen, entre otros:

* [El conjunto de datos no está habilitado para el perfil](../../catalog/datasets/enable-for-profile.md).
* El registro se omite porque solo hay una identidad en el evento.
* [Error de validación en el servicio de identidad](../guardrails.md#identity-value-validation).
   * Por ejemplo, un ECID podría haber superado la longitud máxima de 38 caracteres.
* De manera predeterminada, [AAID están bloqueados para la ingesta](../guardrails.md#identity-namespace-ingestion).
* Se ha quitado la identidad debido a [protecciones del sistema](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

En el contexto de [!DNL Identity Graph Linking Rules], se puede rechazar un registro del servicio de identidad porque el evento entrante tiene dos o más identidades con el mismo área de nombres única pero con un valor de identidad diferente. Este escenario suele ocurrir debido a errores de implementación.

Considere el siguiente evento con dos suposiciones:

1. El nombre de campo CRMID está marcado como una identidad con el área de nombres CRMID.
2. El CRMID del área de nombres se define como un área de nombres única.

El siguiente evento devolverá un mensaje de error que indica que la ingesta ha fallado.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Pasos para solucionar problemas**

Para resolver este error, primero debe recopilar la siguiente información:

* El valor de identidad (`identity_value`) que esperaba ingerir en el gráfico de identidad.
* Conjunto de datos (`dataset_name`) en el que se envió el evento.

A continuación, use [Adobe Experience Platform Query Service](../../query-service/home.md) y ejecute la siguiente consulta:

>[!TIP]
>
>Reemplace `dataset_name` y `identity_value` por la información que ha recopilado.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Después de ejecutar la consulta, busque el registro de evento que esperaba para generar un gráfico y, a continuación, compruebe que los valores de identidad son diferentes en la misma fila. Vea la siguiente imagen para ver un ejemplo:

![Consulta sin título que generó áreas de nombres duplicadas.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Si las dos identidades son exactamente iguales y si el evento se ingiere mediante streaming, tanto Identity como Profile anularán la duplicación de la identidad.

### Los ExperienceEvents posteriores a la autenticación se atribuyen al perfil autenticado incorrecto

La prioridad del área de nombres desempeña un papel importante en la forma en que los fragmentos de evento determinan la identidad principal.

* Una vez que haya configurado y guardado la [configuración de identidad](./identity-settings-ui.md) para una zona protegida determinada, el perfil usará [prioridad de área de nombres](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) para determinar la identidad principal. En el caso de identityMap, el perfil ya no usará el indicador `primary=true`.
* Aunque el perfil ya no hará referencia a este indicador, es posible que otros servicios de Experience Platform sigan utilizando el indicador `primary=true`.

Para que [eventos de usuario autenticados](implementation-guide.md#ingest-your-data) se vinculen al área de nombres de persona, todos los eventos autenticados deben contener el área de nombres de persona (CRMID). Esto significa que, incluso después de que un usuario inicie sesión, el área de nombres de persona debe estar presente en cada evento autenticado.

Puede seguir viendo el indicador &quot;eventos&quot; de `primary=true` al buscar un perfil en el visor de perfiles. Sin embargo, se ignora y el perfil no lo utiliza.

Los AAID están bloqueados de forma predeterminada. Por lo tanto, si está usando el [conector de origen de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md), debe asegurarse de que ECID tenga una prioridad mayor que ECID para que los eventos no autenticados tengan una identidad principal de ECID.

**Pasos para solucionar problemas**

1. Para validar que los eventos autenticados contienen el área de nombres de persona y de cookie, lea los pasos descritos en la sección sobre [solución de errores relacionados con los datos que no se están ingiriendo en el servicio de identidad](#my-identities-are-not-getting-ingested-into-identity-service).
2. Para validar que los eventos autenticados tienen la identidad principal del área de nombres de persona (por ejemplo, CRMID), busque el área de nombres de persona en el visor de perfiles mediante una política de combinación sin unión (esta es la política de combinación que no utiliza gráficos privados). Esta búsqueda solo devolverá eventos asociados al área de nombres de persona.

### Mis fragmentos de eventos de experiencia no se están ingiriendo en el perfil {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Existen varias razones que explican por qué los fragmentos de eventos de experiencia no se incorporan en el perfil, entre ellas, las siguientes:

* [El conjunto de datos no está habilitado para el perfil](../../catalog/datasets/enable-for-profile.md).
* [Es posible que se haya producido un error de validación en el perfil](../../xdm/classes/experienceevent.md).
   * Por ejemplo, un evento de experiencia debe contener un `_id` y un `timestamp`.
   * Además, `_id` debe ser único para cada evento (registro).

En el contexto de la prioridad de área de nombres, el perfil rechazará cualquier evento que contenga dos o más identidades con la prioridad de área de nombres más alta. Por ejemplo, si GAID no está marcado como un área de nombres única y llegaron dos identidades con un área de nombres GAID y valores de identidad diferentes, Profile no almacenará ninguno de los eventos.

**Pasos para solucionar problemas**

Si los datos se envían al lago de datos, pero no al perfil, y cree que esto se debe a enviar dos o más identidades con la prioridad de área de nombres más alta en un solo evento, puede ejecutar la siguiente consulta para validar que hay dos valores de identidad diferentes enviados con el mismo área de nombres:

>[!TIP]
>
>En las siguientes consultas, debe:
>
>* Reemplace `_testimsorg.identification.core.email` por la ruta de acceso que envía la identidad.
>* Reemplazar `Email` por el área de nombres con la prioridad más alta. Este es el mismo área de nombres que no se está ingiriendo.
>* Reemplace `dataset_name` por el conjunto de datos que desee consultar.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

Esta consulta supone lo siguiente:

* Se envía una identidad desde el mapa de identidad y otra identidad desde un descriptor de identidad. **NOTA**: en esquemas XDM (Experience Data Model), el descriptor de identidad es el campo marcado como identidad.
* El CRMID se envía mediante identityMap. Si el CRMID se envía como un campo, quite `key='Email'` de la cláusula WHERE.

>[!NOTE]
>
>**En la implementación de WebSDK y la duplicación de ECID**: Si el campo ECID está marcado como identidad (descriptor de identidad) en lugar de identityMap, se genera un segundo ECID en identityMap. Esta duplicación puede evitar que el perfil del cliente en tiempo real almacene eventos anónimos debido a la presencia de dos ECID en un solo evento.

## Problemas relacionados con el comportamiento de gráficos {#graph-behavior-related-issues}

Esta sección describe problemas comunes que pueden surgir con respecto al comportamiento del gráfico de identidad.

### Los ExperienceEvents no autenticados se están adjuntando al perfil autenticado incorrecto

El algoritmo de optimización de identidad respetará [los vínculos establecidos más recientemente y quitará los vínculos más antiguos](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Por lo tanto, es posible que una vez habilitada esta función, los ECID se puedan reasignar (volver a vincular) de una persona a otra. Para comprender el historial de cómo se vincula una identidad a lo largo del tiempo, siga los pasos a continuación:

**Pasos para solucionar problemas**

>[!NOTE]
>
>Los siguientes pasos recuperarán información en los siguientes supuestos:
>
>* Un solo conjunto de datos está en uso (no consultará varios conjuntos de datos).
>
>* Los datos no se eliminan del lago de datos debido a la eliminación por parte de [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) u otros servicios que realizan la eliminación.

En primer lugar, debe recopilar la siguiente información:

1. El símbolo de identidad (namespaceCode) del área de nombres de la cookie (por ejemplo, ECID) y el área de nombres de la persona (por ejemplo, CRMID) que se enviaron.
1.1. En el caso de las implementaciones de Web SDK, estas suelen ser las áreas de nombres incluidas en el identityMap.
1.2. Para implementaciones de conector de origen de Analytics, estos son el identificador de cookie incluido en el identityMap. El identificador de persona es un campo de eVar marcado como identidad.
2. El conjunto de datos en el que se envió el evento (dataset_name).
3. El valor de identidad del área de nombres de la cookie que se va a buscar (identity_value).

Los símbolos de identidad (namespaceCode) distinguen entre mayúsculas y minúsculas. Para recuperar todos los símbolos de identidad de un conjunto de datos determinado en el identityMap, ejecute la siguiente consulta:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Si no conoce el valor de identidad del identificador de cookie y desea buscar un ID de cookie que se hubiera vinculado a varios identificadores de persona, debe ejecutar la siguiente consulta. Esta consulta supone que ECID es el área de nombres de la cookie y CRMID es el área de nombres de la persona.

>[!BEGINTABS]

>[!TAB Implementación de Web SDK]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implementación del conector de origen de Analytics]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Nota:** personID hace referencia a la ruta del descriptor. Puede encontrar esta información en esquemas.

>[!ENDTABS]

Ahora que ha identificado los valores de las cookies vinculados a varios ID de persona, tome uno de los resultados y utilícelo en la siguiente consulta para obtener una vista cronológica de cuándo ese valor de cookie se vinculó a un identificador de persona diferente:

>[!BEGINTABS]

>[!TAB Implementación de Web SDK]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implementación del conector de origen de Analytics]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Nota**: En este ejemplo se supone que `eVar10` está marcado como identidad. Para las configuraciones, debe cambiar eVar en función de la implementación de su propia organización.

>[!ENDTABS]

### El algoritmo de optimización de identidad no funciona como se esperaba

**Pasos para solucionar problemas**

Consulte la documentación sobre [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md), así como los tipos de estructuras de gráficos admitidos.

* Lea la [guía de configuración de gráficos](./example-configurations.md) para ver ejemplos de estructuras de gráficos compatibles.
* También puede leer la [guía de implementación](./implementation-guide.md#appendix) para ver ejemplos de estructuras de gráficos no admitidas. Hay dos escenarios que podrían ocurrir:
   * No hay un área de nombres única en todos los perfiles.
   * Se produce un escenario [&quot;colgando ID&quot;](./implementation-guide.md#dangling-loginid-scenario). En esta situación, el servicio de identidad no puede determinar si el ID colgado está asociado con ninguna de las entidades de persona de los gráficos.

También puede usar la [herramienta de simulación de gráficos de la interfaz de usuario](./graph-simulation.md) para simular eventos y configurar su propia configuración de área de nombres y prioridad de área de nombres únicas. Hacerlo puede ayudarle a obtener una comprensión básica del comportamiento del algoritmo de optimización de identidad.

Si los resultados de la simulación coinciden con las expectativas de comportamiento del gráfico, puede comprobar si la [configuración de identidad](./identity-settings-ui.md) coincide con la configuración de la simulación.

### Todavía veo gráficos contraídos en mi zona protegida incluso después de configurar la identidad

Los gráficos de identidad se ajustarán al área de nombres única configurada y a la prioridad de área de nombres _después_ de guardar la configuración. Cualquier gráfico &quot;contraído&quot; que exista _antes de_ que guarde su nueva configuración no se verá afectado, hasta que se incorporen nuevos datos de manera que se actualice el gráfico contraído. La identidad principal de los fragmentos de evento en el Perfil del cliente en tiempo real no se actualizará incluso después de que cambie la prioridad del área de nombres.

**Pasos para solucionar problemas**

Puede usar el [visualizador de gráficos de identidad](../features/identity-graph-viewer.md) para comprobar si el gráfico se ha introducido antes o después de la configuración. Examine la última marca de tiempo actualizada en [!UICONTROL Propiedades del vínculo] para ver cuándo el servicio de identidad ingirió el gráfico. Si la marca de tiempo es anterior a la configuración, eso sugiere que el gráfico &quot;contraído&quot; se creó antes de habilitar la función.

![Visor de gráficos de identidad con un gráfico de ejemplo.](../images/troubleshooting/graph_viewer.png)

### Quiero saber cuántos gráficos &quot;colapsados&quot; existen en mi zona protegida

Utilice el panel de identidad para obtener información sobre el estado del gráfico de identidad, como el recuento de identidades y gráficos. Consulte la métrica &quot;Recuento de gráficos con varias áreas de nombres&quot; para ver un recuento de gráficos que se han contraído: son gráficos que contienen dos o más identidades con el mismo área de nombres. Suponiendo que la zona protegida no tenga datos y que haya configurado un área de nombres (por ejemplo, CRMID) para que sea única, se espera que no haya gráficos que tengan dos o más CRMID. En el ejemplo siguiente, hay dos gráficos que contienen dos o más direcciones de correo electrónico.

![El tablero de identidad con métricas sobre el recuento de identidades, el recuento de gráficos, el recuento por área de nombres, el recuento de gráficos por tamaño y el recuento de gráficos de más de dos áreas de nombres.](../images/troubleshooting/identity_dashboard.png)

Puede encontrar un desglose detallado en el [conjunto de datos de exportación de instantáneas de perfil](../../dashboards/query.md) en el lago de datos ejecutando la siguiente consulta:

>[!NOTE]
>
>* Reemplace `dataset_name` con el nombre real de su conjunto de datos.
>
>* Es posible que los recuentos no coincidan exactamente. El panel de identidad se basa en el recuento del gráfico de identidad y la siguiente consulta se basa en el recuento de perfiles con dos o más identidades. El servicio procesa y actualiza los datos de forma independiente.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Puede utilizar la siguiente consulta en el conjunto de datos de exportación de instantáneas de perfil para obtener identidades de muestra de gráficos &quot;contraídos&quot;.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>Las dos consultas enumeradas anteriormente arrojarán los resultados esperados si la zona protegida no está habilitada para el método provisional de dispositivos compartidos y se comportarán de forma diferente a [!DNL Identity Graph Linking Rules].

## Preguntas frecuentes {#faq}

En esta sección se describe una lista de respuestas a las preguntas más frecuentes acerca de [!DNL Identity Graph Linking Rules].

## Algoritmo de optimización de identidad {#identity-optimization-algorithm}

Lea esta sección para obtener respuestas a las preguntas frecuentes acerca del [algoritmo de optimización de identidad](./identity-optimization-algorithm.md).

### Tengo un CRMID para cada una de mis unidades de negocio (B2C CRMID, B2B CRMID), pero no tengo un área de nombres única en todos mis perfiles. ¿Qué sucederá si marco B2C CRMID y B2B CRMID como únicos y habilito mi configuración de identidad?

Este escenario no es compatible. Por lo tanto, es posible que vea que los gráficos se contraen cuando un usuario utiliza su CRMID B2C para iniciar sesión y otro usuario utiliza su CRMID B2B para iniciar sesión. Para obtener más información, lea la sección sobre [requisito del área de nombres de una sola persona](./implementation-guide.md#single-person-namespace-requirement) en la página de implementación.

### ¿El algoritmo de optimización de identidad &quot;corrige&quot; los gráficos contraídos existentes?

Los gráficos contraídos existentes solo se verán afectados (&quot;corregidos&quot;) por el algoritmo de gráficos si estos gráficos se actualizan después de guardar la nueva configuración.

### Si dos personas inician y finalizan sesión con el mismo dispositivo, ¿qué sucede con los eventos? ¿Se transferirán todos los eventos al último usuario autenticado?

* Los eventos anónimos (eventos con ECID como identidad principal en el Perfil del cliente en tiempo real) se transferirán al último usuario autenticado. Esto se debe a que el ECID se vinculará al CRMID del último usuario autenticado (en el servicio de identidad).
* Todos los eventos autenticados (eventos con CRMID definidos como identidad principal) permanecerán con la persona.

Para obtener más información, lea la guía sobre [determinar la identidad principal para los eventos de experiencia](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events).

### ¿Cómo se verán afectados los recorridos en Adobe Journey Optimizer cuando el ECID se transfiera de una persona a otra?

El CRMID del último usuario autenticado se vinculará al ECID (dispositivo compartido). Los ECID se pueden reasignar de una persona a otra según el comportamiento del usuario. El impacto dependerá de cómo se construya la recorrido, por lo que es importante que los clientes prueben la recorrido en un entorno de zona protegida de desarrollo para validarla.

Los puntos clave a destacar son los siguientes:

* Una vez que un perfil introduce un recorrido, la reasignación de ECID no provoca que el perfil se cierre en mitad de un recorrido.
   * Las salidas de recorrido no se activan mediante cambios de gráfico.
* Si un perfil ya no está asociado a un ECID, esto puede provocar un cambio en la ruta de recorrido si hay una condición que utilice la calificación de audiencia.
   * La eliminación de ECID puede cambiar los eventos asociados a un perfil, lo que podría provocar cambios en la calificación de la audiencia.
* La reentrada de un recorrido depende de las propiedades del recorrido.
   * Si desactiva la reentrada de un recorrido, una vez que un perfil sale de ese recorrido, el mismo perfil no se vuelve a introducir durante 91 días (según el tiempo de espera de recorrido global).
* Si un recorrido comienza con un área de nombres de ECID, el perfil que introduce y el perfil que recibe la acción (por ejemplo, correo electrónico, oferta) pueden variar según el diseño del recorrido.
   * Por ejemplo, si hay una condición de espera entre las acciones y el ECID se transfiere durante el período de espera, se puede establecer un perfil diferente.
   * Con esta función, los ECID ya no siempre se asocian a un perfil.
   * Se recomienda iniciar recorridos con áreas de nombres de persona (CRMID).

>[!TIP]
>
>Los recorridos deben buscar un perfil con áreas de nombres únicas porque es posible que se vuelva a asignar un área de nombres no única a otro usuario.
>
>* Los ECID y los áreas de nombres de correo electrónico/teléfono no únicos podrían moverse de una persona a otra.
>* Si un recorrido tiene una condición de espera y si estas áreas de nombres no únicas se utilizan para buscar un perfil en un recorrido, el mensaje de recorrido se puede enviar a la persona incorrecta.

## Prioridad del área de nombres

Lea esta sección para obtener respuestas a las preguntas más frecuentes acerca de [prioridad del área de nombres](./namespace-priority.md).

### He habilitado mi configuración de identidad. ¿Qué sucede con mi configuración si deseo agregar un área de nombres personalizada después de habilitar la configuración?

Hay dos &quot;bloques&quot; de áreas de nombres: áreas de nombres de persona y áreas de nombres de dispositivo/cookie. El área de nombres personalizada recién creada tendrá la prioridad más baja en cada &quot;bloque&quot; para que este nuevo área de nombres personalizada no afecte a la ingesta de datos existente.

### Si el perfil del cliente en tiempo real ya no utiliza el indicador &quot;principal&quot; en identityMap, ¿sigue siendo necesario enviar este valor?

Sí, otros servicios utilizan el indicador &quot;principal&quot; en identityMap. Para obtener más información, lea la guía sobre [las implicaciones de la prioridad del área de nombres en otros servicios de Experience Platform](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services).

### ¿Se aplicará la prioridad de área de nombres a los conjuntos de datos de registro de perfil en el Perfil del cliente en tiempo real?

No. La prioridad de área de nombres solo se aplicará a los conjuntos de datos de Experience Event que utilicen la clase XDM ExperienceEvent.

### ¿Cómo funciona esta función en conjunto con las protecciones del gráfico de identidad de 50 identidades por gráfico? ¿Afecta la prioridad de área de nombres a esta protección definida por el sistema?

El algoritmo de optimización de identidad se aplicará primero para garantizar la representación de la entidad de la persona. Después, si el gráfico intenta superar la [protección del gráfico de identidad](../guardrails.md) (50 identidades por gráfico), se aplicará esta lógica. La prioridad del área de nombres no afecta a la lógica de eliminación de la protección de 50 identidades/gráficos.

## Pruebas

Lea esta sección para obtener respuestas a las preguntas más frecuentes acerca de las características de prueba y depuración de [!DNL Identity Graph Linking Rules].

### ¿Cuáles son algunos de los escenarios que debería probar en un entorno de zona protegida de desarrollo?

En términos generales, las pruebas en una zona protegida de desarrollo deben imitar los casos de uso que tiene intención de ejecutar en la zona protegida de producción. Consulte la siguiente tabla para conocer algunas áreas clave que se deben validar al realizar pruebas exhaustivas:

| Caso de prueba | Pasos de prueba | Resultado esperado |
| --- | --- | --- |
| Representación precisa de la entidad de persona | <ul><li>Imitar la exploración anónima</li><li>Imita el inicio de sesión de dos personas (John, Jane) utilizando el mismo dispositivo</li></ul> | <ul><li>Tanto John como Jane deben asociarse a sus atributos y eventos autenticados.</li><li>El último usuario autenticado debe estar asociado a los eventos de navegación anónimos.</li></ul> |
| Segmentación | Crear cuatro definiciones de segmento (**NOTA**: Cada par de definiciones de segmento debe tener una evaluada mediante un lote y otra de flujo continuo.) <ul><li>Definición del segmento A: Calificación de segmentos basada en los eventos autenticados o atributos de John.</li><li>Definición del segmento B: Calificación de segmentos basada en los eventos autenticados o atributos de Jane.</li></ul> | Independientemente de los escenarios de dispositivos compartidos, John y Jane siempre deben cumplir los requisitos para sus respectivos segmentos. |
| Calificación de audiencias / recorridos unitarios en Adobe Journey Optimizer | <ul><li>Cree un recorrido que comience con una actividad de calificación de audiencia (como la segmentación de streaming creada anteriormente).</li><li>Cree un recorrido que comience con un evento unitario. Este evento unitario debe ser un evento autenticado.</li><li>Debe deshabilitar la reentrada al crear estos recorridos.</li></ul> | <ul><li>Independientemente de los escenarios de dispositivos compartidos, John y Jane deben almacenar en déclencheur los recorridos respectivos que deben introducir.</li><li>John y Jane no deben volver a entrar en el recorrido cuando se les transfiera el ECID.</li></ul> |

{style="table-layout:auto"}

### ¿Cómo valido que esta función funciona según lo esperado?

Use la [herramienta de simulación de gráficos](./graph-simulation.md) para comprobar que la característica funciona a nivel de gráfico individual.

Para validar la característica en un nivel de zona protegida, consulte la sección [!UICONTROL Recuento de gráficos con varias áreas de nombres] en el panel de identidad.