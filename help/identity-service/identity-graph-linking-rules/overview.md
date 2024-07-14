---
title: Resumen de reglas de vinculación de gráficos de identidad
description: Obtenga información acerca de las reglas de vinculación de gráficos de identidad en Identity Service.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 1%

---

# Resumen de reglas de vinculación de gráficos de identidad

>[!AVAILABILITY]
>
>Esta función aún no está disponible; se espera que el programa beta para reglas de vinculación de gráficos de identidad comience en julio en zonas protegidas de desarrollo. Póngase en contacto con el equipo de su cuenta de Adobe para obtener información sobre los criterios de participación.

## Índice 

* [Información general](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Casos de ejemplo](./example-scenarios.md)

Con el servicio de identidad de Adobe Experience Platform y el perfil del cliente en tiempo real, es fácil suponer que los datos se incorporan perfectamente y que todos los perfiles combinados representan a una sola persona individual a través de un identificador de persona, como un ID de CRM. Sin embargo, hay escenarios posibles en los que ciertos datos podrían intentar combinar varios perfiles dispares en un único perfil (&quot;colapso de gráfico&quot;). Para evitar estas combinaciones no deseadas, puede utilizar las configuraciones proporcionadas mediante reglas de vinculación de gráficos de identidad y permitir una personalización precisa para los usuarios.

## Casos de ejemplo en los que podría producirse un colapso de gráfico

* **Dispositivo compartido**: El dispositivo compartido hace referencia a dispositivos que utilizan más de un individuo. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos.
* **Correo electrónico y números de teléfono incorrectos**: Los números de correo electrónico y de teléfono incorrectos hacen referencia a usuarios finales que registran información de contacto no válida, como &quot;test<span>@test.com&quot; para correo electrónico y &quot;+1-111-111-1111&quot; para número de teléfono.
* **Valores de identidad erróneos o incorrectos**: Los valores de identidad erróneos o incorrectos hacen referencia a valores de identidad no únicos que podrían combinar ID de CRM. Por ejemplo, aunque los IDFA deben tener 36 caracteres (32 caracteres alfanuméricos y cuatro guiones), hay escenarios en los que se puede introducir un IDFA con un valor de identidad &quot;user_null&quot;. Del mismo modo, los números de teléfono solo admiten caracteres numéricos, pero se puede introducir un área de nombres de teléfono con un valor de identidad &quot;no especificado&quot;.

Para obtener más información sobre los casos de uso de las reglas de vinculación de gráficos de identidad, lea el documento [ejemplos](./example-scenarios.md).

## Reglas de vinculación de gráfico de identidad {#identity-graph-linking-rules}

Con las reglas de vinculación de gráficos de identidad puede:

* Cree un único gráfico de identidad o perfil combinado para cada usuario configurando áreas de nombres únicas, lo que evitará que dos identificadores de persona diferentes se combinen en un gráfico de identidad.
* Asociar eventos autenticados en línea a la persona configurando prioridades

### Terminología {#terminology}

| Terminología | Descripción |
| --- | --- |
| Área de nombres única | Un área de nombres única es un área de nombres de identidad que se ha configurado para que sea distinta en el contexto de un gráfico de identidades. Puede configurar un área de nombres para que sea única mediante la interfaz de usuario. Una vez que un área de nombres se define como única, un gráfico solo puede tener una identidad que contenga ese área de nombres. |
| Prioridad de área de nombres | La prioridad del área de nombres hace referencia a la importancia relativa de las áreas de nombres en comparación con otras. La prioridad del área de nombres se puede configurar a través de la IU. Puede clasificar las áreas de nombres en un gráfico de identidad determinado. Una vez habilitada, la prioridad de los nombres se utilizará en varios escenarios, como la entrada para el algoritmo de optimización de identidades y la determinación de la identidad principal para los fragmentos de eventos de experiencia. |
| Algoritmo de optimización de identidad | El algoritmo de optimización de identidad garantiza que las directrices creadas al configurar un área de nombres única y las prioridades de área de nombres se apliquen en un gráfico de identidad determinado. |

### Área de nombres única {#unique-namespace}

Puede configurar un área de nombres para que sea única mediante el área de trabajo de IU de configuración de identidad. Al hacerlo, informa al algoritmo de optimización de identidad de que un gráfico determinado solo puede tener una identidad que contenga ese área de nombres única. Esto evita la combinación de dos identificadores de persona dispares dentro del mismo gráfico.

Considere el siguiente escenario:

