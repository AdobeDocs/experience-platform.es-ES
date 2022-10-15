---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;panel de perfiles;panel
title: Guía del panel de perfiles
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los datos del Perfil del cliente en tiempo real de su organización.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 1755f5030f5730ca06ea718635ede9deb1188d21
workflow-type: tm+mt
source-wordcount: '3387'
ht-degree: 0%

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

Consulte la [modificación de tableros](../customize/modify.md) y [Información general de la biblioteca de utilidades](../customize/widget-library.md) documentación para obtener más información.

### Agregar widgets {#add-widget}

Select **[!UICONTROL Agregar utilidad]** para ir a la biblioteca de widgets y ver una lista de las utilidades disponibles para agregarlas al tablero.

![Información general del tablero Perfiles con la utilidad de adición resaltada.](../images/profiles/profiles-overview-add-widget.png)

Desde la biblioteca de utilidades puede examinar la selección de utilidades de segmento estándar y personalizadas. Para obtener información sobre cómo agregar utilidades, consulte la documentación de la biblioteca de utilidades sobre cómo [agregar una utilidad](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Explorar perfiles {#browse-profiles}

La variable [!UICONTROL Examinar] le permite buscar y ver los perfiles de solo lectura introducidos en su organización. Desde aquí puede ver información importante perteneciente al perfil sobre sus preferencias, eventos anteriores, interacciones y segmentos

Para obtener más información sobre las capacidades de visualización de perfiles proporcionadas en la interfaz de usuario de Platform, consulte la documentación de [exploración de perfiles en Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Combinar directivas {#merge-policies}

Las métricas que se muestran en la variable [!UICONTROL Perfiles] tablero se basa en políticas de combinación que se aplican a los datos del perfil del cliente en tiempo real. Cuando los datos se agrupan desde varias fuentes para crear el perfil del cliente, los datos pueden contener valores en conflicto. Por ejemplo, un conjunto de datos puede enumerar a un cliente como &quot;soltero&quot; mientras que otro conjunto de datos puede enumerarlo como &quot;casado&quot;. Es tarea de la directiva de combinación determinar qué datos se priorizan y muestran como parte del perfil.

Para obtener más información sobre las directivas de combinación, incluido cómo crear, editar y declarar una directiva de combinación predeterminada para su organización, comience por leer [información general sobre políticas de combinación](../../profile/merge-policies/overview.md).

El tablero seleccionará automáticamente una directiva de combinación para usar. La política de combinación aplicada se puede cambiar utilizando el menú desplegable situado junto al nombre de la política de combinación.

>[!NOTE]
>
>El menú desplegable solo muestra las políticas de combinación que usan la variable `_xdm.context.profile` esquema. Sin embargo, si la organización ha creado varias políticas de combinación, puede significar que debe desplazarse para ver la lista completa de las políticas de combinación disponibles.

![La ficha Información general de perfiles con la lista desplegable de política de combinación resaltada.](../images/profiles/select-merge-policy.png)

## Esquemas de unión

La variable [!UICONTROL Esquema de unión] dashboard muestra el esquema de unión para una clase XDM específica. Seleccione la **[!UICONTROL Clase]** lista desplegable, puede ver los esquemas de unión de diferentes clases XDM.

Los esquemas de unión están compuestos por varios esquemas que comparten la misma clase y que se han habilitado para Perfil. Permiten ver en una sola vista, una combinación de todos los campos contenidos dentro de cada esquema que comparte la misma clase.

Consulte la guía de la interfaz de usuario del esquema de unión para obtener más información [visualización de esquemas de unión en la interfaz de usuario de Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets y métricas

El tablero está compuesto por widgets, que son métricas de solo lectura que proporcionan información importante sobre los datos de perfil.

La fecha y la hora de la instantánea más reciente se muestran en la parte superior del [!UICONTROL Información general] junto a la lista desplegable combinar directiva . Todos los datos del widget son precisos a partir de esa fecha y hora. La marca de tiempo de la instantánea se proporciona en UTC; no está en la zona horaria del usuario u organización individual.

![La ficha Información general del panel Perfiles con la marca de tiempo de instantánea más reciente resaltada.](../images/profiles/snapshot-timestamp.png)

## Widgets estándar {#standard-widgets}

Adobe proporciona varios widgets estándar que puede utilizar para visualizar distintas métricas relacionadas con los datos del perfil. También puede crear utilidades personalizadas para compartirlas con su organización mediante la [!UICONTROL Biblioteca de utilidades]. Para obtener más información sobre la creación de widgets personalizados, lea la [Información general de la biblioteca de utilidades](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Recuento de perfiles]](#profile-count)
* [[!UICONTROL Tendencia del recuento de perfiles]](#profile-count-trend)
* [[!UICONTROL Cambio de recuento de perfiles]](#profile-count-change)
* [[!UICONTROL Tendencia del cambio en el recuento de perfiles]](#profiles-count-change-trend)
* [[!UICONTROL El recuento de perfiles cambia la tendencia por identidad]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles de identidad únicos]](#single-identity-profiles)
* [[!UICONTROL Perfiles de identidad únicos por identidad]](#single-identity-profiles-by-identity)
* [[!UICONTROL Perfiles sin segmentar]](#unsegmented-profiles)
* [[!UICONTROL Tendencia de perfiles sin segmentar]](#unsegmented-profiles-trend)
* [[!UICONTROL Perfiles sin segmentar por identidad]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiencias]](#audiences)
* [[!UICONTROL Audiencias asignadas al estado de destino]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Tamaño de las audiencias]](#audiences-size)
* [[!UICONTROL Superposición de audiencias por directiva de combinación]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Informe de superposición de audiencia]](#audience-overlap-report)

### [!UICONTROL Recuento de perfiles] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Recuento de perfiles"
>abstract="Esta utilidad muestra el número total de perfiles combinados dentro del Almacenamiento de perfiles en el momento en que se tomó la instantánea. El número depende de la política de combinación seleccionada que se aplique a los datos de perfil."

La variable **[!UICONTROL Recuento de perfiles]** muestra el número total de perfiles combinados dentro del Almacenamiento de perfiles en el momento en que se tomó la instantánea. Este número es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

>[!NOTE]
>
>La variable [!UICONTROL Recuento de perfiles] El widget puede mostrar un número diferente del recuento de perfiles mostrado en la variable [!UICONTROL Examinar] en la ficha [!UICONTROL Perfiles] de la interfaz de usuario por varios motivos. La razón más común para esto es porque la variable [!UICONTROL Examinar] hace referencia al número total de perfiles combinados en función de la política de combinación predeterminada de su organización, mientras que la pestaña [!UICONTROL Recuento de perfiles] hace referencia al número total de perfiles combinados en función de la política de combinación que ha seleccionado ver en el panel.
>
>Otro motivo común se debe a las diferencias entre el momento en que se toma la instantánea del panel y el momento en que se ejecuta el trabajo de muestra para el [!UICONTROL Examinar] pestaña . Puede ver cuándo [!UICONTROL Recuento de perfiles] se actualizó por última vez mirando la marca de tiempo en el widget y para obtener más información sobre cómo se activa el trabajo de muestra en el [!UICONTROL Examinar] consulte la [recuento de perfiles en la guía de la interfaz de usuario del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Tendencia del recuento de perfiles] {#profile-count-trend}

La variable [!UICONTROL Tendencia del recuento de perfiles] La utilidad utiliza un gráfico de líneas para ilustrar la tendencia del número total de perfiles contenidos en el sistema a lo largo del tiempo. Este número total incluye todos los perfiles importados en el sistema desde la última instantánea diaria. Los datos se pueden visualizar en períodos de 30 días, 90 días y 12 meses. El periodo de tiempo se elige en un menú desplegable del widget.

![El widget de tendencia de recuento de perfiles .](../images/profiles/profile-count-trend.png)

### [!UICONTROL Cambio de recuento de perfiles] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Cambio de recuento de perfiles"
>abstract="Esta utilidad muestra el número total de perfiles combinados **added** al Almacenamiento de perfiles en el momento de la última instantánea. El número depende de la política de combinación seleccionada que se aplique a los datos de perfil."

La variable **[!UICONTROL Cambio de recuento de perfiles]** muestra el número de perfiles combinados agregados al Almacenamiento de perfiles desde la instantánea anterior. Este número es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo. Puede utilizar el selector desplegable para ver el número de perfiles agregados en los últimos 30 días, 90 días o 12 meses.

>[!NOTE]
>
>La variable [!UICONTROL Cambio de recuento de perfiles] refleja el número de perfiles agregados **after** la ingesta inicial de perfiles y la configuración del Almacenamiento de perfiles. En otras palabras, si su organización configuró el Almacenamiento de perfiles e ingerió 4 000 000 en el Día 1, en un plazo de 24 horas el panel estaría disponible, sin embargo, el [!UICONTROL Cambio de recuento de perfiles] se establecería en 0. Esto se hace para evitar un pico asociado con la ingesta inicial de perfiles en el sistema. En los próximos 30 días, su organización ingesta 1 000 000 perfiles adicionales en el Almacenamiento de perfiles. Una vez tomada la siguiente instantánea, la variable [!UICONTROL Cambio de recuento de perfiles] La utilidad mostraría un total de 1000 000 perfiles agregados, mientras que la variable [!UICONTROL Recuento de perfiles] La utilidad mostraría 5000 000 perfiles totales.

![El tablero Perfiles de la IU de plataforma con el widget de cambio de recuento de perfiles resaltado.](../images/profiles/profile-count-change.png)

### [!UICONTROL Tendencia del cambio en el recuento de perfiles] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendencia del cambio en el recuento de perfiles"
>abstract="Este widget muestra el número de perfiles combinados que se han agregado a la Tienda de perfiles diariamente durante los últimos 30 días, 90 días o 12 meses. El número también depende de la política de combinación seleccionada que se aplique a los datos de perfil."

La variable **[!UICONTROL Tendencia del cambio en el recuento de perfiles]** muestra el número total de perfiles combinados que se han agregado al Almacenamiento de perfiles diariamente durante los últimos 30 días, 90 días o 12 meses. Este número se actualiza cada día que se toma la instantánea, por lo que si ingeryera perfiles en Platform, el número de perfiles no se reflejaría hasta que se tome la siguiente instantánea. El recuento de perfiles agregados es el resultado de la política de combinación seleccionada que se aplica a los datos de perfil para combinar fragmentos de perfil para formar un único perfil para cada individuo.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

La variable **[!UICONTROL Tendencia del cambio en el recuento de perfiles]** muestra un botón &quot;subtítulos&quot; en la parte superior derecha del widget. Select **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo rótulos automáticos.

![La ficha Información general del perfil muestra el widget de tendencia del cambio del recuento de perfiles con el botón rótulos resaltado.](../images/profiles/profiles-count-change-trend-captions.png)

Un modelo de aprendizaje automático genera automáticamente subtítulos para describir las tendencias clave y los eventos importantes analizando el gráfico y los datos. Las anotaciones se añaden al gráfico en función de los rótulos. Seleccione un rótulo para centrarse en su anotación correspondiente.

![El cuadro de diálogo rótulos automáticos del widget de tendencia de cambio de recuento de perfiles.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL El recuento de perfiles cambia la tendencia por identidad] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Este widget filtra el recuento de perfiles en función de una identidad de origen seleccionada y de una política de combinación, y a continuación ilustra el cambio de número de una variedad de períodos utilizando un gráfico de líneas. La política de combinación se selecciona en el menú desplegable de información general de la parte superior de la página; la identidad de origen y el periodo de tiempo se seleccionan en los menús desplegables de la utilidad. La tendencia se puede visualizar en periodos de 30 días, 90 días y 12 meses.

Esta utilidad le ayuda a administrar sus necesidades de activación de destino demostrando el patrón de crecimiento de perfiles filtrados por una identidad requerida.

![El recuento de perfiles cambia la tendencia por el widget de identidad.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Perfiles por identidad] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Perfiles por identidad"
>abstract="Esta utilidad muestra el desglose de todos los perfiles combinados en su Almacenamiento de perfiles por identidades."

La variable **[!UICONTROL Perfiles por identidad]** muestra el desglose de identidades en todos los perfiles combinados del Almacenamiento de perfiles. El número total de perfiles por identidad (es decir, sumando los valores mostrados para cada área de nombres) puede ser mayor que el número total de perfiles combinados, ya que un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

Consulte la [sección sobre directivas de combinación anterior en este documento](#merge-policies) para obtener más información.

![El tablero de información general Perfiles con el widget Perfiles por identidad resaltado.](../images/profiles/profiles-by-identity.png)

Select **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo rótulos automáticos.

![Cuadro de diálogo perfiles por rótulos de identidad.](../images/profiles/profiles-by-identity-captions.png)

Un modelo de aprendizaje automático genera automáticamente perspectivas de datos analizando la distribución general y las dimensiones clave de los datos.

Para obtener más información sobre las identidades, visite [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

### [!UICONTROL Superposición de identidad] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Superposición de identidad"
>abstract="Esta utilidad utiliza un diagrama de Venn para mostrar la superposición de perfiles en su Almacenamiento de perfiles que contienen las dos identidades seleccionadas."

La variable **[!UICONTROL Superposición de identidad]** La utilidad utiliza un diagrama de Venn, o un diagrama de conjunto, para mostrar la superposición de perfiles en el Almacenamiento de perfiles que contienen las dos identidades seleccionadas.

Utilice los menús desplegables de utilidades para seleccionar las identidades que desea comparar. Los círculos muestran el recuento total relativo de perfiles que contienen cada identidad. El número de perfiles que contienen ambas identidades se representa por el tamaño de la superposición entre los círculos. Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades con ese cliente individual, por lo que es probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre los fragmentos de perfil, comience por leer la sección en [fragmentos de perfil frente a perfiles combinados](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) en la descripción general del Perfil del cliente en tiempo real .

Para obtener más información sobre las identidades, visite [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

### [!UICONTROL Perfiles de identidad únicos] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Perfiles de identidad únicos"
>abstract="Esta utilidad proporciona un recuento de los perfiles de su organización que solo tienen un tipo de ID que crea su identidad. Este tipo de ID puede ser un correo electrónico o un ECID."

La variable [!UICONTROL Perfiles de identidad únicos] proporciona un recuento de los perfiles de su organización que solo tienen un tipo de ID que crea su identidad. Este tipo de ID puede ser un correo electrónico o un ECID. El recuento de perfiles se genera a partir de los datos contenidos en la instantánea más reciente.

![utilidad Perfiles de identidad únicos .](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Perfiles de identidad únicos por identidad] {#single-identity-profiles-by-identity}

Esta utilidad utiliza un gráfico de barras para ilustrar el número total de perfiles identificados con un único identificador. La utilidad admite hasta cinco de las identidades más comunes.

Pase el ratón sobre las barras individuales para ver un cuadro de diálogo que detalle el recuento total de perfiles de una identidad.

![Los perfiles de identidad únicos por widget de identidad.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Perfiles sin segmentar] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Perfiles sin segmentar"
>abstract="Esta utilidad proporciona el número total de perfiles que no están adjuntos a ningún segmento y representa la oportunidad de activar perfiles en toda la organización."

La variable [!UICONTROL Perfiles sin segmentar] proporciona el número total de perfiles que no están adjuntos a ningún segmento. El número generado es preciso a partir de la última instantánea y representa la oportunidad de activar perfiles en toda la organización. También indica la oportunidad de eliminar perfiles que no proporcionan un ROI adecuado.

![El widget Perfiles sin segmentar.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Tendencia de perfiles sin segmentar] {#unsegmented-profiles-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendencia de perfiles sin segmentar"
>abstract="Esta utilidad proporciona una ilustración gráfica de líneas del número de perfiles que no están adjuntos a ningún segmento durante un período de tiempo determinado. La tendencia de perfiles no adjuntos a ningún segmento se puede visualizar en periodos de 30 días, 90 días y 12 meses."

La variable [!UICONTROL Tendencia de perfiles sin segmentar] proporciona una ilustración de gráfico de líneas del número de perfiles que no están adjuntos a ningún segmento durante un período de tiempo determinado. La tendencia de perfiles no adjuntos a ningún segmento se puede visualizar en periodos de 30 días, 90 días y 12 meses. El periodo de tiempo se elige en un menú desplegable del widget. El recuento de perfiles se refleja en el eje y y en el tiempo en el eje x.

![El widget Tendencia de perfiles sin segmentar .](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL Perfiles sin segmentar por identidad] {#unsegmented-profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Perfiles sin segmentar por identidad"
>abstract="Esta utilidad categoriza el número total de perfiles sin segmentar por su identificador único."

La variable [!UICONTROL Perfiles sin segmentar por identidad] categoriza el número total de perfiles sin segmentar por su identificador único. Los datos se visualizan en un gráfico de barras para facilitar la comparación.

![El widget Perfiles sin segmentar por identidad .](../images/profiles/unsegmented-profiles-by-identity.png)

### [!UICONTROL Audiencias] {#audiences}

Esta utilidad proporciona el número total de segmentos que están listos para activarse, según la política de combinación elegida aplicada a los datos de perfil.

Select **[!UICONTROL Audiencias]** para navegar hasta el [!UICONTROL Segmentos] tablero [!UICONTROL Examinar] pestaña . Desde allí puede ver una lista de todas las definiciones de segmentos para su organización.

![El widget Audiencias .](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Informe de superposición de audiencia] {#audience-overlap-report}

Esta utilidad tabulariza los datos de superposición de audiencia de todos los segmentos disponibles filtrados por la política de combinación. Se proporciona una lista de cinco audiencias clasificadas entre los porcentajes de superposición más altos y los más bajos para la política de combinación elegida en el menú desplegable de la parte superior de la pantalla. Los dos segmentos analizados se enumeran en la [!UICONTROL SEGMENTAR UN NOMBRE] y [!UICONTROL NOMBRE DEL SEGMENTO B] columnas. La superposición porcentual se proporciona en la tercera columna con una precisión de doce decimales.

El informe de superposición de audiencia le ayuda a crear nuevos segmentos de alto rendimiento. La observación de superposiciones de porcentaje elevado permite suprimir audiencias e impedir que se envíe la misma audiencia a diferentes destinos. También le ayudan a identificar perspectivas ocultas que podrían ayudar a mejorar la segmentación. La superposición de porcentaje bajo ayuda a localizar perfiles únicos que se van a buscar.

Select **[!UICONTROL Ver más]** para abrir un cuadro de diálogo de pantalla completa que contenga más datos de superposición de audiencia.

![El widget de informe Audiencia se superpone con Ver más resaltado .](../images/profiles/profiles-audience-overlap-report.png)

La variable [!UICONTROL Informe de superposición de audiencia] se abre. Este cuadro de diálogo puede contener hasta 50 filas de análisis de superposición de audiencia divididos en seis columnas. Seleccione el icono de configuración (![El icono de configuración.](../images/profiles/settings-icon.png)) para quitar o agregar columnas de la tabla.

![El cuadro de diálogo Informe de superposición de audiencia .](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Seleccione el **[!UICONTROL Superposición]** para cambiar la clasificación de los resultados entre mayor a menor o de menor a mayor.

Para descargar todo el informe en formato de PDF, seleccione el menú de opciones (**`...`**) seguido de **[!UICONTROL Descargar]**.

![El cuadro de diálogo Informe de superposición de audiencia con la opción de elipses y descarga resaltada.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Seleccione una fila del informe para abrir un diagrama de Venn del análisis de superposición. Pase el ratón sobre una sección del diagrama de Venn para ver el recuento de perfiles en un cuadro de diálogo.

![El cuadro de diálogo Informe de superposición de audiencia incluye un diagrama de Venn y una fila resaltada.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Select **[!UICONTROL Cerrar]** para volver a la [!UICONTROL Perfiles] tablero.

### [!UICONTROL Audiencias asignadas al estado de destino] {#audiences-mapped-to-destination-status}

La variable [!UICONTROL Audiencias asignadas al estado de destino] La utilidad muestra el número total de audiencias asignadas y no asignadas en una única métrica y utiliza un gráfico de anillos para ilustrar la diferencia proporcional entre sus totales. Los números calculados dependen de la política de combinación elegida.

Los recuentos individuales de audiencias asignadas o no asignadas se muestran en un cuadro de diálogo cuando el cursor se sitúa sobre la sección correspondiente del gráfico circular.

![Las audiencias asignadas al widget de estado de destino.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Tamaño de las audiencias] {#audiences-size}

La variable [!UICONTROL Tamaño de las audiencias] proporciona una tabla de dos columnas que enumera hasta 20 segmentos y el número total de audiencias contenidas en cada segmento. La lista se ordena de mayor a menor según el número total de audiencias. El número total de tamaño de audiencia depende de la política de combinación aplicada.

![El widget de tamaño de las audiencias.](../images/profiles/audiences-size.png)

Para ver información completa sobre un segmento, seleccione un nombre de segmento de la lista proporcionada para ir al [!UICONTROL Segmentos] [!UICONTROL Detalle] página. Asimismo, seleccionando **[!UICONTROL Ver todos los segmentos]** desde el final de la utilidad, puede desplazarse hasta la [!UICONTROL Segmentos] [!UICONTROL Examinar] para buscar cualquier segmento existente.

![El widget Tamaño de audiencias con un nombre de segmento y vea todo el texto de los segmentos resaltado.](../images/profiles/audiences-size-view-all-segments.png)

Consulte la documentación para obtener más información sobre la [[!UICONTROL Segmentos] [!UICONTROL  Examinar] ficha](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Superposición de audiencias por directiva de combinación] {#audience-overlap-by-merge-policy}

Esta utilidad utiliza un diagrama de Venn para mostrar la superposición de dos segmentos seleccionados. La política de combinación se elige en la lista desplegable de información general situada en la parte superior de la página y los segmentos para análisis se seleccionan en dos menús desplegables dentro de la utilidad. El número total de perfiles contenidos dentro de la definición de segmento correspondiente se puede ver pasando el cursor sobre un círculo o la intersección.

A medida que la utilidad muestra la transición visual de las definiciones de segmentos, puede optimizar su estrategia de segmentación estudiando las similitudes entre las definiciones de segmentos.

![El tablero Perfiles de la interfaz de usuario de la plataforma con la lista desplegable de directivas de combinación y los desplegables de segmentos de widget resaltados.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel Perfiles y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con [!DNL Profile] en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md).
