---
title: Puntuación predictiva de posibles clientes y cuentas en Real-Time CDP B2B
type: Documentation
description: Información general y más información sobre la característica de puntuación de cuentas y posibles clientes predictiva en CDP B2B del Experience Platform.
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Puntuación predictiva de posibles clientes y cuentas en Real-Time CDP B2B

Los especialistas en marketing B2B se enfrentan a múltiples desafíos en la parte superior del canal de marketing. Para ser eficaces, los especialistas en marketing B2B necesitan una manera automatizada de calificar a la gran cantidad de personas para que puedan centrarse en los objetivos de alto valor. La calificación debe alinearse con el resultado de ventas definitivo, no solo con la conversión de marketing.

Las cuentas, son las entidades últimas que compran productos y servicios B2B. Para comercializar y vender de forma eficaz, los especialistas en marketing B2B deben conocer no solo los de las personas, sino también los de la cuenta, la probabilidad de comprar.

El marketing basado en cuentas, en particular, establece estrategias para las cuentas como objetivos de marketing. Las puntuaciones de propensión a comprar de las cuentas ayudan en gran medida a los especialistas en marketing B2B a priorizar entre las cuentas para maximizar su retorno de la inversión.

El servicio de puntuación de clientes potenciales y cuentas predictivo aborda los desafíos anteriores aprendiendo de los eventos de conversión de fase de oportunidad y prediciendo estos, y agregando actividades de personas al nivel de cuenta para producir las puntuaciones de cuenta. Las puntuaciones están fácilmente disponibles como campos personalizados en perfiles de persona y perfiles de cuenta, y se pueden incluir fácilmente como criterios de segmento para restringir la audiencia. Los principales factores influyentes también están disponibles a nivel agregado y de unidad para ayudar a los especialistas en marketing B2B a comprender mejor qué elementos condujeron a las puntuaciones.

## Comprensión de la puntuación de cuentas y posibles clientes predictivos {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] actualmente se necesita la fuente de datos, ya que es la única fuente de datos que puede proporcionar los eventos de conversión a nivel de perfil de persona.

La Puntuación de posibles clientes y cuentas predictiva utiliza un método de aprendizaje automático basado en árboles (bosque aleatorio/aumento de degradado) para crear el modelo de puntuación de posibles clientes predictivo.

Los administradores tienen la capacidad de configurar varios objetivos de puntuación de perfil, también denominados modelos, uno para cada evento de conversión configurado, lo que permite generar puntuaciones independientes para cada objetivo configurado.

La puntuación de cuentas y posibles clientes predictivos admite los siguientes tipos y campos de objetivos de conversión:

| Tipo de objetivo | Campos |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Ejemplo: `opportunityEvent.dataValueChanges.attributeName` es igual que `Stage` y `opportunityEvent.dataValueChanges.newValue` es igual que `Contract`</ul> |

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
>El algoritmo solo inspecciona `sourceAccountKey.sourceKey` del grupo de campos Persona:personComponents .

* Perfil de la cuenta

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

Se admiten varios modelos, con los siguientes límites duros establecidos:

* Cada simulador para pruebas de producción tiene derecho a cinco modelos.
* Cada simulador para pruebas de desarrollo tiene derecho a un modelo.

Los requisitos de calidad de los datos son los siguientes:

* Lo ideal es que haya dos años de datos más recientes con fines de formación.
* La longitud mínima de los datos necesaria es de seis meses más la ventana de predicción.
* Para cada objetivo de predicción, se requieren al menos 10 eventos de conversión cualificados.

Los trabajos de puntuación se ejecutan diariamente y los resultados se guardan como atributos de perfil y atributos de cuenta, que pueden utilizarse posteriormente en las definiciones de segmentos y la personalización. Las perspectivas de análisis listas para usar también están disponibles en el panel Información general de la cuenta .

Consulte la documentación para obtener más información sobre cómo [administrar la puntuación de cliente potencial y cuenta predictiva](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) servicio.

## Ver resultados predictivos de puntuación de clientes potenciales y cuentas {#how-to-view}

Después de ejecutar el trabajo, los resultados se guardan en un nuevo conjunto de datos del sistema para cada modelo con el nombre `LeadsAI.Scores` - ***el nombre de la puntuación***. Cada grupo de campos de puntuación se puede localizar en `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Atributo | Descripción |
| --- | --- |
| Puntuación | La probabilidad relativa de que un perfil alcance el objetivo predicho dentro del lapso de tiempo definido. Este valor no se debe tratar como un porcentaje de probabilidad, sino como la probabilidad de un perfil comparado con la población general. Esta puntuación va del 0 al 100. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles de puntuación similar. Los percentiles varían de 1 a 100. |
| Tipo de modelo | El tipo de modelo seleccionado, indica si se trata de una persona o una puntuación de cuenta. |
| Fecha de puntuación | Fecha en la que se produjo la puntuación. |
| Factores influyentes | Motivos predichos de por qué es probable que un perfil se convierta. Los factores se componen de los siguientes atributos:<ul><li>Código: El perfil o atributo de comportamiento que influye positivamente en la puntuación predicha de un perfil.</li><li>Valor: El valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso que tiene el perfil o el atributo de comportamiento en la puntuación predicha (baja, media o alta).</li></ul> |

### Ver puntuaciones del perfil del cliente

Para ver las puntuaciones predictivas de un perfil de persona, seleccione **[!UICONTROL Perfiles]** en la sección cliente del panel izquierdo y, a continuación, introduzca el área de nombres de identidad y el valor de identidad. Una vez finalizado, seleccione **[!UICONTROL Ver]**.

A continuación, seleccione el perfil de la lista.

![Perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

La variable **[!UICONTROL Detalle]** ahora incluye las puntuaciones predictivas. Haga clic en el icono de gráfico junto a la puntuación predictiva.

![Puntuación predictiva del perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Un cuadro de diálogo emergente muestra la puntuación, la distribución general de la puntuación, los factores de mayor influencia para esta puntuación y la definición del objetivo de la puntuación.

![Detalles de puntuación predictiva del perfil del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Monitorización de trabajos predictivos de puntuación de cuentas y posibles clientes {#monitoring-jobs}

Puede monitorizar las métricas básicas y el estado diario de ejecución del trabajo a través del panel. Las métricas incluyen:

* Perfiles de persona/cuenta totales marcados
* Siguiente trabajo de puntuación (fecha)
* Siguiente trabajo de formación (fecha)

Para obtener más información, consulte la documentación de [monitorización de trabajos para puntuación de cuentas y posibles clientes predictiva](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
