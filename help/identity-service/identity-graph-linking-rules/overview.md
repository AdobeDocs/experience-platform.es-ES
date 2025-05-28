---
title: Reglas de vinculación de gráfico de identidad
description: Obtenga información acerca de las reglas de vinculación de gráficos de identidad en Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 38d331bd9265f25a3aebdcbd20ae5fc30a93e960
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 7%

---

# Información general de [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Reglas de vinculación de gráficos de identidad"
>abstract="Para evitar estas combinaciones no deseadas, puede utilizar las configuraciones proporcionadas mediante Reglas de vinculación de gráficos de identidad y permitir una personalización precisa para los usuarios."

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules] ya está disponible de forma general. Póngase en contacto con el equipo de cuenta de Adobe o con el servicio de asistencia de Adobe si tiene una zona protegida existente que requiera que los gráficos contraídos se cancelen (&quot;fijos&quot;) después de habilitar la configuración de identidad.

Con el servicio de identidad de Adobe Experience Platform y el perfil del cliente en tiempo real, es fácil suponer que los datos se incorporan perfectamente y que todos los perfiles combinados representan a una sola persona a través de un identificador de persona, como un CRMID. Sin embargo, hay escenarios posibles en los que ciertos datos podrían intentar combinar varios perfiles dispares en un único perfil (&quot;colapso de gráfico&quot;). Para evitar estas combinaciones no deseadas, puede usar las configuraciones proporcionadas mediante [!DNL Identity Graph Linking Rules] y permitir una personalización precisa para los usuarios.

## Introducción 

Los siguientes documentos son esenciales para comprender [!DNL Identity Graph Linking Rules].

* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Resolución de problemas y preguntas frecuentes](./troubleshooting.md)
* [Prioridad del área de nombres](./namespace-priority.md)
* [IU de simulación de gráficos](./graph-simulation.md)
* [IU de configuración de identidad](./identity-settings-ui.md)

## Biblioteca de vídeos

Vea los siguientes vídeos para conocer algunos de los aspectos fundamentales de las reglas de vinculación de gráficos de identidad.

<!-- CARDS
{target = _blank}
* https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/overview
* https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation 

    {description = Learn how to use the graph simulator to test out identity graph linking rules.}

* https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings
    {description = Learn how to enable and configure identity graph linking rules to build accurate customer profiles}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" title="Información general sobre las reglas de vinculación de gráficos de identidad" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3448275/?format=jpeg&nocache=1747851655227&captions=spa" alt="Información general sobre las reglas de vinculación de gráficos de identidad"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" title="Información general sobre las reglas de vinculación de gráficos de identidad">Introducción a las reglas de vinculación de gráficos de identidad</a>
                    </p>
                    <p class="is-size-6">Obtenga información general sobre cómo las reglas de vinculación de gráficos de identidad ayudan a los arquitectos de datos a mantener perfiles de clientes precisos y a evitar el colapso del gráfico.</p>
                </div>
                <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ver</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Graph Simulation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" title="Reglas de vinculación de gráficos de identidad: simulación de gráficos" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3444046/?format=jpeg&nocache=1747851655237&captions=spa" alt="Reglas de vinculación de gráficos de identidad: simulación de gráficos"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" title="Reglas de vinculación de gráficos de identidad: simulación de gráficos">Reglas de vinculación de gráficos de identidad: simulación de gráficos</a>
                    </p>
                    <p class="is-size-6">Aprenda a utilizar el simulador de gráficos para probar las reglas de vinculación de gráficos de identidad.</p>
                </div>
                <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ver</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Identity settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" title="Reglas de vinculación de gráficos de identidad: configuración de identidad" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3458487/?format=jpeg&nocache=1747851655218" alt="Reglas de vinculación de gráficos de identidad: configuración de identidad"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" title="Reglas de vinculación de gráficos de identidad: configuración de identidad">Reglas de vinculación de gráficos de identidad: configuración de identidad</a>
                    </p>
                    <p class="is-size-6">Obtenga información sobre cómo habilitar y configurar reglas de vinculación de gráficos de identidad para crear perfiles de cliente precisos</p>
                </div>
                <a href="https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ver</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


## Contraer escenarios de gráfico {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Contraer escenarios de gráfico"
>abstract="Existen varias razones por las que los gráficos pueden &quot;contraerse&quot; o representar entidades de varias personas."

Esta sección describe los escenarios de ejemplo que puede considerar al configurar [!DNL Identity Graph Linking Rules].

### Dispositivo compartido

Hay casos en los que se pueden producir varios inicios de sesión en un solo dispositivo:

