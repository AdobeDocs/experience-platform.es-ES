---
title: Seguimiento de señales de datos para generar el valor de duración del cliente
description: Esta guía proporciona una demostración completa sobre cómo usar Distiller de datos y paneles definidos por el usuario con Real-time Customer Data Platform para medir y visualizar el valor de duración de los clientes.
source-git-commit: 2346f2d9450bc24e10419c09ee3dbcfb35bd5778
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# Seguimiento de señales de datos para generar el valor de duración de sus clientes

Puede usar Real-time Customer Data Platform para hacer un seguimiento del valor de duración (CLV) de los clientes y visualizar esa métrica con tableros definidos por el usuario. Mediante el uso de Distiller de datos y paneles definidos por el usuario, puede medir el valor que un cliente tiene para su empresa en toda su relación. Conocer el CLV puede ayudarle a desarrollar las estrategias de su empresa para adquirir nuevos clientes, conservando los existentes y manteniendo los márgenes de beneficio.

La siguiente infografía representa el ciclo de recopilación, manipulación, análisis y accionamiento de datos que genera datos de alto rendimiento para mejorar sus campañas de marketing.

![La infografía de viajes de ida y vuelta de datos desde la observación hasta el análisis y la acción.](../images/use-cases/infographic-use-case-cycle.png)

Este caso de uso completo demuestra cómo se pueden capturar y modificar las señales de datos para calcular el atributo derivado del valor de duración del cliente. Estos atributos derivados se pueden aplicar a los datos de perfil de Real-Time CDP y están disponibles para su uso con paneles definidos por el usuario para crear un tablero para el análisis de perspectiva. A través de Data Distiller, puede ampliar el modelo de datos de Real-Time CDP insights y utilizar el atributo derivado de CLV y las perspectivas de panel para crear un nuevo segmento y activarlo en un destino deseado. Estos segmentos se pueden utilizar para crear audiencias de alto rendimiento y potenciar la próxima campaña de marketing.

Esta guía está diseñada para ayudarle a comprender mejor su experiencia con los clientes mediante la medición de señales de datos en puntos de contacto clave que impulsan CLV e implementan un caso de uso similar en su entorno. El proceso completo se resume en la siguiente imagen.

![Una infografía de los pasos generales necesarios para utilizar el valor de duración del cliente.](../images/use-cases/implementation-steps.png)

## Primeros pasos {#getting-started}

Esta guía requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Servicio de consultas](../home.md): Proporciona una interfaz de usuario y una API RESTful donde puede utilizar consultas SQL para analizar y enriquecer los datos.
* [Servicio de segmentación](../../segmentation/home.md): Permite crear segmentos y generar audiencias a partir de los datos del perfil del cliente en tiempo real.

## Requisitos previos

Esta guía requiere que tenga la variable [Distiller de datos](../data-distiller/overview.md) SKU como parte de su oferta de paquetes. Si no está seguro de si tiene esto, póngase en contacto con su representante de servicios de Adobe.

## Crear un atributo derivado {#create-derived-attribute}

El primer paso para establecer el CLV es crear un atributo derivado de las señales de datos capturadas a partir de las acciones del usuario. Este caso de uso en particular se captura en un documento separado sobre un esquema de lealtad de aerolíneas. Consulte la guía para aprender a [utilice el servicio de consulta para crear atributos derivados basados en decimales y utilizarlos con los datos de perfil](./deciles-use-case.md). En el documento se proporcionan ejemplos y explicaciones completos que explican los siguientes pasos:

* Cree un esquema para permitir la acumulación de decimales.
* Utilice el servicio de consulta para crear deciles.
* Generar conjuntos de datos decimales.
* Habilite el esquema para utilizarlo en el perfil de cliente en tiempo real.
* Cree un área de nombres de identidad y marque como identificador principal.
* Cree una consulta para calcular los decimales durante un periodo retroactivo.

## Ampliación del modelo de datos de perspectivas y actualizaciones de la programación {#extend-data-model-and-set-refresh-schedule}

A continuación, debe crear un modelo de datos personalizado o ampliar un modelo de datos de Adobe Real-Time CDP existente para interactuar con sus perspectivas de informes de CLV. Consulte la documentación para aprender a [crear un modelo de datos de perspectivas de informes mediante Query Service para utilizarlo con datos de almacenamiento acelerados y paneles definidos por el usuario](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). El tutorial cubre los siguientes pasos:

* Cree un modelo para crear informes de perspectivas con Data Distiller.
* Cree tablas, relaciones y rellene datos.
* Consulte el modelo de datos de perspectivas de informes.
* Amplíe el modelo de datos con el modelo de datos de perspectivas de Real-Time CDP.
* Cree tablas de dimensión para ampliar el modelo de perspectivas de informes.
* Consulte el modelo de datos de perspectivas del almacén acelerado ampliado

