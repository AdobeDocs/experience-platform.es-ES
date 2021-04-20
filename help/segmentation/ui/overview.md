---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía del usuario;guía de interfaz de usuario;guía de interfaz de usuario de segmentación;generador de segmentos;generador de segmentos;se ha realizado;existente;existe;existe; existe; existe;
solution: Experience Platform
title: Guía de la interfaz de usuario del servicio de segmentación
topic: ui guide
description: El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario para crear y administrar definiciones de segmentos.
translation-type: tm+mt
source-git-commit: 1634466d3a1d8eadc4c98bb93214d8772b6a47a3
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---


# Guía de la interfaz de usuario del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] proporciona una interfaz de usuario para crear y administrar definiciones de segmentos.

## Primeros pasos

Para trabajar con definiciones de segmentos es necesario conocer los distintos [!DNL Experience Platform] servicios involucrados en la segmentación. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] permite dividir los datos almacenados en en  [!DNL Experience Platform] que se relacionan con individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permite la creación de perfiles de clientes al unir identidades de fuentes de datos dispares que se están incorporando en  [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

También es importante conocer dos términos clave que se utilizan en este documento y comprender la diferencia entre ellos:
- **Definición** de segmento: Conjunto de reglas utilizado para describir características o comportamientos clave de una audiencia objetivo.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Información general

En la [[!DNL Experience Platform] UI](http://platform.adobe.com/), seleccione **[!UICONTROL Segments]** en el panel de navegación izquierdo para abrir la pestaña **[!UICONTROL Overview]**. Esta ficha contiene vínculos a documentación y vídeos para ayudarle a comprender y comenzar a trabajar con segmentos.

![](../images/ui/overview/segment-overview.png)

## Examinar

Seleccione la pestaña **[!UICONTROL Browse]** para ver una lista de todas las definiciones de segmentos para su organización IMS.

![](../images/ui/overview/segment-browse-all.png)

Esta vista muestra información sobre la definición del segmento, incluido el desglose, la pérdida, el recuento de perfiles, el método de evaluación, la fecha de creación y la fecha de la última modificación.

El desglose muestra un gráfico de barras que resume el porcentaje de perfiles que pertenecen a cada uno de los siguientes estados: [!UICONTROL Entered], [!UICONTROL Realized] y [!UICONTROL Exiting].

![](../images/ui/overview/segment-browse-breakdown.png)

| Estado | Descripción |
| ------ | ----------- |
| Introducido | Un nuevo perfil dentro del segmento. |
| Realizado | Un perfil existente que se ha mantenido dentro del segmento. |
| Saliendo | Un perfil existente que abandona el segmento. |

La pérdida representa el porcentaje de perfiles que cambian dentro de una definición de segmento en comparación con la última vez que se ejecutó el trabajo del segmento, mientras que el recuento de perfiles representa el número total de perfiles que califican para el segmento.

El método de evaluación puede ser flujo continuo o por lotes. Los segmentos de transmisión se evalúan constantemente a medida que los datos entran en el sistema. Los segmentos por lotes se evalúan según una programación establecida.

![](../images/ui/overview/segment-browse-segments.png)

En la parte superior de la página hay opciones para agregar todos los segmentos a una programación y para crear un nuevo segmento.

Alternar **[!UICONTROL Add all segments to schedule]** habilitará la segmentación programada. Puede encontrar más información sobre la segmentación programada en la sección [segmentación programada de esta guía del usuario](#scheduled-segmentation).

Si selecciona **[!UICONTROL Create segment]**, se le dirigirá al Generador de segmentos. Para obtener más información sobre la creación de segmentos, lea la sección sobre la [creación de segmentos en la guía del usuario](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barra lateral derecha contiene información sobre todos los segmentos dentro de la organización IMS, que enumera el número total de segmentos, la última fecha de evaluación, la siguiente fecha de evaluación, así como un desglose de los segmentos por método de evaluación.

![](../images/ui/overview/segment-browse-segment-info.png)

Al seleccionar la fila de la definición del segmento, se proporciona un resumen de la definición del segmento, incluidas las opciones para editarlo o eliminarlo, la audiencia cualificada para el segmento, el tamaño total de audiencia, además del nombre, descripción, método de evaluación, fecha creada y fecha de la última modificación del segmento.

![](../images/ui/overview/segment-browse-details.png)

## Detalles de la definición del segmento {#segment-details}

Para ver más detalles sobre una definición de segmento específica, seleccione el nombre de un segmento en la pestaña **[!UICONTROL Browse]**.

Aparecerá la página de detalles del segmento. En la parte superior, hay un resumen de la definición del segmento, información sobre el tamaño de audiencia cualificado, así como los destinos para los que se activa el segmento.

![](../images/ui/overview/segment-details-summary.png)

### Resumen de segmentos

La sección **[!UICONTROL Segment summary]** proporciona información como el ID, el nombre, la descripción y los detalles de los atributos.

Además, se le da la opción de editar el segmento. Si selecciona **[!UICONTROL Edit segment]**, pasará al [!DNL Segment Builder]. Para obtener información más detallada sobre el uso del espacio de trabajo [!DNL Segment Builder], lea la [[!DNL Segment Builder] guía del usuario](./segment-builder.md).

### Audiencia total en el segmento

La sección **[!UICONTROL Total audience in segment]** muestra el número total de perfiles que cumplen los requisitos para el segmento.

Las estimaciones se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de 1 millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades, se utilizan 1 millón de entidades; y para más de 20 millones de entidades, se utiliza el 5% del total de entidades. Puede encontrar más información sobre la generación de estimaciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de segmentos.

### Destinos activados

La sección **[!UICONTROL Activated destinations]** muestra los destinos para los que se activa este segmento.

>[!NOTE]
>
> Los destinos son una función disponible con [!DNL Real-time Customer Data Platform] y le permiten exportar datos a plataformas externas. Para obtener más información sobre los destinos, lea la [información general sobre destinos](../../destinations/home.md). Para aprender a activar un segmento en un destino, lea la [guía sobre la activación de segmentos en un destino](../../destinations/ui/activate-destinations.md).

### Ejemplos de perfil

Debajo hay una muestra de perfiles que cumplen los requisitos para el segmento y detallan información que incluye el [!DNL Profile] ID, el nombre, los apellidos y el correo electrónico personal.

La forma en que se activa el muestreo de datos depende del método de ingesta.

Para la ingesta por lotes, el almacén de perfiles se analiza automáticamente cada quince minutos para ver si se ha introducido correctamente un nuevo lote desde que se ejecutó el último trabajo de muestreo. Si ese es el caso, el almacén de perfiles se analiza posteriormente para ver si ha habido al menos un cambio del 5 % en el número de registros. Si se cumplen estas condiciones, se activa un nuevo trabajo de muestreo.

Para la transmisión por secuencias, el almacén de perfiles se analiza automáticamente cada hora para ver si ha habido al menos un cambio del 5 % en el número de registros. Si se cumple esta condición, se activa un nuevo trabajo de muestreo.

El tamaño de la muestra depende del número total de entidades en el almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades en el almacén de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| de 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Para obtener información más detallada sobre cada [!DNL Profile], seleccione el [!DNL Profile] ID. Para obtener más información sobre los detalles de un perfil, lea la [[!DNL Real-time Customer Profile] guía del usuario](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Creación de un segmento {#create-segment}

Al seleccionar **[!UICONTROL Create segment]** en la esquina superior derecha, se abre el espacio de trabajo [!DNL Segment Builder], donde puede empezar a crear una definición de segmento.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] workspace

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de  [!DNL Profile] datos. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

Para obtener información más detallada sobre el uso del espacio de trabajo [!DNL Segment Builder], lea la [[!DNL Segment Builder] guía del usuario](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentación programada {#scheduled-segmentation}

Una vez creadas las definiciones de segmento, puede evaluarlas mediante una evaluación a petición o programada (continua). Evaluación significa mover [!DNL Real-time Customer Profile] datos a través de definiciones de segmento para producir las audiencias correspondientes. Una vez creadas, las audiencias se guardan y almacenan para que se puedan exportar con las API [!DNL Experience Platform].

La evaluación bajo demanda implica el uso de la API para realizar evaluaciones y crear audiencias según sea necesario, mientras que la evaluación programada (también conocida como &quot;segmentación programada&quot;) le permite crear una programación recurrente para evaluar definiciones de segmentos en un momento específico (a un máximo, una vez al día).

### Habilitar la segmentación programada {#enable-scheduled-segmentation}

La activación de las definiciones de segmentos para la evaluación programada se puede realizar mediante la interfaz de usuario o la API. En la interfaz de usuario, vuelva a la pestaña **[!UICONTROL Browse]** dentro de **[!UICONTROL Segments]** y active **[!UICONTROL Add all segments to schedule]**. Esto hará que todos los segmentos se evalúen según la programación establecida por su organización.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un entorno limitado único, no podrá utilizar la evaluación programada.

Actualmente, las programaciones solo se pueden crear mediante la API . Para obtener pasos detallados sobre la creación, edición y trabajo con programaciones mediante la API, siga el tutorial para evaluar y acceder a los resultados del segmento, específicamente la sección sobre [evaluación programada mediante la API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentación por transmisión {#streaming-segmentation}

La segmentación por transmisión es la capacidad de realizar segmentación en [!DNL Platform] en tiempo casi real, mientras se centra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos llegan a [!DNL Platform], lo que reduce la necesidad de programar y ejecutar trabajos de segmentación.

Puede encontrar más información sobre la segmentación de flujo en la [guía del usuario de segmentación de flujo](./streaming-segmentation.md).

>[!NOTE]
>
>Para que la segmentación de flujo continuo funcione, debe habilitar la segmentación programada para la organización. Para obtener más información sobre la activación de la segmentación programada, consulte [la sección de segmentación de flujo continuo en esta guía del usuario](#scheduled-segmentation).

## Segmentación de Edge {#edge-segmentation}

La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.

Puede encontrar más información sobre la segmentación de Edge en la [guía de la interfaz de segmentación de Edge](./edge-segmentation.md)

## Violaciones de políticas

>[!NOTE]
>
>Las infracciones de directiva solo se aplican si está creando un segmento que se ha asignado a un destino.

Una vez que haya terminado de crear su segmento, el control de datos de Adobe Experience Platform analizará el segmento para asegurarse de que no haya infracciones de directiva dentro del segmento. Consulte [[!DNL Data Governance] overview](../../data-governance/home.md) para obtener más información.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Pasos siguientes y recursos adicionales {#next-steps}

La interfaz de usuario [!DNL Segmentation Service] proporciona un flujo de trabajo enriquecido que le permite aislar las audiencias comercializables de los datos [!DNL Real-time Customer Profile].

Para obtener más información sobre [!DNL Segmentation Service], siga leyendo la documentación. Para aprender a utilizar la API [!DNL Segmentation Service], lea la [[!DNL Segmentation Service] guía para desarrolladores](../api/overview.md).
