---
title: Análisis de consentimiento y seguimiento
description: Obtenga información sobre cómo crear un panel de análisis de consentimiento para rastrear las tendencias del consentimiento del usuario a lo largo del tiempo.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: 454f485a327233ca1a5b37ea58f16b7b53255ba6
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Análisis y seguimiento del consentimiento

En el panorama de marketing actual, debe comprender y respetar las preferencias de consentimiento del cliente. Adobe Real-time Customer Data Platform permite a los especialistas en marketing analizar el consentimiento de los clientes para generar confianza, cumplir con las normas de privacidad y ofrecer experiencias más personalizadas.

Este documento detalla cómo crear un panel de consentimiento para varios casos de uso de marketing para datos de Real-Time CDP. En concreto, se centra en cómo crear una audiencia con los atributos adecuados para sus necesidades comerciales y luego consumir las perspectivas mediante el uso de widgets preconfigurados en la interfaz de usuario de Adobe Experience Platform. También se presenta un método alternativo para crear su propio widget personalizado con la función de paneles definida por el usuario.

## Casos de uso {#use-cases}

Los casos de uso cubiertos en esta guía son las tendencias de consentimiento y la superposición de consentimiento.

- **Tendencia de consentimiento** registra las tendencias del consentimiento del usuario a lo largo del tiempo. El análisis de los cambios de preferencias de consentimiento ayuda a los especialistas en marketing a planificar y ejecutar campañas que se adapten a esos cambios de preferencias de usuario. Por ejemplo, es posible que desee ejecutar campañas educativas dirigidas, campañas de transparencia y confianza o campañas de incentivos para impulsar las opciones de consentimiento. También puede correlacionar campañas que puedan haber impactado negativamente en el consentimiento para reducir de forma proactiva la frecuencia de esas campañas.
- **Superposición de consentimiento** utiliza la superposición entre canales de consentimiento para ofrecer mensajes personalizados y coherentes en varios canales para los clientes que han aceptado varios canales. Los especialistas en marketing pueden priorizar y asignar recursos a ciertos canales en los que un mayor grado de consentimiento y mensajería personalizada podría interesar a los clientes y generar tasas de respuesta más altas.

## Creación de audiencias consentidas {#create-consent-audiences}

Para crear un panel de consentimiento, primero debe crear una audiencia de todos los perfiles que han aceptado contactar. Para navegar al Generador de segmentos de Real-time Customer Data Platform, seleccione **[!UICONTROL Audiencias]** en la navegación izquierda de la interfaz de usuario de Platform. Desde el [!UICONTROL Cliente] de la pestaña [!UICONTROL Audiencias] panel, seleccione **[!UICONTROL Crear audiencia]** en la parte superior derecha de la vista, **[!UICONTROL Generar reglas]**.

![El [!UICONTROL Audiencias] panel con [!UICONTROL Cliente], [!UICONTROL Audiencias], y [!UICONTROL Crear segmento] resaltado.](../images/insights-use-cases/consent-analysis/create-audience.png)

