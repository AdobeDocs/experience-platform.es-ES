---
title: Perspectivas personalizables
description: Obtenga información sobre los casos de uso, las funcionalidades esenciales y los pasos necesarios para desarrollar un panel de perspectivas personalizable con Data Distiller. Descubra cómo la capacidad Perspectivas personalizables de Data Distiller puede mejorar la transparencia y obtener perspectivas operativas en diferentes dimensiones, como perfiles, audiencias, campañas, recorridos, autorizaciones y consentimientos.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Perspectivas personalizables

Cree modelos de datos de informes personalizados para extraer perspectivas más profundas, optimizar estrategias y adaptar los análisis para satisfacer necesidades comerciales específicas con Perspectivas personalizables de Data Distiller. Utilice la capacidad Perspectivas personalizables para mejorar la transparencia y obtener perspectivas operativas de sus datos de Adobe Experience Platform en dimensiones como perfiles, audiencias, campañas, recorridos, autorizaciones y consentimientos. Esta capacidad proporciona una solución versátil y adaptable para adaptar los modelos de datos de creación de informes de su organización a las necesidades específicas de su empresa.

Hasta [visualizar sus perspectivas personalizables](../../../dashboards/data-distiller/overview.md) puede utilizar [modo query pro](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) para realizar análisis complejos con consultas SQL personalizadas y transformar los datos en gráficos fácilmente interpretables. Utilice el modo query pro para crear perspectivas y visualizaciones personalizadas en sus paneles y atender a audiencias técnicas y no técnicas descargando sus perspectivas como archivos CSV.

Este documento cubre los casos de uso, las funcionalidades esenciales y los pasos necesarios para desarrollar un panel de perspectivas personalizable con Data Distiller.

## Requisitos previos

Este tutorial utiliza paneles definidos por el usuario para visualizar datos del modelo de datos personalizado en la interfaz de usuario de Platform. Consulte la [documentación de paneles definidos por el usuario](../../../dashboards/user-defined-dashboards.md) para obtener más información sobre esta función.

## Introducción

