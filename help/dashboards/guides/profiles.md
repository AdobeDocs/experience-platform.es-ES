---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;panel de perfiles;panel
title: Panel de perfiles
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los datos del Perfil del cliente en tiempo real de su organización.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: ab76292f569fa8c21dab736d6291891b717d026d
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 1%

---

# [!UICONTROL Perfiles] tablero

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre su [!DNL Real-time Customer Profile] datos, tal como se capturan durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el [!UICONTROL Perfiles] tablero en la interfaz de usuario y proporciona información sobre las métricas que se muestran en el tablero.

Para obtener una descripción general de todas las funciones de perfil de la interfaz de usuario del Experience Platform, visite el [Guía de la interfaz de usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md).

## Datos de tablero de perfil

La variable [!UICONTROL Perfiles] tablero muestra una instantánea de los datos de atributo (registro) que su organización tiene en el Experience Platform Almacenamiento de perfiles . La instantánea no incluye datos de ningún evento (serie temporal).

Los datos de atributo de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel Perfil no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del [!UICONTROL Perfiles] tablero

Para ir a la [!UICONTROL Perfiles] tablero en la interfaz de usuario de Platform, seleccione **[!UICONTROL Perfiles]** en el carril izquierdo, seleccione la opción **[!UICONTROL Información general]** para mostrar el tablero.

>[!NOTE]
>
>Si su organización es nueva en Platform y aún no tiene conjuntos de datos de perfil activos o políticas de combinación creadas, se crea la variable [!UICONTROL Perfiles] tablero no está visible. En su lugar, la variable [!UICONTROL Información general] muestra vínculos y documentación para ayudarle a empezar con el Perfil del cliente en tiempo real.

![](../images/profiles/dashboard-overview.png)

### Modificación de la variable [!UICONTROL Perfiles] tablero

Puede modificar el aspecto del [!UICONTROL Perfiles] tablero seleccionando **[!UICONTROL Modificar tablero]**. Esto le permite mover, agregar y quitar widgets del tablero, así como acceder al **[!UICONTROL Biblioteca de utilidades]** para explorar las utilidades disponibles y crear utilidades personalizadas para su organización.

Consulte la [modificación de tableros](../customize/modify.md) y [información general de la biblioteca de utilidades](../customize/widget-library.md) documentación para obtener más información.

## (Beta) Perspectivas de la eficiencia del perfil {#profile-efficiency-insights}

>[!IMPORTANT]
>
>La funcionalidad de perspectiva de eficacia de perfil se encuentra actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La variable [!UICONTROL Eficacia] proporciona métricas sobre la calidad y exhaustividad de los datos de perfil mediante el uso de widgets de eficacia de perfil. Estas utilidades ilustran de un vistazo la composición de sus perfiles, las tendencias en la integridad a lo largo del tiempo y las evaluaciones de la calidad de sus datos de perfil.

[El panel de eficacia del perfil.](../images/profiles/attributes-quality-assessment.png)

