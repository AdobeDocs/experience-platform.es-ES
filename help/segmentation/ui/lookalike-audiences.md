---
solution: Experience Platform
title: Audiencias con similitud
description: Aprenda a segmentar nuevas audiencias de alto valor en Adobe Experience Platform mediante audiencias de similitud.
badgeLimitedAvailability: label="Disponibilidad limitada" type=Caution
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 10%

---

# Guía de audiencias similares

>[!IMPORTANT]
>
>Tenga en cuenta que las perspectivas de similitud y las audiencias de similitud se encuentran en **disponibilidad limitada**.

En Adobe Experience Platform, las audiencias de similitud proporcionan una perspectiva inteligente de cada una de sus audiencias, aprovechando las perspectivas basadas en el aprendizaje automático para identificar y dirigirse a clientes de alto valor con sus campañas de marketing.

Con las audiencias de similitud, puede crear audiencias ampliadas dirigidas a clientes similares a sus audiencias de alto rendimiento o a clientes de destino similares a audiencias convertidas anteriormente.

## Terminología {#terminology}

Antes de empezar a usar las audiencias de similitud, asegúrese de comprender los siguientes conceptos:

- **Audiencia base**: la audiencia base es la audiencia sobre la que desea obtener más información. Esta es la audiencia a la que se asemeja el modelo **basado** en.
- **Modelo de similitud**: un modelo de similitud es un modelo de aprendizaje automático que se forma en cada audiencia base apta sin necesidad de recibir información del cliente. Cada modelo de similitud crea los factores influyentes y los gráficos de similitud. Un modelo de similitud sí lo hace **no** que te marquen.
- **Audiencia de similitudes**: una audiencia de similitud es la audiencia que se crea cuando se aplica a la audiencia base un modelo de similitud con un umbral de similitud seleccionado. Puede crear varias audiencias de similitud utilizando el mismo modelo de similitud. La audiencia de similitud es lo que se puntúa.
- **Tamaño total de la audiencia a la que se puede dirigir**: el tamaño total de audiencia a la que se puede dirigir es el número total de perfiles en los últimos 30 días menos la población de audiencia base en los últimos 30 días. Por ejemplo, si un cliente tiene 10 millones de perfiles en los últimos 30 días y la audiencia base tiene 1 millón de perfiles en los últimos 30 días, el tamaño total de audiencia direccionable es de 9 millones de perfiles.

## Detalles del modelo de similitud {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="No apto"
>abstract="Actualmente, este público no puede optar a datos de similitud, ya que puede que tenga menos del número mínimo de perfiles necesarios para la formación o que la exportación de perfiles aún no se haya activado."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Procesamiento"
>abstract="Este público se está procesando en este momento. El modelo puede tardar hasta 24 horas en finalizar el procesamiento. Inténtelo de nuevo más tarde."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Error"
>abstract="Se ha producido un error al procesar este modelo. Elimine y vuelva a compilar este modelo o inténtelo de nuevo más tarde."

En Adobe Experience Platform, el modelo de similitud consume tres tipos diferentes de puntos de datos:

- Abono a audiencias en los últimos 30 días
- Experimente eventos de los últimos 30 días que se han introducido en el Perfil del cliente en tiempo real
- Atributos de perfil de los últimos 30 días que se han introducido en el perfil del cliente en tiempo real

Todos estos puntos de datos se convierten en pares de valor clave que se introducen en el modelo de similitud. Solo se conservarán los pares de valor clave con un porcentaje significativo de perfiles coincidentes.

En este momento, el modelo de similitud se ejecuta cada 24 horas, creando y recreando los factores influyentes y los gráficos de similitud para las audiencias base. La puntuación para audiencias de similitud también se ejecuta con frecuencia.

## Derechos {#entitlements}

Los siguientes derechos se aplican al uso de audiencias de similitud:

- Los clientes de Real-Time CDP Prime tienen derecho a **5** audiencias de similitud activas en zonas protegidas de producción
- Los clientes de Real-Time CDP Ultimate tienen derecho a **20** audiencias de similitud activas en zonas protegidas de producción
- Los entornos limitados de desarrollo están limitados a **5** Audiencias similares para todos los clientes de Real-Time CDP