El SKU de Data Distiller es necesario para crear un modelo de datos personalizado para las perspectivas de creación de informes y ampliar los modelos de datos de Real-Time CDP que contienen datos de Platform enriquecidos. Consulte la [empaquetado](../../packaging.md), [barandas](../../guardrails.md#query-accelerated-store), y  [licenciamiento](../../data-distiller/license-usage.md) la documentación relacionada con el SKU de Data Distiller. Si no tiene el SKU de Distiller de datos, póngase en contacto con el representante del servicio de atención al cliente de Adobe para obtener más información.

## Casos de uso de Perspectivas personalizables {#use-cases}

A continuación se muestran casos de uso comunes que se pueden abordar de forma eficaz mediante Perspectivas personalizables en Data Distiller.

### Transparencia del perfil y uso de audiencia {#usage-transparency}

**Reto:** Cómo desglosar los indicadores clave de rendimiento (KPI) según criterios específicos como unidades de negocio, estado de lealtad o valor de duración del cliente (CLTV).

**Solución de perspectivas personalizable:** Data Distiller permite la extensión de los modelos de datos de informes en Adobe Experience Platform, lo que facilita [la adición de atributos de perfil personalizados, como CLTV](../../use-cases/customer-lifetime-value.md) o estado de fidelidad.

### Seguimiento de anomalías de consentimiento {#consent-anomaly-tracking}

**Reto:** Cómo aplicar superposición de audiencias y tamaño de informes de línea de tendencia a atributos de consentimiento personalizados para canales como correo electrónico, SMS y teléfono.

**Solución de perspectivas personalizable:** El modelo de datos de creación de informes se puede ampliar para rastrear los cambios en las preferencias de consentimiento a lo largo del tiempo. Esto implica crear tablas de hechos y dimensiones adicionales para determinar las preferencias y la programación del consentimiento de tendencias [actualización de datos incremental](../../key-concepts/incremental-load.md).

### Optimizar estrategia de segmentación de audiencia {#optimize-audience-segmentation-strategy}

**Reto:** Cómo integrar las puntuaciones de tendencia generadas por modelos de Aprendizaje automático (ML) en sus informes de KPI de audiencia.

**Solución de perspectivas personalizable:** Data Distiller permite la inclusión de [puntuaciones de tendencia de modelos ML personalizados](../../use-cases/propensity-score.md), facilitando el cálculo de puntuaciones acumuladas en el nivel de audiencia. Estos datos se pueden registrar junto con los KPI estándar.

### Expansión de audiencia {#audience-expansion}

**Reto:** Obtenga algo más que recuentos de perfiles en informes de superposición de audiencias y obtenga datos demográficos o preferencias adicionales para guiar las estrategias de expansión de audiencias.

**Solución de perspectivas personalizable:** Al ampliar el modelo de datos de creación de informes, los usuarios pueden incorporar atributos de perfil adicionales, lo que enriquece el informe de superposición de audiencias con los datos demográficos y las preferencias relevantes.

## Funcionalidades clave para generar Perspectivas personalizables {#key-capabilities}

La siguiente ilustración resalta varias funciones esenciales para generar Perspectivas personalizables. Estas funciones incluyen:

1. **Visualizaciones de datos:** Incorporar elementos visuales como tendencias y gráficos de barras para obtener una vista completa de las tendencias de los datos.
1. **Creación de tableros:** Permite la creación de paneles personalizados adaptados a casos de uso específicos, lo que proporciona una experiencia de análisis más personalizada y dirigida.
1. **Modelado flexible de datos SQL:** Utilice un enfoque versátil de modelado de datos SQL que permita a los usuarios combinar y manipular diferentes conjuntos de datos sin problemas, mejorando la adaptabilidad y la profundidad analítica.
1. **Almacenamiento acelerado:** Implementación de un mecanismo de almacenamiento acelerado para ofrecer de forma eficaz perspectivas agregadas a través de SQL, lo que garantiza un acceso rápido y optimizado a la información valiosa.
1. **Conectividad de BI:** Facilita una integración perfecta con las herramientas de Business Intelligence (BI) más populares, como Power BI, Tableau, Looker y Apache Superset. Esta conectividad garantiza la compatibilidad con diversos entornos de BI, lo que ofrece a los usuarios la flexibilidad de utilizar la herramienta que elijan para realizar análisis e informes detallados.

![Representaciones visuales de las funcionalidades clave de las Perspectivas personalizables de Data Distiller.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Pasos para crear perspectivas personalizables {#steps-to-create}

Para desarrollar un panel de perspectivas personalizable dentro de Data Distiller, siga las instrucciones paso a paso a continuación.

1. **Exploración de consultas ad hoc:** Comience por ejecutar Ad Hoc `SELECT` para explorar datos sin procesar en el lago de datos. Esto permite realizar análisis de datos exploratorios sobre la marcha para experimentar y validar datos en los que los resultados de las consultas no se almacenan en el lago de datos.
1. **Utilización de consultas por lotes:** Utilice consultas por lotes para [crear trabajos programados](../../api/scheduled-queries.md#create-a-new-scheduled-query) para generar tablas agregadas de perspectivas, lo que garantiza un enfoque sistemático y automatizado del procesamiento de datos. Se ejecutan consultas por lotes `INSERT TABLE AS SELECT` y `CREATE TABLE AS SELECT` consultas para limpiar, dar forma, manipular y enriquecer datos. Los resultados de estas consultas se almacenan en el lago de datos.
1. **Carga de perspectivas agregadas:** Cargue las perspectivas agregadas generadas en el almacén acelerado y utilice SQL para probar consultas y garantizar la precisión y eficacia de la recuperación de datos. Para obtener información sobre cómo [realizar consultas sin estado en el almacén acelerado](../../api/accelerated-queries.md), consulte la documentación.
1. **Acceso e integración:** Acceda a las perspectivas almacenadas en la tienda acelerada sin problemas mediante la integración con Adobe Experience Platform [Paneles definidos por el usuario](../../../dashboards/user-defined-dashboards.md) u otras herramientas de Business Intelligence (BI) preferidas. Estas integraciones con clientes de terceros facilitan una experiencia coherente e intuitiva para los usuarios.

![Una infografía que ilustra los cuatro pasos para obtener perspectivas personalizables en Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Pasos siguientes

Al leer este documento, ahora comprende mejor los casos de uso, las capacidades esenciales y los pasos necesarios para desarrollar un panel de perspectivas personalizable con Data Distiller. Para continuar aprendiendo a crear modelos de datos de informes personalizados, consulte la [guía del modelo de datos de reporting insights](./reporting-insights-data-model.md).
