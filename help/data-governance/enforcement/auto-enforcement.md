---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;Aplicación automática;aplicación basada en API;control de datos
solution: Experience Platform
title: Aplicación automática de directivas
description: Este documento explica cómo se aplican automáticamente las políticas de uso de datos al activar segmentos en destinos en Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# Aplicación automática de directivas

>[!IMPORTANT]
>
>La aplicación automática de directivas solo está disponible para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

Una vez etiquetados los datos y definidas las políticas de uso de los datos, puede hacer cumplir las políticas de uso de los datos. Al activar segmentos de audiencia en destinos, Adobe Experience Platform aplica automáticamente las políticas de uso en caso de que se produzcan infracciones.

>[!NOTE]
>
>Este documento se centra en la aplicación de las políticas de control y consentimiento de los datos. Para obtener información sobre las políticas de control de acceso, consulte la documentación sobre [control de acceso basado en atributos](../../access-control/abac/overview.md).

## Requisitos previos

Esta guía requiere una comprensión práctica de los servicios de la plataforma implicados en la aplicación automática. Consulte la siguiente documentación para obtener más información antes de continuar con esta guía:

* [Administración de datos de Adobe Experience Platform](../home.md): El marco mediante el cual Platform exige el cumplimiento de las normas de uso de datos mediante el uso de etiquetas y políticas.
* [Perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): El motor de segmentación dentro de [!DNL Platform] se utiliza para crear segmentos de audiencia a partir de perfiles de clientes en función de los comportamientos y atributos de los clientes.
* [Destinos](../../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación sin problemas de datos desde Platform para campañas de marketing multicanal, campañas de correo electrónico, publicidad de destino, etc.

## Flujo de aplicación {#flow}

El diagrama siguiente ilustra cómo se integra la aplicación de políticas en el flujo de datos de la activación de segmentos:

![](../images/enforcement/enforcement-flow.png)

Cuando se activa por primera vez un segmento, [!DNL Policy Service] comprobaciones de las políticas aplicables basadas en los siguientes factores:

* Las etiquetas de uso de datos aplicadas a campos y conjuntos de datos dentro del segmento que se va a activar.
* El propósito de marketing del destino.
* Los perfiles que han consentido en incluirse en la activación de segmentos, según las políticas de consentimiento configuradas.

>[!NOTE]
>
>Si hay etiquetas de uso de datos que solo se han aplicado a ciertos campos dentro de un conjunto de datos (en lugar de todo el conjunto de datos), la aplicación de esas etiquetas de nivel de campo en la activación solo se produce bajo las siguientes condiciones:
>
>* Los campos se utilizan en la definición del segmento.
>* Los campos se configuran como atributos proyectados para el destino de destino.


## Línea de datos {#lineage}

El linaje de datos desempeña un papel clave en la forma en que se aplican las políticas en Platform. En términos generales, el linaje de datos se refiere al origen de un conjunto de datos y a lo que le sucede (o a dónde se mueve) a lo largo del tiempo.

En el contexto de la administración de datos, el linaje permite que las etiquetas de uso de datos se propaguen desde conjuntos de datos a servicios descendentes que consumen sus datos, como el Perfil del cliente en tiempo real y los destinos. Esto permite evaluar y aplicar las políticas en varios puntos clave del recorrido de los datos a través de Platform y proporciona contexto a los consumidores de datos para saber por qué se produjo una infracción de la política.

En Experience Platform, a la aplicación de políticas le preocupa el siguiente linaje:

1. Los datos se incorporan a Platform y se almacenan en **conjuntos de datos**.
1. Los perfiles de cliente se identifican y construyen a partir de esos conjuntos de datos combinando fragmentos de datos según la variable **combinar directiva**.
1. Los grupos de perfiles se dividen en **segmentos** en función de atributos comunes.
1. Los segmentos se activan para el flujo descendente **destinos**.

Cada etapa del calendario anterior representa una entidad que puede contribuir a la aplicación de las políticas, como se indica en el cuadro siguiente:

| Etapa del linaje de datos | Función en la aplicación de políticas |
| --- | --- |
| Conjunto de datos | Los conjuntos de datos contienen etiquetas de uso de datos (aplicadas en el nivel de conjunto de datos o campo) que definen los casos de uso para los que se puede utilizar todo el conjunto de datos o campos específicos. Se producirán infracciones de directiva si se utiliza un conjunto de datos o campo que contenga determinadas etiquetas con un fin restringido por una directiva.<br><br>Los atributos de consentimiento recopilados de sus clientes también se almacenan en conjuntos de datos. Si tiene acceso a políticas de consentimiento, cualquier perfil que no cumpla los requisitos de atributos de consentimiento de sus políticas se excluirá de los segmentos que se activan en un destino. |
| Combinar directiva | Las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos al combinar fragmentos de varios conjuntos de datos. Se producirán infracciones de directiva si las políticas de combinación están configuradas de modo que los conjuntos de datos con etiquetas restringidas se activen en un destino. Consulte la [información general sobre políticas de combinación](../../profile/merge-policies/overview.md) para obtener más información. |
| Segmento | Las reglas de segmentos definen qué atributos deben incluirse en los perfiles de cliente. Dependiendo de los campos que incluya una definición de segmento, el segmento heredará cualquier etiqueta de uso aplicada para esos campos. Se producirán infracciones de directiva si activa un segmento cuyas etiquetas heredadas están restringidas por las políticas aplicables del destino de destino según su caso de uso de marketing. |
| Destino | Al configurar un destino, se puede definir una acción de marketing (a veces denominada caso de uso de marketing). Este caso de uso se correlaciona con una acción de marketing tal como se define en una política. En otras palabras, la acción de marketing que defina para un destino determina qué políticas de uso de datos y políticas de consentimiento son aplicables a ese destino.<br><br>Las infracciones de la política de uso de datos se producen si activa un segmento cuyas etiquetas de uso están restringidas para la acción de marketing del destino objetivo.<br><br>(Beta) Cuando se activa un segmento, cualquier perfil que no contenga los atributos de consentimiento necesarios para la acción de marketing (según se definen en las políticas de consentimiento) se excluye de la audiencia activada. |

>[!IMPORTANT]
>
>Algunas políticas de uso de datos pueden especificar dos o más etiquetas con una relación AND. Por ejemplo, una directiva podría restringir una acción de marketing si las etiquetas `C1` Y `C2` están presentes, pero no restringe la misma acción si solo está presente una de esas etiquetas.
>
>En cuanto a la aplicación automática, el marco de control de datos no considera la activación de segmentos independientes en un destino como una combinación de datos. Por lo tanto, el ejemplo `C1 AND C2` directiva es **NOT** se aplica si estas etiquetas se incluyen en segmentos separados. En su lugar, esta política solo se aplica cuando ambas etiquetas están presentes en el mismo segmento tras la activación.

Cuando se producen infracciones de directiva, los mensajes resultantes que aparecen en la interfaz de usuario proporcionan herramientas útiles para explorar el linaje de datos de contribución de la infracción para ayudar a resolver el problema. Más información en la siguiente sección.

## Mensajes de aplicación de políticas {#enforcement}

Las secciones siguientes describen los diferentes mensajes de aplicación de políticas que aparecen en la interfaz de usuario de Platform:

* [Infracción de la directiva de uso de datos](#data-usage-violation)
* [Evaluación de la directiva de consentimiento](#consent-policy-evaluation)

### Infracción de la directiva de uso de datos {#data-usage-violation}

Si se produce una infracción de política al intentar activar un segmento (o [realizar modificaciones en un segmento ya activado](#policy-enforcement-for-activated-segments)) la acción se impide y aparece una ventana emergente que indica que se han violado una o más políticas. Una vez que se ha activado una infracción, la variable **[!UICONTROL Guardar]** se desactiva para la entidad que modifique hasta que se actualicen los componentes adecuados para cumplir las políticas de uso de datos.

Seleccione una infracción de directiva en la columna izquierda de la ventana emergente para mostrar los detalles de dicha infracción.

![](../images/enforcement/violation-policy-select.png)

El mensaje de infracción proporciona un resumen de la política violada, incluidas las condiciones que la política está configurada para comprobar, la acción específica que activó la infracción y una lista de posibles resoluciones para el problema.

![](../images/enforcement/violation-summary.png)

Se muestra un gráfico de linaje de datos debajo del resumen de infracciones, que le permite visualizar qué conjuntos de datos, políticas de combinación, segmentos y destinos estuvieron involucrados en la infracción de directiva. La entidad que está cambiando se resalta en el gráfico, indicando qué punto del flujo está causando la infracción. Puede seleccionar un nombre de entidad dentro del gráfico para abrir la página de detalles de la entidad en cuestión.

![](../images/enforcement/data-lineage.png)

También puede usar la variable **[!UICONTROL Filtro]** icono (![](../images/enforcement/filter.png)) para filtrar las entidades mostradas por categoría. Se deben seleccionar al menos dos categorías para que se muestren los datos.

![](../images/enforcement/lineage-filter.png)

Select **[!UICONTROL Vista de lista]** para mostrar el linaje de datos como una lista. Para volver al gráfico visual, seleccione **[!UICONTROL Vista de ruta]**.

![](../images/enforcement/list-view.png)

### Evaluación de la directiva de consentimiento {#consent-policy-evaluation}

Si tiene [crear políticas de consentimiento](../policies/user-guide.md#consent-policy) y están activando un segmento en un destino, puede ver cómo las políticas de consentimiento afectan al porcentaje de perfiles que se incluyen en la activación.

#### Evaluación previa a la activación

Una vez que llegue al **[!UICONTROL Consulte]** step when [activación de un destino](../../destinations/ui/activation-overview.md), seleccione **[!UICONTROL Ver políticas aplicadas]**.

![Botón Ver políticas aplicadas en el flujo de trabajo de activación de destino](../images/enforcement/view-applied-policies.png)

Aparece un cuadro de diálogo de comprobación de políticas que muestra una vista previa de cómo las políticas de consentimiento afectan a la audiencia consentida de los segmentos activados.

![Cuadro de diálogo de comprobación de la política de consentimiento en la interfaz de usuario de Platform](../images/enforcement/consent-policy-check.png)

El cuadro de diálogo muestra la audiencia consentida para un segmento a la vez. Para ver la evaluación de directivas de un segmento diferente, utilice el menú desplegable situado encima del diagrama para seleccionar uno de la lista.

![Conmutador de segmentos en el cuadro de diálogo de comprobación de políticas](../images/enforcement/segment-switcher.png)

Utilice el carril izquierdo para cambiar entre las políticas de consentimiento aplicables para el segmento seleccionado. Las políticas que no están seleccionadas se representan en la sección &quot;[!UICONTROL Otras políticas]&quot; del diagrama.

![Conmutador de directivas en el cuadro de diálogo de comprobación de directivas](../images/enforcement/policy-switcher.png)

El diagrama muestra la superposición entre tres grupos de perfiles:

1. Perfiles que cumplen los requisitos para el segmento seleccionado
1. Perfiles que cumplen los requisitos para la directiva de consentimiento seleccionada
1. Perfiles que cumplen los requisitos para las otras políticas de consentimiento aplicables para el segmento (denominados &quot;[!UICONTROL Otras políticas]&quot; en el diagrama)

Los perfiles que cumplen los tres grupos anteriores representan la audiencia consentida para el segmento seleccionado, resumida en el carril derecho.

![Sección Resumen del cuadro de diálogo de comprobación de políticas](../images/enforcement/summary.png)

Pase el ratón sobre una de las audiencias del diagrama para mostrar el número de perfiles que contiene.

![Resaltado de una sección de diagrama en el cuadro de diálogo de comprobación de políticas](../images/enforcement/highlight-segment.png)

La audiencia consentida se representa mediante la superposición central del diagrama y se puede resaltar como las demás secciones.

![Resaltado de la audiencia consentida en el diagrama](../images/enforcement/consented-audience.png)

#### Aplicación de ejecución de flujo

Cuando se activan los datos en un destino, los detalles de ejecución del flujo muestran el número de identidades que se excluyeron debido a políticas de consentimiento activas.

![Métricas de identidades excluidas para una ejecución de flujo de datos](../images/enforcement/dataflow-run-enforcement.png)

## Aplicación de políticas para segmentos activados {#policy-enforcement-for-activated-segments}

La aplicación de políticas sigue aplicándose a los segmentos después de activarlos, lo que restringe cualquier cambio en un segmento o su destino que pueda provocar una infracción de la política. Debido a cómo [linaje de datos](#lineage) funciona en la aplicación de políticas, cualquiera de las siguientes acciones puede potencialmente déclencheur una infracción:

* Actualización de las etiquetas de uso de datos
* Cambio de los conjuntos de datos de un segmento
* Cambio de los predicados de segmentos
* Cambio de las configuraciones de destino

Si alguna de las acciones anteriores déclencheur una infracción, se impide que esa acción se guarde y se muestre un mensaje de infracción de directiva, lo que garantiza que los segmentos activados sigan cumpliendo las políticas de uso de datos al modificarse.

## Pasos siguientes

Este documento abarcaba cómo funciona la aplicación automática de políticas en el Experience Platform. Para ver los pasos sobre cómo integrar mediante programación la aplicación de políticas en las aplicaciones mediante llamadas a API, consulte la guía de [Aplicación basada en API](./api-enforcement.md).
