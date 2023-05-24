---
keywords: Experience Platform;inicio;temas populares;aplicación de políticas;aplicación automática;aplicación basada en API;gobernanza de datos
solution: Experience Platform
title: Aplicación automática de políticas
description: Este documento explica cómo se aplican automáticamente las políticas de uso de datos al activar segmentos en destinos en Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: d0113390f49ba7ba7ecbbc40bdcd750a26040006
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# Aplicación automática de políticas

>[!IMPORTANT]
>
>La aplicación automática de directivas solo está disponible para organizaciones que han adquirido **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad**.

Una vez etiquetados los datos y definidas las políticas de uso de datos, puede aplicar el cumplimiento de las políticas. Al activar segmentos de audiencia en destinos, Adobe Experience Platform aplica automáticamente las políticas de uso en caso de que se produzca alguna infracción.

>[!NOTE]
>
>Este documento se centra en la aplicación de la gobernanza de datos y las políticas de consentimiento. Para obtener información sobre las políticas de control de acceso, consulte la documentación sobre [control de acceso basado en atributos](../../access-control/abac/overview.md).

## Requisitos previos

Esta guía requiere una comprensión práctica de los servicios de Platform implicados en la aplicación automática. Consulte la siguiente documentación para obtener más información antes de continuar con esta guía:

