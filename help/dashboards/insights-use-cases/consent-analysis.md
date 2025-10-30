---
title: Análisis de consentimiento y seguimiento
description: Obtenga información sobre cómo crear un panel de análisis de consentimiento para rastrear las tendencias del consentimiento del usuario a lo largo del tiempo.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# Análisis y seguimiento del consentimiento

En el panorama de marketing actual, debe comprender y respetar las preferencias de consentimiento del cliente. Adobe Real-Time Customer Data Platform permite a los especialistas en marketing analizar el consentimiento de los clientes para generar confianza, cumplir con las normas de privacidad y ofrecer experiencias más personalizadas.

Este documento detalla cómo crear un panel de consentimiento para varios casos de uso de marketing para datos de Real-Time CDP. En concreto, se centra en cómo crear una audiencia con los atributos adecuados para sus necesidades comerciales y luego consumir las perspectivas mediante el uso de widgets preconfigurados en la interfaz de usuario de Adobe Experience Platform. También se presenta un método alternativo para crear su propio widget personalizado con la función de paneles definida por el usuario.

## Casos de uso {#use-cases}

Los casos de uso cubiertos en esta guía son las tendencias de consentimiento y la superposición de consentimiento.

- **Tendencia del consentimiento** registra la tendencia del consentimiento del usuario a lo largo del tiempo. El análisis de los cambios de preferencias de consentimiento ayuda a los especialistas en marketing a planificar y ejecutar campañas que se adapten a esos cambios de preferencias de usuario. Por ejemplo, es posible que desee ejecutar campañas educativas dirigidas, campañas de transparencia y confianza o campañas de incentivos para impulsar las opciones de consentimiento. También puede correlacionar campañas que puedan haber impactado negativamente en el consentimiento para reducir de forma proactiva la frecuencia de esas campañas.
- **Superposición de consentimiento** utiliza la superposición entre canales de consentimiento para ofrecer mensajes personalizados y coherentes en varios canales para los clientes que han dado su consentimiento a varios canales. Los especialistas en marketing pueden priorizar y asignar recursos a ciertos canales en los que un mayor grado de consentimiento y mensajería personalizada podría interesar a los clientes y generar tasas de respuesta más altas.

## Creación de audiencias consentidas {#create-consent-audiences}

Para crear un panel de consentimiento, primero debe crear una audiencia de todos los perfiles que han aceptado contactar. Para ir al Generador de segmentos de Real-Time Customer Data Platform, seleccione **[!UICONTROL Audiences]** en el panel de navegación izquierdo de la interfaz de usuario de Experience Platform. En la ficha [!UICONTROL Customer] del panel [!UICONTROL Audiences], seleccione **[!UICONTROL Create audience]** en la parte superior derecha de la vista y, a continuación, **[!UICONTROL Build rules]**.

![Se resaltó el panel [!UICONTROL Audiences] con [!UICONTROL Customer], [!UICONTROL Audiences] y [!UICONTROL Create segment].](../images/insights-use-cases/consent-analysis/create-audience.png)

