---
title: Puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B
type: Documentation
description: Información general y más detalles sobre la función de puntuación de cuenta y posible cliente predictivo de Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B

Los especialistas en marketing B2B se enfrentan a múltiples desafíos en la parte superior del canal de marketing. Para ser eficaces, los especialistas en marketing B2B necesitan una forma automatizada de cualificar al gran número de personas para que puedan centrarse en los objetivos de alto valor. La calificación debe estar alineada con el resultado final de ventas, no solo con la conversión de marketing.

Las cuentas son las entidades finales que adquieren productos y servicios B2B. Para comercializar y vender de forma eficaz, los especialistas en marketing B2B deben conocer no solo la probabilidad de compra de la persona, sino también la de la cuenta.

El marketing basado en cuentas, en particular, estrategiza las cuentas como objetivos de marketing. Las puntuaciones de inclinación a la compra de las cuentas ayudan en gran medida a los especialistas en marketing B2B a priorizar entre las cuentas para maximizar el retorno de la inversión.

El servicio predictivo de puntuación de cuenta y posible cliente aborda los desafíos anteriores aprendiendo y prediciendo los eventos de conversión de la fase de oportunidad, y agregando actividades de persona en el nivel de cuenta para producir las puntuaciones de cuenta. Las puntuaciones están fácilmente disponibles como campos personalizados en perfiles de personas y perfiles de cuenta, y se pueden incluir fácilmente como criterios de segmento para refinar la audiencia. Los principales factores influyentes también están disponibles a nivel agregado y unitario para ayudar a los especialistas en marketing B2B a comprender mejor qué elementos impulsaron las puntuaciones.

## Explicación de la puntuación predictiva de clientes potenciales y cuentas {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] actualmente, se necesita una fuente de datos, ya que es la única fuente de datos que puede proporcionar los eventos de conversión en el nivel de perfil de la persona.

La puntuación predictiva de clientes potenciales y cuentas utiliza un método de aprendizaje automático basado en árbol (aumento aleatorio de bosque/degradado) para crear el modelo de puntuación predictiva de posibles clientes.

Los administradores tienen la capacidad de configurar varios objetivos de puntuación de perfil, también denominados modelos, uno para cada evento de conversión configurado, lo que permite generar puntuaciones independientes para cada objetivo configurado.

La puntuación predictiva de posibles clientes y cuentas admite los siguientes tipos y campos de objetivos de conversión:

| Tipo de meta | Campos |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Ejemplo: `opportunityEvent.dataValueChanges.attributeName` igual a `Stage` y `opportunityEvent.dataValueChanges.newValue` igual a `Contract`</ul> |

El algoritmo tiene en cuenta los siguientes atributos y datos de entrada:

* Perfil de persona

| Campo XDM | Obligatorio/Opcional |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Requerido |
| `workAddress.country` | Opcional |
| `extSourceSystemAudit.createdDate` | Requerido |
| `extendedWorkDetails.jobTitle` | Opcional |

>[!NOTE]
> 
>El algoritmo solo inspecciona `sourceAccountKey.sourceKey` en el grupo de campos Persona:componentePersona.

* Perfil de cuenta

| Campo XDM | Obligatorio/Opcional |
| --- | --- |
| `accountKey.sourceKey` | Requerido |
| `extSourceSystemAudit.createdDate` | Requerido |
| `accountOrganization.industry` | Opcional |
| `accountOrganization.numberOfEmployees` | Opcional |
| `accountOrganization.annualRevenue.amount` | Opcional |

* Evento de experiencia

| Campo XDM | Obligatorio/Opcional |
| --- | --- |
| `_id` | Requerido |
| `personKey.sourceKey` | Requerido |
| `timestamp` | Requerido |
| `eventType` | Requerido |

Se admiten varios modelos, con los siguientes límites estrictos establecidos:

* Cada zona protegida de producción tiene derecho a cinco modelos.
* Cada zona protegida de desarrollo tiene derecho a un modelo.

Los requisitos de calidad de los datos son los siguientes:

* Lo ideal es que haya dos años de datos más recientes con fines de formación.
* La longitud mínima de datos requerida es de seis meses más la ventana de predicción.
* Para cada objetivo de predicción se requieren al menos 10 eventos de conversión calificados.

Los trabajos de puntuación se ejecutan diariamente y los resultados se guardan como atributos de perfil y atributos de cuenta, que luego se pueden utilizar en definiciones de segmentos y personalización. Las perspectivas de análisis listas para usar también están disponibles en el panel de información general de la cuenta.

Consulte la documentación para obtener más información sobre cómo [administrar puntuación de cuenta y posible cliente predictivo](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) servicio.

## Ver resultados predictivos de puntuación de clientes potenciales y cuentas {#how-to-view}

Después de ejecutar el trabajo, los resultados se guardan en un nuevo conjunto de datos del sistema para cada modelo con el nombre `LeadsAI.Scores` - ***el nombre de la puntuación***. Cada grupo de campos de puntuación puede encontrarse en `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Atributo | Descripción |
| --- | --- |
| Puntuación | La probabilidad relativa de que un perfil alcance el objetivo predicho dentro del lapso de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino más bien como la probabilidad de un perfil en comparación con la población general. Esta puntuación va del 0 al 100. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles con puntuaciones similares. Los percentiles van del 1 al 100. |
| Tipo de modelo | El tipo de modelo seleccionado indica si se trata de una puntuación de persona o de cuenta. |
| Fecha de puntuación | La fecha en la que se produjo la puntuación. |
| Factores influyentes | Razones previstas sobre por qué es probable que un perfil se convierta. Los factores se componen de los siguientes atributos:<ul><li>Código: el perfil o atributo de comportamiento que influye positivamente en la puntuación prevista de un perfil.</li><li>Valor: Valor del perfil o atributo de comportamiento.</li><li>Importancia: indica el peso que tiene el perfil o atributo de comportamiento en la puntuación predicha (baja, media, alta).</li></ul> |

### Ver puntuaciones del perfil del cliente

Para ver las puntuaciones predictivas de un perfil de persona, seleccione **[!UICONTROL Perfiles]** en la sección cliente del panel izquierdo y, a continuación, introduzca el área de nombres de identidad y el valor de identidad. Una vez finalizado, seleccione **[!UICONTROL Ver]**.

A continuación, seleccione el perfil en la lista.

![Perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

El **[!UICONTROL Detalle]** ahora incluye las puntuaciones predictivas. Haga clic en el icono de gráfico junto a la puntuación predictiva.

![Puntuación predictiva del perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Un cuadro de diálogo emergente muestra la puntuación, la distribución general de la puntuación, los factores más influyentes para esta puntuación y la definición del objetivo de la puntuación.

![Detalles de puntuación predictiva del perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Supervisión de trabajos predictivos de puntuación de clientes potenciales y cuentas {#monitoring-jobs}

Puede monitorizar las métricas básicas y el estado diario de ejecución del trabajo a través del panel. Las métricas incluyen:

* Perfiles totales de persona/cuenta marcados
* Siguiente trabajo de puntuación (fecha)
* Siguiente trabajo de formación (fecha)

Para obtener más información, consulte la documentación sobre [supervisar trabajos para la puntuación predictiva de clientes potenciales y cuentas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