Consulte la documentación del modelo de datos de Real-time Customer Data Platform Insights para obtener información sobre cómo [personalice las plantillas de consulta SQL para crear informes de Real-Time CDP para los casos de uso de los indicadores clave de rendimiento (KPI) y marketing](../../dashboards/cdp-insights-data-model.md).

Asegúrese de establecer una programación para actualizar el modelo de datos personalizado en una cadencia normal. Esto garantiza que los datos regresen como parte de la canalización de ingesta según sea necesario y rellena los tableros definidos por el usuario. Consulte la [guía de consultas de programación](../ui/query-schedules.md#create-schedule) para aprender a configurar su programación.

## Creación de un tablero para capturar perspectivas {#build-a-custom-dashboard}

Ahora que ha creado su modelo de datos personalizado, ya puede visualizar los datos con consultas personalizadas y tableros definidos por el usuario. Consulte la descripción general de los paneles definidos por el usuario para obtener instrucciones completas sobre cómo [crear un tablero personalizado](../../dashboards/user-defined-dashboards.md). La guía de la interfaz de usuario incluye detalles sobre:

* Cómo crear un widget.
* Cómo usar el compositor de utilidades.

A continuación se pueden ver ejemplos de utilidades CLV personalizadas que utilizan bloques decimales.

![Una colección de widgets CLTV personalizados basados en deciles.](../images/use-cases/deciles-user-defined-dashboard.png)

## Cree y active segmentos para crear audiencias de alto rendimiento {#create-and-activate-segments}

El siguiente paso es crear segmentos y generar audiencias a partir de los datos del perfil del cliente en tiempo real. Consulte la guía de la interfaz de usuario del Generador de segmentos para obtener información sobre cómo [crear y activar segmentos en Platform](../../segmentation/ui/segment-builder.md). La guía proporciona secciones sobre cómo:

* Cree definiciones de segmento mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
* Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
* Consulte las estimaciones de su audiencia potencial, lo que le permite ajustar las definiciones de segmentos según sea necesario.
* Habilite todas las definiciones de segmentos para la segmentación programada.
* Habilite definiciones de segmento especificadas para la segmentación de flujo continuo.

También hay un [tutorial de vídeo del generador de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) disponible para obtener más información.

## Activar el segmento para una campaña de correo electrónico {#activate-segment-for-campaign}

Una vez creado el segmento, está listo para activarlo en un destino. Platform admite una variedad de proveedores de servicios de correo electrónico (ESP) que le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales.

Marque la [información general sobre destinos de marketing por correo electrónico](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) para obtener una lista de los destinos admitidos a los que desea exportar los datos (por ejemplo, el [Oracle Eloqua](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) ).

## Ver los datos de análisis devueltos de la campaña {#post-campaign-data-analysis}

Los datos de las fuentes ahora pueden ser [procesado de forma incremental](../essential-concepts/incremental-load.md) como parte de una actualización programada del modelo de datos en el almacén de datos acelerado. Cualquier evento de respuesta de los clientes se puede ingerir en Adobe Experience Platform a medida que se produce o en lotes. El modelo de datos se puede actualizar una o varias veces al día según la configuración o los conectores de origen. Consulte la [información general sobre la API de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md) o [información general sobre la ingesta de transmisión](../../ingestion/streaming-ingestion/overview.md) para obtener más información.

Una vez actualizado el modelo de datos, los widgets de tablero personalizados proporcionan señales significativas que le permiten medir y visualizar el valor de duración de los clientes.

![Un widget personalizado para mostrar el número de correos electrónicos abiertos según su segmento y campaña de correo electrónico.](../images/use-cases/post-activation-and-email-response-kpis.png)

Se proporcionan diversas opciones de visualización para su análisis personalizado.

![El correo electrónico que abre el widget de bloques de campaña.](../images/use-cases/email-opened-by-campaign-buckets.png)

Estas perspectivas pueden, a su vez, ayudarle a desarrollar sus estrategias comerciales para campañas posteriores.

![Recopilación de cuatro widgets personalizados que detallan los resultados de la campaña de correo electrónico.](../images/use-cases/example-widgets.png)

## Pasos siguientes

Al leer este documento, debe comprender mejor cómo puede usar Real-time Customer Data Platform para rastrear y visualizar la métrica de valor de duración del cliente (CLV). Para obtener más información sobre los muchos casos de uso empresarial a los que se aplican mediante Query Service y el Experience Platform, se recomienda leer los siguientes documentos:

* [Ejemplo completo de un caso de uso de exploración abandonado que demuestra la versatilidad y las ventajas del servicio de consulta.](./abandoned-browse.md)
* [Cómo utilizar el servicio de consulta y el aprendizaje automático para determinar y filtrar la actividad de bots a partir del tráfico de visitantes de un sitio web en línea real](./bot-filtering.md)
* [Cómo realizar una coincidencia en los datos de Platform que combina resultados de varios conjuntos de datos al hacer coincidir aproximadamente una cadena de su elección.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