* Scott usa una tableta y abre su navegador Google Chrome para ir a nike<span>.com, donde inicia sesión y busca nuevos zapatos de baloncesto.
   * En segundo plano, este escenario registra las siguientes identidades:
      * Un área de nombres y valor ECID para representar el uso del explorador
      * Un área de nombres y valor de ID de CRM para representar al usuario autenticado (Scott inició sesión con su nombre de usuario y contraseña combinados).
* A continuación, su hijo Peter usa la misma tableta y también usa Google Chrome para ir a nike<span>.com, donde inicia sesión con su propia cuenta para buscar equipos de fútbol.
   * En segundo plano, este escenario registra las siguientes identidades:
      * El mismo espacio de nombres y valor de ECID para representar el explorador.
      * Un nuevo área de nombres y valor de ID de CRM para representar al usuario autenticado.

Si CRM ID se configuró como un área de nombres única, el algoritmo de optimización de identidad divide los CRM ID en dos gráficos de identidad independientes, en lugar de combinarlos juntos.

Si no configura un área de nombres única, puede terminar con combinaciones de gráficos no deseadas, como dos identidades con el mismo área de nombres de ID de CRM, pero con valores de identidad diferentes (escenarios como estos suelen representar dos entidades de persona diferentes en el mismo gráfico).

Debe configurar un área de nombres única para informar al algoritmo de optimización de identidad a fin de aplicar limitaciones a los datos de identidad que se incorporan en un gráfico de identidad determinado.

### Prioridad de área de nombres {#namespace-priority}

La prioridad del área de nombres hace referencia a la importancia relativa de las áreas de nombres en comparación con otras. La prioridad del área de nombres se puede configurar a través de la interfaz de usuario y puede clasificar las áreas de nombres en un gráfico de identidad determinado.

Una forma en que se utiliza la prioridad del área de nombres es determinar la identidad principal de los fragmentos de evento de experiencia (comportamiento del usuario) en el Perfil del cliente en tiempo real. Si se establece la configuración de prioridad, ya no se utilizará la configuración de identidad principal del SDK web para determinar qué fragmentos de perfil se almacenan.

Las áreas de nombres únicas y las prioridades de área de nombres se pueden configurar en el área de trabajo de IU de configuración de identidad. Sin embargo, los efectos de sus configuraciones son diferentes:

| | Servicio de identidad | Perfil del cliente en tiempo real |
| --- | --- | --- |
| Área de nombres única | En el servicio de identidad, el algoritmo de optimización de identidad hace referencia a áreas de nombres únicas para determinar los datos de identidad que se incorporan a un gráfico de identidad determinado. | Las áreas de nombres únicas no afectan al perfil del cliente en tiempo real. |
| Prioridad de área de nombres | En el servicio de identidad, para los gráficos que tienen varias capas, la prioridad del área de nombres determinará que se eliminen los vínculos adecuados. | Cuando se incorpora un evento de experiencia en el perfil, el área de nombres con la prioridad más alta se convierte en la identidad principal del fragmento de perfil. |

* La prioridad del área de nombres no afecta al comportamiento del gráfico cuando se alcanza el límite de 50 identidades por gráfico.
* **La prioridad del área de nombres es un valor numérico** asignado a un área de nombres que indica su importancia relativa. Es una propiedad de un área de nombres.
* **La identidad principal es la identidad con la que se almacena un fragmento de perfil en relación con**. Un fragmento de perfil es un registro de datos que almacena información sobre un usuario determinado: atributos (normalmente incorporados mediante registros CRM) o eventos (normalmente incorporados a partir de eventos de experiencia o datos en línea).
* La prioridad del área de nombres determina la identidad principal de los fragmentos de eventos de experiencia.
   * Para los registros de perfil, puede utilizar el espacio de trabajo de esquemas de la interfaz de usuario de Experience Platform para definir campos de identidad, incluida la identidad principal. Lea la guía [definición de campos de identidad en la interfaz de usuario](../../xdm/ui/fields/identity.md) para obtener más información.
* Si un evento de experiencia tiene dos o más identidades de la prioridad de área de nombres más alta en el identityMap, se rechazará la ingesta porque se considerará como &quot;datos incorrectos&quot;. Por ejemplo, si identityMap contiene `{ECID: 111, CRMID: John, CRMID: Jane}`, todo el evento se rechazará como datos incorrectos porque implica que el evento está asociado simultáneamente a `CRMID: John` y a `CRMID: Jane`.

Para obtener más información, lea la guía sobre [prioridad del área de nombres](./namespace-priority.md).

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [algoritmo de optimización de identidad](./identity-optimization-algorithm.md).
* [Prioridad de área de nombres](./namespace-priority.md).
* [Ejemplos de escenarios para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md).