Aparecerá el Generador de segmentos. A continuación, seleccione **[!UICONTROL XDM Individual Profile]** de las opciones disponibles. Consulte la documentación para obtener más información sobre el [lienzo del generador de reglas](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![Generador de segmentos con la carpeta de atributos [!UICONTROL XDM Individual Profile] resaltada.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Busque los atributos de consentimiento de las opciones disponibles. Seleccione **[!UICONTROL Consents and Preferences]**.

>[!NOTE]
>
>Si ha mantenido su consentimiento de usuario en un atributo diferente al grupo de campos recomendado por Adobe, debe seleccionar esos atributos en lugar de los que se muestran a continuación.

Encontrará más información sobre la [administración del consentimiento en la documentación de segmentation](../../segmentation/tutorials/consents.md#handling-consent-in-segmentation).

![Generador de segmentos con la carpeta de atributos [!UICONTROL Consent and Preferences] resaltada.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

Se muestran las distintas opciones de consentimiento y preferencia. Como esta demostración se centra en el consentimiento para contactar con a través de varios canales de marketing, seleccione **[!UICONTROL Marketing Preferences]**.

![Generador de segmentos con la carpeta [!UICONTROL Marketing Preferences] resaltada.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

Se muestra la lista de preferencias de marketing. Aunque este caso de uso de ejemplo se centra en el correo electrónico, los SMS y las llamadas, puede generar perspectivas para cualquier otra combinación o para todas las opciones. Para cada uno de los canales, realice los siguientes pasos para crear una audiencia.

Para comenzar a configurar una audiencia, seleccione **[!UICONTROL Receive SMS]** / **[!UICONTROL Receive email]** / **[!UICONTROL Receive calls]**.

![Los canales de contacto de marketing disponibles están resaltados en el generador de audiencias.](../images/insights-use-cases/consent-analysis/channels.png)

Aparecerá la carpeta [!UICONTROL Subscriptions]. De las opciones disponibles, seleccione y arrastre el atributo **[!UICONTROL Choice Value]** al panel central y, a continuación, seleccione el valor que desee en la lista desplegable. En este caso, seleccione **Sí (adhesión)**. A continuación, asigne un nombre a la audiencia según sus necesidades comerciales y proporcione una descripción fácil de usar.

>[!NOTE]
>
>Hay un límite flexible en el número de audiencias que se recomienda crear. Encontrará más información en la [documentación de protecciones de segmentación](../../profile/guardrails.md#segmentation-guardrails).

![Atributo [!UICONTROL Choice Value] con el valor [!UICONTROL Yes (opt-in)] resaltado en el generador de segmentos. También se resaltan el nombre y la descripción de la audiencia.](../images/insights-use-cases/consent-analysis/choice-value.png)

Después de crear las audiencias necesarias, se enumeran en la pestaña [!UICONTROL Audiences] [!UICONTROL Browse].

>[!NOTE]
>
>Al crear una audiencia, debe esperar a que se complete el trabajo de segmentación por lotes antes de que los datos estén disponibles para empezar a crear el panel de consentimiento. La segmentación por lotes describe el proceso de mover todos los datos de perfil a la vez a través de las definiciones de segmentos para producir las audiencias correspondientes. Una vez creada, esta audiencia se guarda y almacena para que la exporte y utilice. Los segmentos por lotes se evalúan automáticamente cada 24 horas.

## Consumir perspectivas {#consume-insights}

Adobe ha creado varias perspectivas que están disponibles automáticamente en los paneles Perfiles, Audiencias y Destinos. Cualquier audiencia que cree se puede utilizar automáticamente con estas perspectivas preconfiguradas. Consulte la documentación del widget estándar para obtener una lista de las perspectivas disponibles en los paneles de [Perfiles](../guides/profiles.md#standard-widgets), [Audiencias](../guides/audiences.md#standard-widgets) y [Destinos](../guides/destinations.md).

## Solapamiento de público {#audience-overlap}

Para revisar la superposición entre dos audiencias de consentimiento cualesquiera, agregue [!UICONTROL Audience overlap by merge policy] a su panel Perfiles y seleccione las audiencias que desee en los menús desplegables. Consulte la documentación para obtener instrucciones sobre cómo agregar un widget al tablero sobre la [*superposición de audiencias mediante la política de combinación*](../guides/profiles.md#audience-overlap-by-merge-policy) para obtener más información sobre insight.

<!-- Image needs updating to night mode -->

![El panel Perfiles con la superposición de Audiencias por widget de política de combinación resaltado. El widget visualiza las superposiciones entre dos audiencias de consentimiento.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

Puede ver la superposición de todas las audiencias en las que los usuarios han aceptado recibir llamadas entre todas las demás audiencias, con el informe Superposición de audiencias en el panel Audiencias. Para ver la superposición de audiencias de consentimiento, primero vaya a la pestaña [!UICONTROL Audiences] [!UICONTROL Overview]. Desde allí, puede agregar el widget [!UICONTROL Audience overlap report] al panel Audiencias. Una vez creado el widget, seleccione la audiencia **[!UICONTROL User consented to calls]** en el menú desplegable de información general de audiencia en la parte superior de la página. A continuación, seleccione **[!UICONTROL View more]** en el widget de informe de superposición de audiencia para ver hasta 50 de las superposiciones principales y hasta 50 de las superposiciones menos importantes en relación con el segmento seleccionado.

<!-- Image needs updating to night mode -->

![Panel de audiencias con el widget de informe de superposición de audiencias mostrado. El usuario aceptó las llamadas a la audiencia como audiencia de comparación y el vínculo Ver más se resaltan.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

El cuadro de diálogo Informe de superposición de audiencias se amplía para mostrar datos adicionales de superposición de audiencias.

<!-- Image needs updating to night mode -->

![Informe de superposición de audiencias en el que los usuarios aceptaron resaltar la audiencia del correo electrónico.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendencias de tamaño de público {#audience-size-trends}

Cuando crea una audiencia basada en el consentimiento, la tendencia es automática hasta 12 meses desde la fecha de creación de la audiencia. Para tener una tendencia funcional del consentimiento del cliente, agregue los siguientes widgets a la página [!UICONTROL Segments] [!UICONTROL Overview]. Estas perspectivas ofrecen un poderoso medio para rastrear cómo su consentimiento está cambiando con el tiempo. Incluso se correlacionan con cualquier campaña que ejecute en paralelo que pueda afectar positiva o negativamente al consentimiento. Las descripciones ofrecidas para estos widgets se aplican a un caso de uso de consentimiento.

- [Tendencia de tamaño de audiencia](../guides/audiences.md#audience-size-trend): este widget ofrece una forma de rastrear cómo ha cambiado su consentimiento respectivo con el paso del tiempo.
- [Tendencia de cambio de tamaño de audiencia](../guides/audiences.md#audience-size-change-trend): este widget rastrea cómo ha cambiado diariamente el consentimiento del cliente. Por ejemplo, si el recuento del consentimiento del cliente disminuyó en 100 000, puede ver cómo se produjo ese cambio diariamente.
- [Tendencia del tamaño de la audiencia según la identidad](../guides/audiences.md#audience-size-trend-by-identity): con este widget puede rastrear cómo ha cambiado su respectivo consentimiento con el paso del tiempo, pero aún más filtrado por una identidad específica, como un correo electrónico.

<!-- Image needs updating to night mode -->

![Se muestra el panel Audiencias con la tendencia de tamaño de audiencia, la tendencia de tamaño de audiencia por identidad y el widget de tendencia de cambio de tamaño de audiencia. Se resaltó la audiencia de usuarios que aceptaron recibir correo electrónico.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Panel de información general de audiencias {#audiences-overview-dashboard}

Después de crear una audiencia relacionada con el consentimiento, como &quot;Usuarios con consentimiento para SMS&quot;, puede ver información de consentimiento personalizada clave sobre su audiencia añadiendo los widgets adecuados al panel Información general de audiencias. Vaya a [!UICONTROL Audiences] [!UICONTROL Overview] y agregue los widgets seleccionados desde la biblioteca de widgets. Cualquier widget agregado a su vista del tablero se puede cambiar de tamaño y mover usando la función [!UICONTROL Modify dashboard]. La vista personalizada puede contener perspectivas como la tendencia a lo largo del tiempo (hasta 12 meses), la superposición con otras audiencias y la composición de identidad de la audiencia. A continuación se muestra una vista de ejemplo.

![El tablero de audiencias con los usuarios que aceptaron la audiencia de SMS está resaltado en el menú desplegable de audiencia global.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Paneles de control definidos por el usuario {#usr-defined-dashboards}

También puede crear sus propios widgets con paneles definidos por el usuario. La creación de su propio widget le proporciona un control completo sobre el tipo de widget, junto con flexibilidad para agregar filtros y mucho más, directamente en Adobe Real-Time CDP.

Por ejemplo, si desea analizar la tendencia de varias audiencias de consentimiento en el mismo gráfico, de modo que pueda ver con el paso del tiempo cómo ha cambiado cada una de las preferencias de consentimiento. Este tipo de visualización es posible con paneles definidos por el usuario en pasos mínimos y una configuración única. En primer lugar, seleccione **[!UICONTROL Dashboards]** en el panel de navegación izquierdo. Aparece el área de trabajo [!UICONTROL Dashboards]. Luego seleccione **[!UICONTROL Create dashboard]**. Encontrará instrucciones completas sobre cómo [crear un tablero y un widget personalizado](../standard-dashboards.md) en la guía de tableros definida por el usuario.

![Espacio de trabajo de paneles con paneles y Crear panel resaltados.](../images/standard-dashboards/create-dashboard.png)

Cuando [seleccione su modelo de datos](../standard-dashboards.md#select-data-model) en el compositor de widgets, seleccione `CDPInsights` seguido de **[!UICONTROL Next]**. Aparecerá el cuadro de diálogo [!UICONTROL Select table].

![Cuadro de diálogo Seleccionar modelo de datos con el modelo CDPInsights resaltado.](../images/standard-dashboards/select-data-model-dialog.png)

La vista siguiente muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione el `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![Se resaltó el cuadro de diálogo Seleccionar tabla con la tabla &#39;adwh_fact_profile_by_segment_and_namespace_trendlines&#39;.](../images/insights-use-cases/consent-analysis/select-table.png)

Una vez que el compositor de widgets se rellene con los datos de la tabla seleccionada, realice los pasos siguientes:

- [Busque [!UICONTROL Attributes]](../standard-dashboards.md#add-filter-attributes) `[!UICONTROL date]` y, a continuación, utilice el icono + para agregar el atributo `[!UICONTROL date]` al eje X desde el menú desplegable.
  ![El compositor de widgets con el menú desplegable y el icono de complemento resaltados.](../images/standard-dashboards/attributes-dropdown.png)
- Busque [!UICONTROL Attributes] por `[!UICONTROL count_of_profiles]` y, a continuación, utilice el icono + para agregar el atributo `[!UICONTROL count_of_profiles]` al eje Y desde el menú desplegable.
- Seleccione el icono `...` (elipses) en el campo [!UICONTROL Y-axis] y, a continuación, seleccione la función de agregado [!UICONTROL SUM] en el menú desplegable.
  ![Widget de tendencias de consentimiento del compositor de widgets con el modelo de datos, la tabla, el menú desplegable del eje Y y la función SUMA resaltados.](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Seleccione el menú desplegable [!UICONTROL Marks] y cambie el tipo de gráfico a [!UICONTROL Line].
- Busque [!UICONTROL Attributes] para `[!UICONTROL segment_name]` y, a continuación, utilice el icono + para agregar `segment_name` como [!UICONTROL Filter] desde el menú desplegable. Aparecerá el cuadro de diálogo [!UICONTROL Filter: Segment_name]. Seleccione las audiencias creadas anteriormente relacionadas con el consentimiento. Para este ejemplo, seleccione **[!UICONTROL Users Consented to Calls]**, **[!UICONTROL Users Consented to SMS]** y **[!UICONTROL Users Consented to Email]**, seguidos de **[!UICONTROL Apply]**.
- Busque [!UICONTROL Attributes] para `[!UICONTROL segment_name]` y, a continuación, seleccione el icono + para agregar `segment_name` como [!UICONTROL Color] en el menú desplegable.
- Abra [el panel [!UICONTROL Properties]](../standard-dashboards.md#widget-properties) y proporcione [!UICONTROL Widget title] y [!UICONTROL Axis label] adecuados.
  ![Compositor de widgets con el icono de propiedades y el título de widget resaltados.](../images/standard-dashboards/properties-panel.png)
- Seleccione **[!UICONTROL Save and close]** para confirmar la configuración.

>[!TIP]
>
>Ahora puede cambiar el tamaño del widget o moverlo al tamaño y la posición deseados antes de guardar el tablero.


La siguiente imagen muestra cómo aparece el widget terminado y otras perspectivas personalizadas potenciales. Para obtener más información sobre los tipos de widgets que se pueden crear, consulte la [documentación del modelo de datos](../data-models/cdp-insights-data-model-b2c.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![El widget de tendencias de consentimiento personalizado terminado.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Políticas de consentimiento de seguimiento {#consent-policies}

Los paneles de consentimiento que cree capturarán únicamente la **distribución de atributos de consentimiento y preferencia**.

>[!NOTE]
>
>Para los clientes de **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, estos paneles **no** reflejan ningún seguimiento de las directivas de consentimiento. El seguimiento disponible incluye el número de directivas creadas, habilitadas y el impacto en el abono a audiencias.

## Próximos pasos

Al leer este documento, ha aprendido a crear paneles para obtener una vista completa de las preferencias de consentimiento del cliente mediante perspectivas de Real-Time CDP. Este documento muestra cómo Real-Time CDP proporciona una solución sólida para el panorama actual centrado en la privacidad, donde la recopilación, segmentación, análisis y campañas de marketing personalizadas basadas en datos de consentimiento son cruciales para los especialistas en marketing.