| Dispositivo compartido | Descripción |
| --- | --- |
| Ordenadores familiares y tabletas | El marido y la mujer inician sesión en sus respectivas cuentas bancarias. |
| Quiosco público | Viajeros en un aeropuerto que inician sesión con su ID de fidelidad para facturar maletas e imprimir tarjetas de embarque. |
| Centro de llamadas | El personal del centro de llamadas inicia sesión en un solo dispositivo en nombre de los clientes que llaman al servicio de atención al cliente para resolver problemas. |

![Diagrama de algunos dispositivos compartidos comunes.](../images/identity-settings/shared-devices.png "Diagrama de algunos dispositivos compartidos comunes."){zoomable="yes"}

En estos casos, desde un punto de vista gráfico, sin límites habilitados, un solo ECID se vinculará a varios CRMID.

Con [!DNL Identity Graph Linking Rules], puede:

* Configure el ID utilizado para iniciar sesión como identificador único. Por ejemplo, puede limitar un gráfico para almacenar solo una identidad con un área de nombres CRMID y, por lo tanto, definir ese CRMID como el identificador único de un dispositivo compartido.
   * Al hacer esto, puede asegurarse de que los CRMID no se fusionen con el ECID.

### Escenarios de correo electrónico/teléfono no válidos

También hay casos de usuarios que proporcionan valores falsos como números de teléfono o direcciones de correo electrónico al registrarse. En estos casos, si los límites no están habilitados, las identidades relacionadas con el teléfono/correo electrónico terminarán vinculándose a varios CRMID diferentes.

![Diagrama que representa situaciones de correo electrónico o teléfono no válidas.](../images/identity-settings/invalid-email-phone.png "Diagrama que representa situaciones de correo electrónico o teléfono no válidas."){zoomable="yes"}

Con [!DNL Identity Graph Linking Rules], puede:

* Configure el CRMID, el número de teléfono o la dirección de correo electrónico como identificador único y, por lo tanto, limite una persona a un solo CRMID, número de teléfono o dirección de correo electrónico asociados a su cuenta.

### Valores de identidad erróneos o incorrectos

Hay casos en los que se incorporan valores de identidad erróneos y no únicos en el sistema, independientemente del área de nombres. Algunos ejemplos son:

* Área de nombres IDFA con el valor de identidad &quot;user_null&quot;.
   * Los valores de identidad IDFA deben tener 36 caracteres: 32 caracteres alfanuméricos y cuatro guiones.
* Área de nombres del número de teléfono con el valor de identidad &quot;no especificado&quot;.
   * Los números de teléfono no deben contener caracteres alfabéticos.

Estas identidades podrían resultar en los siguientes gráficos, donde varios CRMID se combinan con la identidad &quot;mala&quot;:

![Ejemplo gráfico de datos de identidad con valores de identidad erróneos o incorrectos.](../images/identity-settings/bad-data.png "Ejemplo gráfico de datos de identidad con valores de identidad erróneos o incorrectos."){zoomable="yes"}

Con [!DNL Identity Graph Linking Rules] puede configurar el CRMID como identificador único para evitar que el perfil no deseado se contraiga debido a este tipo de datos.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

Con [!DNL Identity Graph Linking Rules] puede:

* Cree un único gráfico de identidad o perfil combinado para cada usuario configurando áreas de nombres únicas, lo que evitará que dos identificadores de persona diferentes se combinen en un gráfico de identidad.
* Asociar eventos autenticados en línea a la persona configurando prioridades

### Terminología {#terminology}

| Terminología | Descripción |
| --- | --- |
| Área de nombres única | Un área de nombres única es un área de nombres de identidad que se ha configurado para que sea distinta en el contexto de un gráfico de identidades. Puede configurar un área de nombres para que sea única mediante la interfaz de usuario. Una vez que un área de nombres se define como única, un gráfico solo puede tener una identidad que contenga ese área de nombres. |
| Prioridad del área de nombres | La prioridad del área de nombres hace referencia a la importancia relativa de las áreas de nombres en comparación con otras. La prioridad del área de nombres se puede configurar a través de la IU. Puede clasificar las áreas de nombres en un gráfico de identidad determinado. Una vez habilitada, la prioridad de los nombres se utilizará en varios casos, como la entrada para el algoritmo de optimización de identidad y la determinación de la identidad principal para los fragmentos de evento de experiencia. |
| Algoritmo de optimización de identidad | El algoritmo de optimización de identidad garantiza que las directrices creadas configurando un área de nombres única y las prioridades de área de nombres se apliquen en un gráfico de identidad determinado. |

### Área de nombres única {#unique-namespace}

Puede configurar un área de nombres para que sea única mediante el área de trabajo de IU de configuración de identidad. Al hacerlo, informa al algoritmo de optimización de identidad de que un gráfico determinado solo puede tener una identidad que contenga ese área de nombres única. Esto evita la combinación de dos identificadores de persona dispares dentro del mismo gráfico.

Considere el siguiente escenario:

* Scott usa una tableta y abre su explorador Google Chrome para ir a acme<span>.com, donde inicia sesión y busca nuevos zapatos de baloncesto.
   * En segundo plano, este escenario registra las siguientes identidades:
      * Un área de nombres y valor ECID para representar el uso del explorador
      * Un área de nombres CRMID y un valor para representar al usuario autenticado (Scott inició sesión con su nombre de usuario y contraseña combinados).
* A continuación, su hijo Peter usa la misma tableta y también usa Google Chrome para ir a acme<span>.com, donde inicia sesión con su propia cuenta para buscar equipos de fútbol.
   * En segundo plano, este escenario registra las siguientes identidades:
      * El mismo espacio de nombres y valor de ECID para representar el explorador.
      * Un nuevo espacio de nombres CRMID y valor para representar al usuario autenticado.

Si CRMID se configuró como un área de nombres única, el algoritmo de optimización de identidad divide los CRMID en dos gráficos de identidad independientes, en lugar de combinarlos.

Si no configura un área de nombres única, puede terminar con combinaciones de gráficos no deseadas, como dos identidades con el mismo área de nombres CRMID, pero con valores de identidad diferentes (escenarios como estos suelen representar dos entidades de persona diferentes en el mismo gráfico).

Debe configurar un área de nombres única para informar al algoritmo de optimización de identidad a fin de aplicar limitaciones a los datos de identidad que se incorporan en un gráfico de identidad determinado.

### Prioridad del área de nombres {#namespace-priority}

La prioridad del área de nombres hace referencia a la importancia relativa de las áreas de nombres en comparación con otras. La prioridad del área de nombres se puede configurar a través de la interfaz de usuario y puede clasificar las áreas de nombres en un gráfico de identidad determinado.

Una forma en que se utiliza la prioridad del área de nombres es determinar la identidad principal de los fragmentos de evento de experiencia (comportamiento del usuario) en el Perfil del cliente en tiempo real. Si se establece la configuración de prioridad, la configuración de identidad principal de Web SDK ya no se utilizará para determinar qué fragmentos de perfil se almacenan.

Las áreas de nombres únicas y las prioridades de área de nombres se pueden configurar en el área de trabajo de IU de configuración de identidad. Sin embargo, los efectos de sus configuraciones son diferentes:

| | Servicio de identidad | Perfil del cliente en tiempo real |
| --- | --- | --- |
| Área de nombres única | En el servicio de identidad, el algoritmo de optimización de identidad hace referencia a áreas de nombres únicas para determinar los datos de identidad que se incorporan a un gráfico de identidad determinado. | Las áreas de nombres únicas no afectan al perfil del cliente en tiempo real. |
| Prioridad del área de nombres | En el servicio de identidad, para los gráficos que tienen varias capas, la prioridad del área de nombres determinará que se eliminen los vínculos adecuados. | Cuando se incorpora un evento de experiencia en el perfil, el área de nombres con la prioridad más alta se convierte en la identidad principal del fragmento de perfil. |

* La prioridad del área de nombres no afecta al comportamiento del gráfico cuando se alcanza el límite de 50 identidades por gráfico.
* **La prioridad del área de nombres es un valor numérico** asignado a un área de nombres que indica su importancia relativa. Es una propiedad de un área de nombres.
* **La identidad principal es la identidad con la que se almacena un fragmento de perfil en relación con**. Un fragmento de perfil es un registro de datos que almacena información sobre un usuario determinado: atributos (normalmente incorporados mediante registros CRM) o eventos (normalmente incorporados a partir de eventos de experiencia o datos en línea).
* La prioridad del área de nombres determina la identidad principal de los fragmentos de eventos de experiencia.
   * Para los registros de perfil, puede utilizar el espacio de trabajo de esquemas de la interfaz de usuario de Experience Platform para definir campos de identidad, incluida la identidad principal. Lea la guía [definición de campos de identidad en la interfaz de usuario](../../xdm/ui/fields/identity.md) para obtener más información.
* Si un evento de experiencia tiene dos o más identidades de la prioridad de área de nombres más alta en el identityMap, se rechazará la ingesta porque se considerará como &quot;datos incorrectos&quot;. Por ejemplo, si identityMap contiene `{ECID: 111, CRMID: John, CRMID: Jane}`, todo el evento se rechazará como datos incorrectos porque implica que el evento está asociado simultáneamente a `CRMID: John` y a `CRMID: Jane`.

Para obtener más información, lea la guía sobre [prioridad del área de nombres](./namespace-priority.md).

## Pasos siguientes

Para obtener más información sobre [!DNL Identity Graph Linking Rules], lea la siguiente documentación:

* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Resolución de problemas y preguntas frecuentes](./troubleshooting.md)
* [Prioridad del área de nombres](./namespace-priority.md)
* [IU de simulación de gráficos](./graph-simulation.md)
* [IU de configuración de identidad](./identity-settings-ui.md)