Los paquetes de complementos, que estarán disponibles más adelante, aumentan las autorizaciones de los entornos limitados de producción en 20 audiencias de similitud por paquete.

Para confirmar si tiene acceso a audiencias de similitud, póngase en contacto con su representante de Adobe.

## Ver perspectivas de similitud {#view}

La información sobre similitudes está integrada en la página de detalles de audiencia. Para ver las perspectivas de similitud de una audiencia, seleccione **[!UICONTROL Audiencias]** en la barra de navegación izquierda, seguido de **[!UICONTROL Examinar]** y la audiencia para la que desee ver las perspectivas.

![Se resalta el botón Audiencias, así como la audiencia base que se está utilizando para el modelado de similitudes.](../images/ui/lookalike-audiences/browse.png)

Aparecerá la página de detalles de la audiencia. Seleccionar **[!UICONTROL Información sobre similitudes]** para ver las similitudes de la audiencia. El **[!UICONTROL Información sobre similitudes]** se muestra la página. Esta página tiene tres elementos principales: el gráfico de similitud y alcance, las audiencias de similitud y los factores influyentes.

![La pestaña Información sobre similitudes aparece resaltada y muestra información sobre similitudes para la audiencia base.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Similitud y alcance {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Similitud y alcance"
>abstract="El gráfico de similitud y alcance traza el alcance esperado de un público de similitud compuesto por perfiles que superan una determinada puntuación de similitud. Puede situarse sobre un punto específico del gráfico para mostrar el porcentaje de similitud y el recuento de perfiles esperado para el punto resaltado actualmente."

La sección de similitud y alcance muestra un gráfico que representa el alcance esperado de una audiencia de similitud compuesta por perfiles superiores a una puntuación de similitud determinada. La puntuación de similitud representa el **Distancia** de similitud entre el perfil de la audiencia base y el perfil de la perspectiva de similitud.

![Se resaltará el gráfico de similitud y alcance.](../images/ui/lookalike-audiences/similarity-and-reach.png)

En este gráfico, el eje x mide el porcentaje de similitud entre un perfil y los miembros de la audiencia seleccionada. La puntuación de similitud va del 0% al 100%, con una puntuación de similitud más alta que indica que un perfil está más cerca, en términos de valores de factor influyente, de los miembros de la audiencia seleccionada.

El eje Y muestra el recuento esperado de perfiles con el porcentaje de similitud que corresponde al valor coincidente del eje X. Este recuento esperado de perfiles va desde 0 hasta el tamaño total de audiencia direccionable o 25 millones de perfiles, el que sea menor. Este eje se mide en una **escala logarítmica** para mejorar la legibilidad del gráfico.

Tenga en cuenta que el gráfico es **acumulativo** de derecha a izquierda. Esto significa que en cualquier punto del gráfico, el valor del eje Y es el número de perfiles que tienen una similitud **superior** el umbral de similitud. Por ejemplo, si el eje x está en el 60 % y el eje y es de 10 millones, significa que hay 10 millones de perfiles que tienen una similitud de o superior al 60 % con la audiencia base.

Puede situarse sobre un punto específico del gráfico para mostrar el porcentaje de similitud y el recuento de perfiles esperado para el punto resaltado actualmente.

### Audiencias de similitud {#list}

La sección Audiencias de similitud muestra una lista de todas las audiencias de similitud que se han creado anteriormente para la audiencia base seleccionada.

![Se resalta la sección Audiencias de similitud.](../images/ui/lookalike-audiences/select-laa.png)

### Factores influyentes {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Factores influyentes"
>abstract="Los factores influyentes son atributos, eventos y pertenencias a públicos que son importantes para explicar la similitud de un perfil de los miembros del público base. Las etiquetas y políticas de uso de datos se pueden utilizar para que ciertos datos no se consideren factores influyentes en modelos de similitud."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=es#exclude" text="Excluir datos"

La sección de factores influyentes muestra los 100 factores que más influyen en el modelo de similitud para la audiencia base seleccionada. Estos factores influyentes son los atributos de perfil, los eventos de experiencia y las suscripciones a audiencias, que son los más importantes para explicar las similitudes en la audiencia base. Comprender los principales factores influyentes le permite personalizar mejor el contenido de marketing para esta audiencia y para cualquier audiencia de similitud que cree a partir de ella. Tenga en cuenta que no se mostrarán todos los factores influyentes que afectan al modelo de similitud.

En el caso de factores influyentes numéricos, los pares de valor clave se pueden agrupar en bloques, según el número de valores diferentes que tenga la clave. Por ejemplo, si tiene una clave de `income`, es muy probable que haya muchos valores únicos. Como resultado, los pares de valor clave se colocarán en bloques que podrían tener el aspecto de `income=[0 -> 30000]`, `income=[30000 -> 50000]`, y `income=[50000 -> 100000]`.

Estos contenedores se vuelven a calcular regularmente para garantizar que los datos se mantengan actualizados.

![Se resalta la sección de factores influyentes.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Los factores influyentes se clasifican en orden de importancia y son independientes entre sí.

| Campo | Descripción |
| ----- | ----------- |
| Tipo | El tipo de datos del que se deriva el factor influyente. Puede ser un atributo de perfil, un evento de experiencia o una pertenencia a una audiencia. |
| Clave | Nombre del campo de datos. Para las claves del tipo de pertenencia a audiencia, este valor representa el **namespace** de la audiencia de la que proceden los datos. Los valores posibles incluyen `ups` (Servicio de segmentación) y `AO` (Audience Orchestration). Para claves de otros tipos, este valor representa la ruta del campo XDM. Por ejemplo, si la empresa Luma tiene un campo personalizado llamado ingresos, la clave sería `_luma.income` |
| Valor | El valor varía según el factor influyente que represente. Para atributos de perfil o eventos de experiencia, este campo representa el valor o el rango de valores del campo de datos que indica la similitud con los miembros de la audiencia base. El intervalo de valores se escribe en el formulario `[A -> B]`, donde `A` representa el rango inferior mientras que `B` representa el rango superior. Para las suscripciones a audiencias, este campo es el nombre de la audiencia. |
| Importancia | El nivel relativo de importancia del factor influyente. Puede ser alto, medio o bajo. |

## Crear una audiencia de similitud {#create}

>[!IMPORTANT]
>
>Usted **no puede** usar una audiencia de similitud como audiencia base para otra audiencia de similitud. Es decir, tú... **no puede** crear audiencias de similitud encadenadas.

Para crear una audiencia de similitud, debe seleccionar la audiencia en la que desea basar la audiencia de similitud. Para acceder a la lista de audiencias disponibles, seleccione **[!UICONTROL Audiencias]** en la barra de navegación izquierda, seguido de **[!UICONTROL Examinar]**. Aparecerá la lista de audiencias. En esta página, puede seleccionar la audiencia que desee utilizar como audiencia base.

![Se resalta el botón Audiencias, así como la audiencia base que se está utilizando para el modelado de similitudes.](../images/ui/lookalike-audiences/browse.png)

En la página de detalles de la audiencia, seleccione **[!UICONTROL Crear audiencias de similitud]** para comenzar el proceso de creación de una audiencia de similitud.

![El [!UICONTROL Crear audiencias de similitud] botón resaltado.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

El **[!UICONTROL Crear una audiencia similar]** aparece la ventana emergente. En esta página, puede establecer el porcentaje de similitud para la audiencia de similitud.

![El [!UICONTROL Crear una audiencia similar] se muestra la ventana emergente.](../images/ui/lookalike-audiences/create-audience.png)

Puede establecer este porcentaje de similitud de tres formas diferentes:

- Mueva el control deslizante para definir el porcentaje de similitud
- Introduzca el porcentaje de similitud en el cuadro de entrada numérica situado junto al regulador
- Pase el ratón sobre el gráfico y seleccione la ubicación que desee para definir el porcentaje de similitud

También puede actualizar los detalles sobre la audiencia de similitud, incluido su nombre y descripción. De forma predeterminada, el nombre de la audiencia de similitud se genera en función del nombre de la audiencia base y el porcentaje de similitud especificado anteriormente.

![La información básica se resalta en la variable [!UICONTROL Crear una audiencia similar] popover.](../images/ui/lookalike-audiences/basic-info.png)

Seleccionar **[!UICONTROL Crear]** para terminar de crear su audiencia de similitud.

![El botón Crear se resalta dentro de la etiqueta [!UICONTROL Crear una audiencia similar] popover.](../images/ui/lookalike-audiences/create-audience.png)

Se puede acceder a la audiencia de similitud recién creada en el **[!UICONTROL Audiencias de similitud]** de la página de detalles de audiencia y también está disponible en el Portal de audiencias y para otros usos posteriores. Tenga en cuenta que la audiencia de similitud tardará un poco en recibir la puntuación. Hasta que se clasifique, el recuento de perfiles parecerá ser 0.

## Ver detalles de audiencias similares {#view-details}

Para ver los detalles de una audiencia de similitud, seleccione la audiencia de similitud en la **[!UICONTROL Audiencias de similitud]** de la audiencia base.

![Se resalta la sección Audiencias de similitud.](../images/ui/lookalike-audiences/select-laa.png)

Aparecerá la página de detalles de la audiencia. Para obtener más información sobre esta página, lea la [sección de detalles de audiencia de la guía de IU del servicio de segmentación](./overview.md#audience-details).

![Se muestran los detalles de la audiencia de similitud.](../images/ui/lookalike-audiences/laa-details.png)

## Excluir campos de datos del modelado de similitud {#exclude}

Las audiencias similares se pueden configurar para excluir campos de datos restringidos para la acción de marketing &quot;Ciencia de datos&quot; mediante la aplicación de las etiquetas y políticas de uso de datos relevantes. Los datos etiquetados como restringidos del uso para la ciencia de datos se eliminarán de consideración al entrenar un modelo de audiencia de similitud y al generar una audiencia de similitud a partir del modelo entrenado. 

La etiqueta estándar &quot;C9&quot; se puede utilizar para etiquetar datos que no deben utilizarse para la ciencia de datos y se puede aplicar habilitando la directiva estándar &quot;Restringir la ciencia de datos&quot;. También puede crear políticas adicionales para restringir el uso de datos con otras etiquetas, incluidas las etiquetas confidenciales, para la ciencia de datos. Para obtener más información sobre la administración de las políticas de uso de datos, lea la [Guía de IU de políticas de uso de datos](../../data-governance/policies/user-guide.md). Para obtener más información sobre la administración de etiquetas de uso de datos, lea la [guía de IU de etiquetas de uso de datos](../../data-governance/labels/user-guide.md).

De forma predeterminada, el proceso de modelado para audiencias de similitud excluirá **cualquiera** campo, conjunto de datos o audiencia en función de la política de privacidad habilitada para su organización. Si la audiencia base no tiene etiquetas de contrato, el proceso de modelado excluirá **cualquiera** campo, conjunto de datos o audiencia en función de la política de privacidad habilitada para su organización.

Tenga en cuenta que **usted** son responsables de garantizar que los datos, incluidos los datos confidenciales, estén etiquetados correctamente y que las políticas de uso de datos se hayan definido y habilitado para cumplir con las obligaciones legales y regulatorias en las que opera. También debe tener en cuenta que los campos de datos o las suscripciones a segmentos que son **no** la correlación directa con los campos de datos asociados normalmente con tipos de datos confidenciales o protegidos puede ser una fuente de sesgo potencial. **Usted** son responsables de analizar los datos para identificar, etiquetar y aplicar las políticas de uso de datos adecuadas a los datos, incluidos los campos de datos que puedan representar tipos de datos confidenciales o protegidos y que deban excluirse del modelado.

## Pasos siguientes

Después de leer esta guía, ha aprendido a ver perspectivas de similitud y a crear audiencias de similitud basadas en estas perspectivas. Para obtener más información sobre las audiencias en la interfaz de usuario de Adobe Experience Platform, lea la [Guía de IU del servicio de segmentación](./overview.md).