Aparecerá el Generador de segmentos. A continuación, seleccione **[!UICONTROL Perfil individual de XDM]** en las opciones disponibles. Consulte la documentación para obtener más información sobre [lienzo del generador de reglas](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![El Generador de segmentos con [!UICONTROL Perfil individual de XDM] carpeta de atributos resaltada.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Busque los atributos de consentimiento de las opciones disponibles. Seleccionar **[!UICONTROL Consentimientos y preferencias]**.

>[!NOTE]
>
>Si ha mantenido su consentimiento de usuario en un atributo diferente al grupo de campos Adobe recomendado, debe seleccionar esos atributos en lugar de los que se muestran a continuación.

Encontrará más información en la [gestión del consentimiento en la segmentación](../../segmentation/consents.md#handling-consent-in-segmentation) documentación.

![El Generador de segmentos con [!UICONTROL Consentimiento y preferencias] carpeta de atributos resaltada.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

Se muestran las distintas opciones de consentimiento y preferencia. Como esta demostración se centra en el consentimiento para contactar con a través de varios canales de marketing, seleccione **[!UICONTROL Preferencias de marketing]**.

![El Generador de segmentos con [!UICONTROL Preferencias de marketing] carpeta resaltada.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

Se muestra la lista de preferencias de marketing. Aunque este caso de uso de ejemplo se centra en el correo electrónico, los SMS y las llamadas, puede generar perspectivas para cualquier otra combinación o para todas las opciones. Para cada uno de los canales, realice los siguientes pasos para crear una audiencia.

Para empezar a configurar una audiencia, seleccione **[!UICONTROL Recibir SMS]** / **[!UICONTROL Recibir correo electrónico]** / **[!UICONTROL Recibir llamadas]**.

![Los canales de contacto disponibles para marketing se resaltan en el generador de audiencias.](../images/insights-use-cases/consent-analysis/channels.png)

El [!UICONTROL Suscripciones] carpeta aparece. De las opciones disponibles, seleccione y arrastre el **[!UICONTROL Valor de opción]** al panel central y, a continuación, seleccione el valor deseado en la lista desplegable. En este caso, seleccione **Sí (adhesión)**. A continuación, asigne un nombre a la audiencia según sus necesidades comerciales y proporcione una descripción fácil de usar.

>[!NOTE]
>
>Hay un límite flexible en el número de audiencias que se recomienda crear. Encontrará más información en la [documentación sobre protecciones de segmentación](../../profile/guardrails.md#segmentation-guardrails).

![El [!UICONTROL Valor de opción] con el atributo [!UICONTROL Sí (adhesión)] valor resaltado en el generador de segmentos. También se resaltan el nombre y la descripción de la audiencia.](../images/insights-use-cases/consent-analysis/choice-value.png)

Después de crear las audiencias necesarias, se enumeran en la [!UICONTROL Audiencias] [!UICONTROL Examinar] pestaña.

>[!NOTE]
>
>Al crear una audiencia, debe esperar a que se complete el trabajo de segmentación por lotes antes de que los datos estén disponibles para empezar a crear el panel de consentimiento. La segmentación por lotes describe el proceso de mover todos los datos de perfil a la vez a través de las definiciones de segmentos para producir las audiencias correspondientes. Una vez creada, esta audiencia se guarda y almacena para que la exporte y utilice. Los segmentos por lotes se evalúan automáticamente cada 24 horas.

## Consumir perspectivas {#consume-insights}

Adobe ha creado varias perspectivas que están disponibles automáticamente en los paneles Perfiles, Audiencias y Destinos. Cualquier audiencia que cree se puede utilizar automáticamente con estas perspectivas preconfiguradas. Consulte la documentación del widget estándar para obtener una lista de las perspectivas disponibles en la [Perfiles](../guides/profiles.md#standard-widgets), [Audiencias](../guides/audiences.md#standard-widgets), y [Destinos](../guides/destinations.md) paneles.

## Superposición de audiencias {#audience-overlap}

Para revisar la superposición entre dos audiencias de consentimiento cualesquiera, añada la variable [!UICONTROL Superposición de audiencias por política de combinación] Vaya al panel Perfiles y seleccione las audiencias que desee en los menús desplegables. Consulte la documentación para obtener instrucciones sobre cómo agregar un widget al tablero. [*Superposición de audiencias por política de combinación*](../guides/profiles.md#audience-overlap-by-merge-policy) para obtener más información sobre la perspectiva.

<!-- Image needs updating to night mode -->

![El panel Perfiles con el widget Superposición de audiencias por política de combinación resaltado. El widget visualiza las superposiciones entre dos audiencias de consentimiento.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

Puede ver la superposición de todas las audiencias en las que los usuarios han aceptado recibir llamadas entre todas las demás audiencias, con el informe Superposición de audiencias en el panel Audiencias. Para ver la superposición de audiencias de consentimiento, vaya primero a la [!UICONTROL Audiencias] [!UICONTROL Información general] pestaña. A partir de ahí, puede agregar la variable [!UICONTROL Informe de superposición de audiencia] al tablero Audiencias. Una vez creado el widget, seleccione la **[!UICONTROL El usuario aceptó las llamadas]** audiencia del menú desplegable información general de audiencia en la parte superior de la página. A continuación, seleccione **[!UICONTROL Ver más]** en el widget Informe de superposición de audiencias para ver hasta 50 de las superposiciones principales y hasta 50 de las superposiciones menos importantes con respecto al segmento seleccionado.

<!-- Image needs updating to night mode -->

![El tablero Audiencias con el widget Informe de superposición de audiencias mostrado. El usuario aceptó las llamadas de audiencia como audiencia de comparación, y el vínculo Ver más aparece resaltado.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

El cuadro de diálogo Informe de superposición de audiencias se amplía para mostrar datos adicionales de superposición de audiencias.

<!-- Image needs updating to night mode -->

![Informe de superposición de audiencias en el que se resalta la audiencia de correo electrónico consentida por los usuarios.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendencias de tamaño de audiencia {#audience-size-trends}

Cuando crea una audiencia basada en el consentimiento, la tendencia es automática hasta 12 meses desde la fecha de creación de la audiencia. Para tener una tendencia funcional del consentimiento del cliente, agregue los siguientes widgets al [!UICONTROL Segmentos] [!UICONTROL Información general] página. Estas perspectivas ofrecen un poderoso medio para rastrear cómo su consentimiento está cambiando con el tiempo. Incluso se correlacionan con cualquier campaña que ejecute en paralelo que pueda afectar positiva o negativamente al consentimiento. Las descripciones ofrecidas para estos widgets se aplican a un caso de uso de consentimiento.

- [Tendencia de tamaño de audiencia](../guides/audiences.md#audience-size-trend): este widget ofrece una forma de rastrear cómo ha cambiado su consentimiento respectivo con el paso del tiempo.
- [Tendencia de cambio de tamaño de audiencia](../guides/audiences.md#audience-size-change-trend): este widget rastrea cómo ha cambiado el consentimiento del cliente diariamente. Por ejemplo, si el recuento del consentimiento del cliente disminuyó en 100 000, puede ver cómo se produjo ese cambio diariamente.
- [Tendencia del tamaño de la audiencia por identidad](../guides/audiences.md#audience-size-trend-by-identity): con este widget puede rastrear cómo ha cambiado su respectivo consentimiento con el paso del tiempo, pero aún más filtrado por una identidad específica, como un correo electrónico.

<!-- Image needs updating to night mode -->

![El panel Audiencias con la tendencia de tamaño de audiencia, la tendencia de tamaño de audiencia por identidad y el widget de tendencia de cambio de tamaño de audiencia mostrado. Se resalta la audiencia de correo electrónico de Usuarios consentidos.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Panel de información general de audiencias {#audiences-overview-dashboard}

Después de crear una audiencia relacionada con el consentimiento, como &quot;Usuarios con consentimiento para SMS&quot;, puede ver información de consentimiento personalizada clave sobre su audiencia añadiendo los widgets adecuados al panel Información general de audiencias. Vaya a [!UICONTROL Audiencias] [!UICONTROL Información general] y añada los widgets seleccionados desde la biblioteca de widgets. Cualquier widget que se añada a la vista del tablero se puede cambiar de tamaño y mover utilizando el [!UICONTROL Modificar tablero] función. La vista personalizada puede contener perspectivas como la tendencia a lo largo del tiempo (hasta 12 meses), la superposición con otras audiencias y la composición de identidad de la audiencia. A continuación se muestra una vista de ejemplo.

![El panel de audiencias con el consentimiento de los usuarios para la audiencia de SMS se resalta en el menú desplegable de audiencia global.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Paneles definidos por el usuario {#usr-defined-dashboards}

También puede crear sus propios widgets con paneles definidos por el usuario. La creación de su propio widget le proporciona un control completo sobre el tipo de widget, junto con flexibilidad para agregar filtros y mucho más, directamente en Adobe Real-Time CDP.

Por ejemplo, si desea analizar la tendencia de varias audiencias de consentimiento en el mismo gráfico, de modo que pueda ver con el paso del tiempo cómo ha cambiado cada una de las preferencias de consentimiento. Este tipo de visualización es posible con paneles definidos por el usuario en pasos mínimos y una configuración única. Primero, seleccione **[!UICONTROL Paneles]** en el panel de navegación izquierdo. El [!UICONTROL Paneles] espacio de trabajo. A continuación seleccione **[!UICONTROL Crear tablero]**. Instrucciones completas sobre cómo [crear un tablero y un widget personalizado](../user-defined-dashboards.md) se encuentra en la guía de paneles definida por el usuario.

![Espacio de trabajo de paneles con paneles y Crear panel resaltados.](../images/user-defined-dashboards/create-dashboard.png)

Cuando usted [seleccione el modelo de datos](../user-defined-dashboards.md#select-data-model) en el compositor de widgets, seleccione `CDPInsights` seguido de **[!UICONTROL Siguiente]**. El [!UICONTROL Seleccionar tabla] aparece el cuadro de diálogo.

![El cuadro de diálogo Seleccionar modelo de datos con el modelo CDPInsights resaltado.](../images/user-defined-dashboards/select-data-model-dialog.png)

La vista siguiente muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione el `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![El cuadro de diálogo Seleccionar tabla con la tabla &quot;adwh_fact_profile_by_segment_and_namespace_trendlines&quot; resaltada.](../images/insights-use-cases/consent-analysis/select-table.png)

Una vez que el compositor de widgets se rellene con los datos de la tabla seleccionada, realice los pasos siguientes:

- [Buscar [!UICONTROL Atributos]](../user-defined-dashboards.md#add-filter-attributes) para `[!UICONTROL date]`, luego use el icono + para agregar `[!UICONTROL date]` al eje X desde el menú desplegable.
  ![Compositor de widgets con el icono del complemento y el menú desplegable resaltados.](../images/user-defined-dashboards/attributes-dropdown.png)
- Buscar [!UICONTROL Atributos] para `[!UICONTROL count_of_profiles]`, luego use el icono + para agregar `[!UICONTROL count_of_profiles]` al eje Y desde el menú desplegable.
- Seleccione el `...` (elipses) en el icono [!UICONTROL Eje Y] y, a continuación, seleccione el [!UICONTROL SUM] función de agregado del menú desplegable.
  ![El widget de tendencias de consentimiento del compositor de widgets con el modelo de datos, la tabla, el menú desplegable del eje Y y la función SUMA resaltadas. ](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Seleccione el [!UICONTROL Marcas] y cambie el tipo de gráfico a [!UICONTROL Línea].
- Buscar [!UICONTROL Atributos] para el `[!UICONTROL segment_name]`, luego use el icono + para agregar `segment_name` as a [!UICONTROL Filtrar] en el menú desplegable. El [!UICONTROL Filtro: Segment_name] aparece el cuadro de diálogo. Seleccione las audiencias creadas anteriormente relacionadas con el consentimiento. Para este ejemplo, seleccione **[!UICONTROL Usuarios que aceptaron llamadas]**, **[!UICONTROL Usuarios con consentimiento para SMS]**, y **[!UICONTROL Usuarios que aceptaron enviar correo electrónico]**, seguido de **[!UICONTROL Aplicar]**.
- Buscar [!UICONTROL Atributos] para `[!UICONTROL segment_name]`, luego seleccione el icono + para agregar `segment_name` as a [!UICONTROL Color] en el menú desplegable.
- Abrir [el [!UICONTROL Propiedades] panel](../user-defined-dashboards.md#widget-properties) y proporcionar un [!UICONTROL Título del widget] y [!UICONTROL Etiqueta del eje].
  ![Compositor de widgets con el icono de propiedades y el título de widget resaltados.](../images/user-defined-dashboards/properties-panel.png)
- Seleccionar **[!UICONTROL Guardar y cerrar]** para confirmar la configuración.

>[!TIP]
>
>Ahora puede cambiar el tamaño del widget o moverlo al tamaño y la posición deseados antes de guardar el tablero.


La siguiente imagen muestra cómo aparece el widget terminado y otras perspectivas personalizadas potenciales. Para obtener más información sobre los tipos de widgets que se pueden crear, consulte la [documentación del modelo de datos](../cdp-insights-data-model.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![El widget personalizado de tendencias de consentimiento terminado.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Políticas de consentimiento de seguimiento {#consent-policies}

Los paneles de consentimiento que cree capturarán el **solo distribución de atributos de consentimiento y preferencia**.

>[!NOTE]
>
>Para clientes de **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad**, estos paneles **no** reflejar cualquier seguimiento de las directivas de consentimiento. El seguimiento disponible incluye el número de directivas creadas, habilitadas y el impacto en el abono a audiencias.

## Pasos siguientes

Al leer este documento, ha aprendido a crear paneles para obtener una vista completa de las preferencias de consentimiento del cliente mediante perspectivas de Real-Time CDP. Este documento muestra cómo Real-Time CDP proporciona una solución sólida para el panorama actual centrado en la privacidad, donde la recopilación, segmentación, análisis y campañas de marketing personalizadas basadas en datos de consentimiento son cruciales para los especialistas en marketing.