Consulte la [sección widgets de eficacia de perfil](#profile-efficacy-widgets) para obtener más información sobre los widgets disponibles actualmente.

El diseño de este tablero también se puede personalizar seleccionando [**[!UICONTROL Modificar tablero]**](../customize/modify.md) de la variable [!UICONTROL Información general] pestaña .

## Explorar perfiles {#browse-profiles}

La variable [!UICONTROL Examinar] le permite buscar y ver los perfiles de solo lectura introducidos en su organización de IMS. Desde aquí puede ver información importante perteneciente al perfil sobre sus preferencias, eventos anteriores, interacciones y segmentos

Para obtener más información sobre las capacidades de visualización de perfiles proporcionadas en la interfaz de usuario de Platform, consulte la documentación de [exploración de perfiles en Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Combinar directivas {#merge-policies}

Las métricas que se muestran en la variable [!UICONTROL Perfiles] Los tableros se basan en políticas de combinación que se aplican a los datos del perfil del cliente en tiempo real. Cuando los datos se reúnen desde varias fuentes para crear el perfil del cliente, es posible que los datos contengan valores en conflicto (por ejemplo, un conjunto de datos puede enumerar a un cliente como &quot;único&quot;, mientras que otro conjunto de datos puede enumerar al cliente como &quot;casado&quot;). Es tarea de la directiva de combinación determinar qué datos se priorizan y muestran como parte del perfil.

Para obtener más información sobre las directivas de combinación, incluido cómo crear, editar y declarar una directiva de combinación predeterminada para su organización, comience por leer [información general sobre políticas de combinación](../../profile/merge-policies/overview.md).

El tablero seleccionará automáticamente una política de combinación para mostrar, pero puede cambiar la política de combinación seleccionada mediante el menú desplegable. Para elegir otra política de combinación, seleccione la lista desplegable junto al nombre de la política de combinación y, a continuación, seleccione la política de combinación que desee ver.

>[!NOTE]
>
>El menú desplegable muestra solamente las políticas de combinación relacionadas con la clase de perfil individual XDM. Sin embargo, si la organización ha creado varias políticas de combinación, puede significar que tendrá que desplazarse para ver la lista completa de las políticas de combinación disponibles.

![](../images/profiles/select-merge-policy.png)

## Esquemas de unión

La variable [!UICONTROL Esquema de unión] dashboard muestra el esquema de unión para una clase XDM específica. Seleccione la [!UICONTROL **Clase**] lista desplegable, puede ver los esquemas de unión de diferentes clases XDM.

Los esquemas de unión están compuestos por varios esquemas que comparten la misma clase y que se han habilitado para Perfil. Permiten ver en una sola vista, una combinación de todos los campos contenidos dentro de cada esquema que comparte la misma clase.

Consulte la guía de la interfaz de usuario del esquema de unión para obtener más información [visualización de esquemas de unión en la interfaz de usuario de Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets y métricas

El tablero está compuesto por widgets, que son métricas de solo lectura que proporcionan información importante sobre los datos de perfil.

La fecha y hora de &quot;última actualización&quot; de un widget muestra cuándo se tomó la última instantánea de los datos. La fecha y la hora de la instantánea se proporcionan en UTC; no se encuentra en la zona horaria del usuario individual o de la organización de IMS.

## Widgets estándar

Adobe proporciona varios widgets estándar que puede utilizar para visualizar distintas métricas relacionadas con los datos del perfil. También puede crear utilidades personalizadas para compartirlas con su organización mediante la [!UICONTROL Biblioteca de utilidades]. Para obtener más información sobre la creación de widgets personalizados, lea la [información general de la biblioteca de utilidades](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Recuento de perfiles]](#profile-count)
* [[!UICONTROL Perfiles añadidos]](#profiles-added)
* [[!UICONTROL Tendencia del recuento de perfiles]](#profiles-count-trend)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)

### [!UICONTROL Recuento de perfiles] {#profile-count}

La variable **[!UICONTROL Recuento de perfiles]** muestra el número total de perfiles combinados dentro del Almacenamiento de perfiles en el momento en que se tomó la instantánea. Este número es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

>[!NOTE]
>
>La variable [!UICONTROL Recuento de perfiles] El widget puede mostrar un número diferente del recuento de perfiles mostrado en la variable [!UICONTROL Examinar] en la ficha [!UICONTROL Perfiles] de la interfaz de usuario por varios motivos. La razón más común es porque la variable [!UICONTROL Examinar] hace referencia al número total de perfiles combinados en función de la política de combinación predeterminada de su organización, mientras que la pestaña [!UICONTROL Recuento de perfiles] hace referencia al número total de perfiles combinados en función de la política de combinación que ha seleccionado ver en el panel.
>
>Otro motivo común se debe a las diferencias entre el momento en que se toma la instantánea del panel y el momento en que se ejecuta el trabajo de muestra para el [!UICONTROL Examinar] pestaña . Puede ver cuándo [!UICONTROL Recuento de perfiles] se actualizó por última vez mirando la marca de tiempo en el widget y para obtener más información sobre cómo se activa el trabajo de muestra en el [!UICONTROL Examinar] consulte la [recuento de perfiles en la guía de la interfaz de usuario del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Perfiles añadidos] {#profiles-added}

La variable **[!UICONTROL Perfiles añadidos]** muestra el número total de perfiles combinados que se agregaron al Almacenamiento de perfiles desde la última instantánea que se tomó. Este número es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo. Puede utilizar el selector desplegable para ver los perfiles agregados en los últimos 30 días, 90 días o 12 meses.

>[!NOTE]
>
>La variable [!UICONTROL Perfiles añadidos] refleja el número de perfiles agregados después de configurar el Almacenamiento de perfiles y de ingerir perfiles. En otras palabras, si su organización configuró el Almacenamiento de perfiles e ingerió 4 000 000 en el Día 1, en un plazo de 24 horas el panel estaría disponible, sin embargo, el [!UICONTROL Perfiles añadidos] se establecería en 0. Esto se hace para evitar un pico asociado con la ingesta inicial de perfiles en el sistema. En los próximos 30 días, su organización ingesta 1 000 000 perfiles adicionales en el Almacenamiento de perfiles. Una vez tomada la siguiente instantánea, la variable [!UICONTROL Perfiles añadidos] La utilidad mostraría un total de 1000 000 perfiles agregados, mientras que la variable [!UICONTROL Recuento de perfiles] La utilidad mostraría 5000 000 perfiles totales.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Tendencia del recuento de perfiles] {#profiles-count-trend}

La variable **[!UICONTROL Tendencia del recuento de perfiles]** muestra el número total de perfiles combinados que se han agregado al Almacenamiento de perfiles diariamente durante los últimos 30 días, 90 días o 12 meses. Este número se actualiza cada día que se toma la instantánea, por lo que si ingeryera perfiles en Platform, el número de perfiles no se reflejaría hasta que se tome la siguiente instantánea. El recuento de perfiles agregados es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil para formar un único perfil para cada individuo.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

La variable **[!UICONTROL Tendencia del recuento de perfiles]** muestra un botón &quot;subtítulos&quot; en la parte superior derecha del widget. Select **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo rótulos automáticos.

![La ficha Información general del perfil muestra el widget de tendencia del recuento de perfiles con el botón rótulos resaltado.](../images/profiles/profile-count-trend-captions.png)

Un modelo de aprendizaje automático genera automáticamente subtítulos para describir las tendencias clave y los eventos importantes analizando el gráfico y los datos.

![Cuadro de diálogo de rótulos automáticos para el widget de tendencia de recuento de perfiles.](../images/profiles/profiles-count-trends-automatic-captions-dialog.png)

### [!UICONTROL Perfiles por identidad] {#profiles-by-identity}

La variable **[!UICONTROL Perfiles por identidad]** muestra el desglose de identidades en todos los perfiles combinados del Almacenamiento de perfiles. El número total de perfiles por identidad (es decir, sumando los valores mostrados para cada área de nombres) puede ser mayor que el número total de perfiles combinados, ya que un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

Para obtener más información sobre las identidades, visite [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Superposición de identidad] {#identity-overlap}

La variable **[!UICONTROL Superposición de identidad]** La utilidad muestra un diagrama de Venn o un diagrama de conjunto, que muestra la superposición de perfiles en su Almacenamiento de perfiles que contienen varias identidades.

Después de utilizar los menús desplegables del widget para seleccionar las identidades que desea comparar, aparecen círculos que muestran el tamaño relativo de cada identidad, y el número de perfiles que contienen ambas áreas de nombres se representa por el tamaño de la superposición entre los círculos. Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades con ese cliente individual, por lo que es probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre los fragmentos de perfil, comience por leer la sección en [fragmentos de perfil frente a perfiles combinados](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) en la descripción general del Perfil del cliente en tiempo real .

Para obtener más información sobre las identidades, visite [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## (Beta) Widgets de eficacia del perfil {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>Los widgets de eficiencia de perfil están actualmente en versión beta y no están disponibles para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Adobe proporciona varias utilidades para evaluar la integridad de los perfiles introducidos disponibles para su análisis de datos. Cada una de las utilidades de eficacia del perfil se puede filtrar mediante la política de combinación. Para cambiar el filtro de directiva de combinación, seleccione la opción[!UICONTROL Perfiles mediante una directiva de combinación] y elija la política adecuada en la lista disponible.

Para obtener más información sobre cada una de las utilidades de eficacia de perfil, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Evaluación de la calidad de los atributos]](#attribute-quality-assessment)
* [[!UICONTROL Complejidad del perfil]](#profile-completeness)
* [[!UICONTROL Tendencia de integridad del perfil]](#profile-completeness-trend)

### (Beta) [!UICONTROL Evaluación de la calidad de los atributos] {#attribute-quality-assessment}

Este widget muestra la integridad y cardinalidad de cada atributo de perfil desde la última fecha de procesamiento. Esta información se presenta como una tabla con cuatro columnas donde cada fila de la tabla representa un único atributo.

| Columna | Descripción |
|---|---|
| Atributo | Nombre del atributo. |
| Perfiles | Número de perfiles que tienen este atributo y se rellenan con valores no nulos. |
| Complejidad | Este porcentaje está determinado por el número total de perfiles que tienen este atributo y que se rellenan con valores no nulos. El número se calcula dividiendo el número total de perfiles por el número total de valores no vacíos en los perfiles de ese atributo. |
| Cardinalidad | El número total de **único** valores no nulos de este atributo. Se mide en todos los perfiles. |

![El widget de evaluación de la calidad de los atributos](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Perfiles completos] {#profile-completeness}

Este widget crea un gráfico circular de la integridad del perfil desde la última fecha de procesamiento. La integridad de un perfil se mide por el porcentaje de atributos que se rellenan con valores no nulos entre todos los atributos observados.

Este widget muestra la proporción de perfiles con una integridad alta, media o baja. De forma predeterminada, hay tres niveles de integridad configurados:

* Alto contenido: Los perfiles tienen más del 70 % de atributos completados.
* Complejidad media: Los perfiles tienen menos del 70 % y más del 30 % de atributos completados.
* Baja exhaustividad: Los perfiles tienen menos del 30 % de atributos rellenados.

![Los perfiles mediante la utilidad de integridad](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Tendencia de integridad del perfil] {#profile-completeness-trend}

Este widget crea un gráfico de columnas apiladas para mostrar la tendencia de la integridad del perfil a lo largo del tiempo. La integridad se mide mediante el porcentaje de atributos que se rellenan con valores no nulos entre todos los atributos observados. Clasifica la integridad del perfil como alta, media o baja desde la última fecha de procesamiento.

El eje x representa el tiempo, el eje y representa el número de perfiles y los colores representan los tres niveles de integridad del perfil.

Los tres niveles de integridad son:

* Alto contenido: Los perfiles tienen más del 70 % de atributos completados.
* Complejidad media: Los perfiles tienen menos del 70 % y más del 30 % de atributos completados.
* Baja exhaustividad: Los perfiles tienen menos del 30 % de atributos rellenados.

![El widget de tendencia de la compleción de perfiles](../images/profiles/profiles-completeness-trend.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel Perfiles y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con [!DNL Profile] en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md).