* [Gobernanza de datos de Adobe Experience Platform](../home.md): marco mediante el cual Platform aplica el cumplimiento del uso de datos mediante el uso de etiquetas y políticas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): el motor de segmentación dentro de [!DNL Platform] se utiliza para crear segmentos de audiencia a partir de los perfiles de clientes en función de los comportamientos y atributos de los clientes.
* [Destinos](../../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y mucho más.

## Flujo de aplicación {#flow}

El diagrama siguiente ilustra cómo se integra la aplicación de directivas en el flujo de datos de activación de segmentos:

![](../images/enforcement/enforcement-flow.png)

Cuando se activa un segmento por primera vez, [!DNL Policy Service] comprueba las directivas aplicables en función de los siguientes factores:

* Las etiquetas de uso de datos aplicadas a campos y conjuntos de datos dentro del segmento que se va a activar.
* El propósito de marketing del destino.
* Los perfiles que han aceptado incluirse en la activación del segmento, en función de las políticas de consentimiento configuradas.

>[!NOTE]
>
>Si hay etiquetas de uso de datos que solo se hayan aplicado a ciertos campos dentro de un conjunto de datos (en lugar de todo el conjunto de datos), la aplicación de esas etiquetas de nivel de campo en la activación solo se produce en las siguientes condiciones:
>
>* Los campos se utilizan en la definición del segmento.
>* Los campos se configuran como atributos proyectados para el destino final.


## Linaje de datos {#lineage}

El linaje de datos desempeña un papel clave en la forma en que se aplican las políticas en Platform. En términos generales, el linaje de datos hace referencia al origen de un conjunto de datos y a lo que le sucede (o a dónde se mueve) a lo largo del tiempo.

En el contexto de la gobernanza de datos, el linaje permite que las etiquetas de uso de datos se propaguen de conjuntos de datos a servicios descendentes que consumen sus datos, como el perfil del cliente en tiempo real y los destinos. Esto permite evaluar y aplicar las políticas en varios puntos clave del recorrido de los datos a través de Platform y proporciona contexto a los consumidores de datos para saber por qué se ha producido una infracción de política.

En Experience Platform, la aplicación de políticas se refiere al siguiente linaje:

1. Los datos se incorporan en Platform y se almacenan en **conjuntos de datos**.
1. Los perfiles de cliente se identifican y construyen a partir de esos conjuntos de datos combinando fragmentos de datos según la variable **política de combinación**.
1. Los grupos de perfiles se dividen en **segmentos** en función de atributos comunes.
1. Los segmentos se activan en sentido descendente **destinos**.

Cada etapa de la cronología anterior representa una entidad que puede contribuir a la aplicación de las políticas, como se indica en la tabla siguiente:

| Fase de linaje de datos | Función en la aplicación de políticas |
| --- | --- |
| Conjunto de datos | Los conjuntos de datos contienen etiquetas de uso de datos (aplicadas en el nivel de conjunto de datos o campo) que definen para qué casos de uso se puede utilizar todo el conjunto de datos o campos específicos. Se producirán infracciones de directivas si se utiliza un conjunto de datos o un campo que contenga determinadas etiquetas para un fin restringido por una directiva.<br><br>Cualquier atributo de consentimiento recopilado de sus clientes también se almacena en conjuntos de datos. Si tiene acceso a las políticas de consentimiento, los perfiles que no cumplan los requisitos de atributo de consentimiento de las políticas se excluirán de los segmentos activados en un destino. |
| Política de combinación | Las políticas de combinación son las reglas que utiliza Platform para determinar la prioridad que se dará a los datos al combinar fragmentos de varios conjuntos de datos. Se producirán infracciones de directivas si las políticas de combinación se configuran de modo que los conjuntos de datos con etiquetas restringidas se activen en un destino. Consulte la [resumen de políticas de combinación](../../profile/merge-policies/overview.md) para obtener más información. |
| Segmento | Las reglas de segmentos definen qué atributos deben incluirse de los perfiles de clientes. Según los campos que incluya una definición de segmento, el segmento heredará las etiquetas de uso aplicadas a esos campos. Se producirán violaciones de política si activa un segmento cuyas etiquetas heredadas estén restringidas por las políticas aplicables del destino de destino, según su caso de uso de marketing. |
| Destino | Al configurar un destino, se puede definir una acción de marketing (a veces denominada caso de uso de marketing). Este caso de uso se correlaciona con una acción de marketing tal como se define en una directiva. En otras palabras, la acción de marketing que defina para un destino determina qué políticas de uso de datos y políticas de consentimiento son aplicables a ese destino.<br><br>Las infracciones de las políticas de uso de datos se producen si activa un segmento cuyas etiquetas de uso están restringidas para la acción de marketing del destino de destino.<br><br>(Beta) Cuando se activa un segmento, los perfiles que no contienen los atributos de consentimiento necesarios para la acción de marketing (según se definen en las políticas de consentimiento) se excluyen de la audiencia activada. |

>[!IMPORTANT]
>
>Algunas políticas de uso de datos pueden especificar dos o más etiquetas con una relación AND. Por ejemplo, una directiva podría restringir una acción de marketing si las etiquetas `C1` Y `C2` están ambas presentes, pero no restringe la misma acción si solo una de esas etiquetas está presente.
>
>En cuanto a la aplicación automática, el marco de control de datos no considera la activación de segmentos independientes en un destino como una combinación de datos. Por lo tanto, el ejemplo `C1 AND C2` la política es **NO** se aplica si estas etiquetas se incluyen en segmentos separados. En su lugar, esta directiva solo se aplica cuando ambas etiquetas están presentes en el mismo segmento tras la activación.

Cuando se producen violaciones de directivas, los mensajes resultantes que aparecen en la interfaz de usuario proporcionan herramientas útiles para explorar el linaje de datos que contribuye a la infracción para ayudar a resolver el problema. En la siguiente sección se proporcionan más detalles.

## Mensajes de aplicación de políticas {#enforcement}

Las secciones siguientes describen los diferentes mensajes de aplicación de políticas que aparecen en la IU de Platform:

* [Infracción de directiva de uso de datos](#data-usage-violation)
* [Evaluación de directiva de consentimiento](#consent-policy-evaluation)

### Infracción de directiva de uso de datos {#data-usage-violation}

Si se produce una infracción de directiva al intentar activar un segmento (o [realización de ediciones en un segmento ya activado](#policy-enforcement-for-activated-segments)) la acción se impide y aparece una ventana emergente que indica que se han violado una o más políticas. Una vez activada una infracción, la variable **[!UICONTROL Guardar]** El botón está desactivado para la entidad que está modificando hasta que se actualicen los componentes adecuados para cumplir con las políticas de uso de datos.

Seleccione una infracción de directiva en la columna izquierda de la ventana emergente para mostrar los detalles de dicha infracción.

![](../images/enforcement/violation-policy-select.png)

El mensaje de infracción proporciona un resumen de la directiva que se ha violado, incluidas las condiciones que la directiva está configurada para comprobar, la acción específica que activó la infracción y una lista de posibles soluciones para el problema.

![](../images/enforcement/violation-summary.png)

Debajo del resumen de la infracción se muestra un gráfico de linaje de datos, que le permite visualizar qué conjuntos de datos, políticas de combinación, segmentos y destinos participaron en la infracción de política. La entidad que está cambiando actualmente aparece resaltada en el gráfico, indicando en qué punto del flujo se produce la infracción. Puede seleccionar un nombre de entidad dentro del gráfico para abrir la página de detalles de la entidad en cuestión.

![](../images/enforcement/data-lineage.png)

También puede utilizar la variable **[!UICONTROL Filtrar]** icono (![](../images/enforcement/filter.png)) para filtrar las entidades mostradas por categoría. Se deben seleccionar al menos dos categorías para que se muestren los datos.

![](../images/enforcement/lineage-filter.png)

Seleccionar **[!UICONTROL Vista de lista]** para mostrar el linaje de datos como una lista. Para volver al gráfico visual, seleccione **[!UICONTROL Vista de ruta]**.

![](../images/enforcement/list-view.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

Si tiene [directivas de consentimiento creadas](../policies/user-guide.md#consent-policy) y estén activando un segmento en un destino, puede ver cómo las políticas de consentimiento afectan al porcentaje de perfiles incluidos en la activación.

#### Mejora de la política de consentimiento para medios de pago {#consent-policy-enhancement}

Mejora de la aplicación de la política de consentimiento en [lote](../../destinations/destination-types.md#file-based) y [transmisión](../../destinations/destination-types.md#streaming-destinations) se han realizado destinos que incluyen activaciones de medios de pago. Esta mejora está disponible para los clientes de Privacy and Security Shield o Healthcare Shield, y elimina de forma proactiva los perfiles de los destinos de lote y de flujo continuo a medida que cambia el estado del consentimiento. También garantiza que los cambios de consentimiento se propaguen inmediatamente para que la audiencia adecuada siempre esté segmentada.

Buena Estas mejoras permiten confiar más en la estrategia de marketing, ya que eliminan la necesidad de que los especialistas en marketing agreguen manualmente atributos de consentimiento a su expresión de segmento. Esto garantiza que no se segmenten perfiles de forma involuntaria para ninguna experiencia de marketing una vez que se haya retirado el consentimiento o ya no se cumpla la política de consentimiento. Las políticas de consentimiento de marketing que establecen reglas sobre cómo se deben administrar los datos de consentimiento o preferencia en varios flujos de trabajo de marketing ahora se aplican automáticamente en los flujos de trabajo de activación en las soluciones descendentes.

>[!NOTE]
>
>No hay cambios en la interfaz de usuario como resultado de esta mejora.

#### Evaluación previa a la activación

Una vez que llegue a la **[!UICONTROL Revisar]** paso cuando [activación de un destino](../../destinations/ui/activation-overview.md), seleccione **[!UICONTROL Ver directivas aplicadas]**.

![Botón Ver políticas aplicadas en el flujo de trabajo de activación de destino](../images/enforcement/view-applied-policies.png)

Aparece un cuadro de diálogo de comprobación de directivas que muestra una previsualización de cómo las políticas de consentimiento afectan a la audiencia consentida de los segmentos activados.

![Cuadro de diálogo de comprobación de directivas de consentimiento en la IU de Platform](../images/enforcement/consent-policy-check.png)

El cuadro de diálogo muestra la audiencia consentida para un segmento a la vez. Para ver la evaluación de directivas de un segmento diferente, utilice el menú desplegable situado encima del diagrama para seleccionar uno de la lista.

![Conmutador de segmentos en el cuadro de diálogo de comprobación de directivas](../images/enforcement/segment-switcher.png)

Utilice el carril izquierdo para cambiar entre las políticas de consentimiento aplicables al segmento seleccionado. Las políticas que no están seleccionadas se representan en la sección &quot;[!UICONTROL Otras políticas]&quot; del diagrama.

![Conmutador de directivas en el cuadro de diálogo de comprobación de directivas](../images/enforcement/policy-switcher.png)

El diagrama muestra la superposición entre tres grupos de perfiles:

1. Perfiles aptos para el segmento seleccionado
1. Perfiles aptos para la política de consentimiento seleccionada
1. Perfiles que cumplen los requisitos de las demás políticas de consentimiento aplicables para el segmento (denominadas &quot;[!UICONTROL Otras políticas]&quot; en el diagrama)

Los perfiles que cumplen los tres grupos anteriores representan la audiencia consentida para el segmento seleccionado, resumida en el carril derecho.

![Sección Resumen del cuadro de diálogo de comprobación de directivas](../images/enforcement/summary.png)

Pase el ratón sobre una de las audiencias del diagrama para ver el número de perfiles que contiene.

![Resaltar una sección de diagrama en el cuadro de diálogo de comprobación de directivas](../images/enforcement/highlight-segment.png)

La audiencia consentida se representa mediante la superposición central del diagrama y se puede resaltar como las otras secciones.

![Resaltar la audiencia consentida en el diagrama](../images/enforcement/consented-audience.png)

#### Ejecución de ejecución de flujo

Cuando se activan los datos en un destino, los detalles de la ejecución del flujo muestran el número de identidades que se excluyeron debido a las políticas de consentimiento activas.

![Métricas de identidades excluidas para una ejecución de flujo de datos](../images/enforcement/dataflow-run-enforcement.png)

## Aplicación de políticas para segmentos activados {#policy-enforcement-for-activated-segments}

La aplicación de directivas sigue aplicándose a los segmentos una vez activados, lo que restringe cualquier cambio realizado en un segmento o en su destino que pueda provocar una infracción de directiva. Debido a cómo [linaje de datos](#lineage) funciona en la aplicación de directivas, cualquiera de las siguientes acciones puede infringir potencialmente un déclencheur:

* Actualización de etiquetas de uso de datos
* Cambiar conjuntos de datos para un segmento
* Cambio de predicados de segmento
* Cambio de configuraciones de destino

Déclencheur Si alguna de las acciones anteriores infringe alguna, se impide guardar esa acción y se muestra un mensaje de infracción de directiva, lo que garantiza que los segmentos activados sigan cumpliendo las políticas de uso de datos cuando se modifiquen.

## Pasos siguientes

Este documento abarcaba cómo funciona la aplicación automática de directivas en Experience Platform. Para ver los pasos sobre cómo integrar mediante programación la aplicación de políticas en sus aplicaciones mediante llamadas a la API, consulte la guía sobre [Aplicación basada en API](./api-enforcement.md).
