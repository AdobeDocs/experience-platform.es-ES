---
keywords: Experience Platform;introducción;inteligencia artificial aplicada al cliente;temas populares;entrada de inteligencia artificial aplicada al cliente;salida de inteligencia artificial aplicada al cliente; requisitos de datos
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Requisitos de datos en Customer AI
topic-legacy: Getting started
description: Obtenga más información acerca de los eventos, las entradas y los resultados necesarios que utiliza la inteligencia artificial aplicada al cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 1%

---


# Entrada y salida en Customer AI

En el siguiente documento se describen los diferentes eventos, entradas y resultados necesarios que se utilizan en la inteligencia artificial aplicada al cliente.

## Introducción {#getting-started}

Estos son los pasos para crear modelos de tendencia e identificar audiencias objetivo para el marketing personalizado en la inteligencia artificial aplicada al cliente:

1. Describir casos de uso: ¿cómo ayudarían los modelos de tendencia a identificar audiencias de destino para el marketing personalizado? ¿Cuáles son mis objetivos comerciales y las tácticas correspondientes para lograr el objetivo? ¿Dónde puede encajar el modelado de tendencia en este proceso?

2. Priorizar casos de uso: ¿cuáles son las prioridades más altas para la empresa?

3. Generar modelos en la inteligencia artificial aplicada al cliente: vea este [tutorial rápido](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=es) y consulte nuestra [guía de interfaz de usuario](../customer-ai/user-guide/configure.md) para obtener un proceso paso a paso con el fin de crear un modelo.

4. [Generar segmentos](../customer-ai/user-guide/create-segment.md) utilizando los resultados del modelo.

5. Realice acciones comerciales dirigidas en función de estos segmentos. Monitorice los resultados e itere las acciones para mejorar.

Estas son algunas configuraciones de ejemplo para su primer modelo.  El modelo de ejemplo, creado en este documento, utiliza un modelo de inteligencia artificial aplicada al cliente para predecir quién tiene probabilidades de realizar la conversión para un negocio minorista en los próximos 30 días. El conjunto de datos de entrada es un conjunto de datos Adobe Analytics.

| Paso | Definición | Ejemplo |
| ---- | ------ | ------- |
| Configurar | Especifique información básica sobre el modelo. | **Nombre**: modelo de tendencia de compra en lápiz <br> **Tipo de modelo**: Conversión |
| Seleccionar datos | Especifique los conjuntos de datos utilizados para crear el modelo. | **Conjunto de datos**: conjunto de datos de Adobe Analytics <br> **Identidad**: Asegúrese de que la columna de identidad de cada conjunto de datos esté configurada para ser una identidad común. |
| Definir meta | Defina el objetivo, la población elegible, los eventos personalizados y los atributos del perfil. | **Objetivo de predicción**: Seleccione `commerce.purchases.value` igual a lápiz <br> **Ventana de resultados**: 30 días. |
| Definir opciones | Configure la programación para la actualización del modelo y habilite las puntuaciones para el perfil | **Horario**: Semanalmente <br> **Habilitar para el perfil**: debe habilitarse para que la salida del modelo se utilice en la segmentación. |

## Resumen de datos {#data-overview}

En las siguientes secciones se describen los diferentes eventos, entradas y resultados necesarios que se utilizan en la inteligencia artificial aplicada al cliente.

La inteligencia artificial aplicada al cliente funciona analizando los siguientes conjuntos de datos para predecir la pérdida (cuando es probable que un cliente deje de usar el producto) o la conversión (cuando es probable que un cliente realice una compra) puntuaciones de tendencia:

- Datos de Adobe Analytics que usan el [conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Datos de Adobe Audience Manager que usan el [conector de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Conjunto de datos de evento de experiencia](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Conjunto de datos de evento de experiencia del consumidor](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

Puede agregar varios conjuntos de datos de diferentes fuentes si cada uno de los conjuntos de datos comparte el mismo tipo de identidad (área de nombres), como un ECID. Para obtener más información sobre cómo agregar varios conjuntos de datos, visite la [Guía del usuario de inteligencia artificial aplicada al cliente](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Los conectores de Source tardan hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe verificar que el conjunto de datos tenga la longitud mínima de datos necesaria para la inteligencia artificial aplicada al cliente. Revise la sección [datos históricos](#data-requirements) para verificar que tiene suficientes datos para el objetivo de predicción.

En la tabla siguiente se describen algunos términos comunes utilizados en este documento:

| Término | Definición |
| --- | --- |
| [Modelo de datos de experiencia (XDM)](../../xdm/home.md) | XDM es el marco de trabajo básico que permite a Adobe Experience Cloud, con tecnología Adobe Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. Experience Platform utiliza el sistema XDM para organizar los datos de una manera determinada que facilite su uso para los servicios de Experience Platform. |
| [Esquema XDM](../../xdm/schema/composition.md) | Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. Antes de poder introducir los datos en Experience Platform, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase XDM base y cero o más grupos de campos de esquema. |
| [clase XDM](../../xdm/schema/field-constraints.md) | Todos los esquemas XDM describen datos que se pueden categorizar como `Experience Event`. El comportamiento de datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el número más pequeño de propiedades que debe contener un esquema para representar un comportamiento de datos determinado. |
| [Grupos de campo](../../xdm/schema/composition.md) | Componente que define uno o varios campos de un esquema. Los grupos de campos aplican la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en todos los esquemas en los que se incluyen. Los grupos de campos solo son compatibles con clases específicas, identificadas por su atributo `meta:intendedToExtend`. |
| [Tipo de datos](../../xdm/schema/composition.md) | Componente que también puede proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes. Los tipos de datos descritos en este documento son compatibles con los esquemas CEE y Adobe Analytics. |
| [Perfil del cliente en tiempo real](../../profile/home.md) | El Perfil del cliente en tiempo real proporciona un perfil de consumidor centralizado para la administración de experiencias personalizada y dirigida. Cada perfil contiene datos agregados de todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que involucran a personas que han tenido lugar en cualquiera de los sistemas que utiliza con Experience Platform. |

## Datos de entrada de Customer AI {#customer-ai-input-data}

Para conjuntos de datos de entrada, como Adobe Analytics y Adobe Audience Manager, los respectivos conectores de origen asignan directamente los eventos en estos grupos de campos estándar (Commerce, Web, Aplicación y Búsqueda) de forma predeterminada durante el proceso de conexión. La siguiente tabla muestra los campos de evento de los grupos de campos estándar predeterminados para la inteligencia artificial aplicada al cliente.

Para obtener más información sobre la asignación de datos de Adobe Analytics o de Audience Manager, visite las asignaciones de campos de Analytics o la guía de asignaciones de campos de [Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Puede utilizar esquemas XDM de evento de experiencia o de evento de experiencia del consumidor para conjuntos de datos de entrada que no se rellenen a través de uno de los conectores anteriores. Se pueden agregar grupos de campos XDM adicionales durante el proceso de creación del esquema. Adobe puede proporcionar los grupos de campos, como los grupos de campos estándar o un grupo de campos personalizados, que coincide con la representación de datos en Experience Platform.

>[!IMPORTANT]
>
>Debe asegurarse de que los datos se rellenen en estos conjuntos de datos de entrada. Si no se encuentran eventos de grupos de campos estándar en los conjuntos de datos de entrada, debe agregar eventos personalizados durante el flujo de trabajo de configuración. Consulte los detalles sobre los eventos personalizados.

### Grupos de campos estándar utilizados por Customer AI {#standard-events}

Los eventos de experiencia se utilizan para determinar varios comportamientos de cliente. Según la estructura de los datos, es posible que los tipos de evento enumerados a continuación no abarquen todos los comportamientos del cliente. Depende de usted determinar qué campos tienen los datos necesarios para identificar de forma clara e inequívoca la actividad del usuario web o de otro canal específico. Según el objetivo de predicción, los campos obligatorios que se necesitan pueden cambiar.

>[!NOTE]
>
>Si utiliza datos de Adobe Analytics o Adobe Audience Manager, el esquema se crea automáticamente con los eventos estándar necesarios para capturar los datos. Si está creando su propio esquema EE personalizado para capturar datos, debe tener en cuenta qué grupos de campos son necesarios para capturar los datos.

La inteligencia artificial aplicada al cliente utiliza los eventos en estos cuatro grupos de campos estándar de forma predeterminada: Commerce, Web, Aplicación y Búsqueda. No es necesario tener datos para cada evento en los grupos de campos estándar enumerados a continuación, pero se requieren ciertos eventos para ciertos escenarios. Si tiene disponibles eventos en los grupos de campos estándar, se recomienda incluirlos en el esquema. Por ejemplo, si desea crear un modelo de inteligencia artificial aplicada al cliente para predecir eventos de compra, resulta útil tener datos de los grupos de campos Commerce y Detalles de página web.

Para ver un grupo de campos en la interfaz de usuario de Experience Platform, seleccione la pestaña **[!UICONTROL Esquemas]** en el carril izquierdo, seguida de la pestaña **[!UICONTROL Grupos de campos]**.

| Grupo de campo | Tipo de evento | Ruta de campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalles de Commerce] | pedido | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | cierres | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | compras | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Detalles web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Detalles de la aplicación] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpupgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Detalles de búsqueda] | buscar | `search.keywords` |

Además, la inteligencia artificial aplicada al cliente puede utilizar los datos de suscripción para crear mejores modelos de pérdida. Se necesitan datos de suscripción para cada perfil que use el formato de tipo de datos [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md). La mayoría de los campos son opcionales; sin embargo, para lograr un modelo de pérdida óptimo, se recomienda que proporcione datos para tantos campos como sea posible, como `startDate`, `endDate` y cualquier otro detalle relevante. Póngase en contacto con el equipo de su cuenta para obtener soporte adicional sobre esta función.

### Añadir eventos personalizados y atributos de perfil {#add-custom-events}

Si tiene información que desea incluir además de los [campos de evento estándar](#standard-events) predeterminados que usa la inteligencia artificial aplicada al cliente, puede usar la [configuración de evento personalizada](./user-guide/configure.md#custom-events) para aumentar los datos que usa el modelo.

#### Cuándo utilizar eventos personalizados

Los eventos personalizados son necesarios cuando los conjuntos de datos elegidos en el paso de selección de conjuntos de datos contienen *none* de los campos de evento predeterminados utilizados por la inteligencia artificial aplicada al cliente. La inteligencia artificial aplicada al cliente necesita información sobre al menos un evento de comportamiento del usuario que no sea el resultado.

Los eventos personalizados son útiles para lo siguiente:

- Incorporar conocimientos de dominio o experiencia previa en el modelo.

- Mejora de la calidad del modelo predictivo.

- Obtención de información e interpretaciones adicionales.

Los mejores candidatos para los eventos personalizados son los datos que contienen conocimientos de dominio que pueden ser predictivos del resultado. Algunos ejemplos generales de eventos personalizados son:

- Registrarse para obtener cuenta

- Suscribirse a la Newsletter

- Realizar una llamada al servicio de atención al cliente

A continuación se muestra una selección de ejemplos de eventos personalizados específicos del sector:

| Industria | Eventos personalizados |
| --- | --- |
| Comercial | Transacción en la tienda<br>Suscríbete a la tarjeta del club<br>Cupón móvil de clip. |
| Entretenimiento | Suscripción a la temporada de compra <br> Transmitir vídeo. |
| Hospitalidad | Haga una reserva en el restaurante <br>. Compre puntos de fidelidad. |
| Viajes | Añadir información conocida del viajero Compra millas. |
| Comunicaciones | Plan de actualización/reducción/cancelación. |

Los eventos personalizados deben representar acciones iniciadas por el usuario para poder seleccionarse. Por ejemplo, &quot;Envío de correo electrónico&quot; es una acción iniciada por un experto en marketing y no por el usuario, por lo que no debe utilizarse como evento personalizado.

### Datos históricos

La inteligencia artificial aplicada al cliente requiere datos históricos para la formación de modelos. La duración necesaria para que los datos existan dentro del sistema está determinada por dos elementos clave: la ventana de resultados y la población elegible.

De forma predeterminada, la inteligencia artificial aplicada al cliente busca un usuario que haya tenido actividad en los últimos 45 días si no se proporciona ninguna definición de población apta durante la configuración de la aplicación. Además, la inteligencia artificial aplicada al cliente requiere un mínimo de 500 eventos clasificatorios y 500 no clasificatorios (1000 en total) a partir de datos históricos basados en una definición de objetivo predicha.

Los siguientes ejemplos muestran el uso de una fórmula simple que ayuda a determinar la cantidad mínima de datos necesaria. Si tiene más datos que el requisito mínimo, es probable que el modelo proporcione resultados más precisos. Si tiene menos de la cantidad mínima requerida, el modelo fallará, ya que no hay suficientes datos para la formación del modelo.

La inteligencia artificial aplicada al cliente emplea un modelo de supervivencia para estimar la probabilidad de que un evento se produzca en un momento determinado e identificar los factores que influyen, junto con el aprendizaje supervisado que define las poblaciones positivas y negativas y árboles basados en decisiones como `lightgbm` para generar una puntuación de probabilidad.

**fórmula**:

Para decidir la duración mínima requerida de los datos existentes en el sistema:

- El mínimo de datos necesario para crear funciones es de 30 días. Comparar la ventana retrospectiva de idoneidad con 30 días:

   - Si la ventana retrospectiva de idoneidad es mayor de 30 días, la necesidad de datos = ventana retrospectiva de idoneidad + ventana de resultado.

   - De lo contrario, el requisito de datos = 30 días + ventana de resultado.

** Si hay más de una condición para definir la población elegible, la ventana retrospectiva de idoneidad es la más larga.

>[!NOTE]
>
>30 es el número mínimo de días requeridos para la población elegible. Si no se proporciona, el valor predeterminado es de 45 días.

**Ejemplos**:

- Desea predecir si es probable que un cliente compre un reloj en los próximos 30 días para aquellos que hayan realizado alguna actividad en la web en los últimos 60 días.

   - Ventana retrospectiva de idoneidad = 60 días

   - Ventana de resultado = 30 días

   - Datos necesarios = 60 días + 30 días = 90 días

- Desea predecir si es probable que el usuario compre un reloj en los próximos 7 días **sin** que proporcione una población elegible explícita. En este caso, la población elegible toma como valor predeterminado &quot;aquellos que han tenido actividad en los últimos 45 días&quot; y la ventana de resultado es de 7 días.

   - Ventana retrospectiva de idoneidad = 45 días

   - Ventana de resultado = 7 días

   - Datos necesarios = 45 días + 7 días = 52 días

- Desea predecir si es probable que el cliente compre un reloj en los próximos 7 días para aquellos que hayan realizado alguna actividad en la web en los últimos 7 días.

   - Ventana retrospectiva de idoneidad = 7 días

   - Datos mínimos necesarios para crear funciones = 30 días

   - Ventana de resultado = 7 días

   - Datos necesarios = 30 días + 7 días = 37 días

Aunque la inteligencia artificial aplicada al cliente requiere un período mínimo de tiempo para que los datos existan en el sistema, también funciona mejor con datos recientes. Al utilizar datos de comportamiento más recientes, es probable que la inteligencia artificial aplicada al cliente genere una predicción más precisa del comportamiento futuro de un usuario.

## Datos de salida de Customer AI {#customer-ai-output-data}

La inteligencia artificial aplicada al cliente genera varios atributos para perfiles individuales que se consideran aptos. Existen dos maneras de consumir la puntuación (salida) en función de lo que haya aprovisionado. Si tiene un conjunto de datos habilitado para el Perfil del cliente en tiempo real, puede consumir datos del Perfil del cliente en tiempo real en [Generador de segmentos](../../segmentation/ui/segment-builder.md). Si no tiene un conjunto de datos con perfil habilitado, puede [descargar el conjunto de datos de salida de inteligencia artificial aplicada al cliente](./user-guide/download-scores.md) disponible en el lago de datos.

Puede encontrar el conjunto de datos de salida en el área de trabajo **Conjuntos de datos** de Experience Platform. Todos los conjuntos de datos de salida de inteligencia artificial aplicada al cliente comienzan con el nombre **Puntuaciones de inteligencia artificial aplicada al cliente - NAME_OF_APP**. Del mismo modo, todos los esquemas de salida de inteligencia artificial aplicada al cliente comienzan con el nombre **Esquema de inteligencia artificial aplicada al cliente - Name_of_app**.

![Convenciones de nomenclatura para conjuntos de datos de salida en inteligencia artificial aplicada al cliente.](./images/user-guide/cai-schema-name-of-app.png)

La siguiente tabla describe los distintos atributos que se encuentran en la salida de la inteligencia artificial aplicada al cliente:

| Atributo | Descripción |
| ----- | ----------- |
| [!UICONTROL Puntuación] | La probabilidad relativa de que un cliente alcance el objetivo predicho dentro del lapso de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino más bien como la probabilidad de un individuo en comparación con la población general. Esta puntuación va del 0 al 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil para lograr el objetivo predicho dentro del lapso de tiempo definido. Cuando se comparan resultados entre diferentes objetivos, se recomienda considerar la probabilidad por encima del percentil o la puntuación. La probabilidad siempre se debe utilizar al determinar la probabilidad promedio en toda la población elegible, ya que la probabilidad tiende a estar en el lado inferior para los eventos que no ocurren con frecuencia. Los valores del rango de probabilidad están entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles con puntuaciones similares. Por ejemplo, un perfil con una clasificación de percentil de 99 para la pérdida indica que tiene un mayor riesgo de pérdida en comparación con el 99 % de todos los demás perfiles marcados. Los percentiles van del 1 al 100. |
| Tipo de tendencia | El tipo de tendencia seleccionado. |
| Fecha de puntuación | La fecha en la que se produjo la puntuación. |
| Factores influyentes | Estas son las razones previstas por las que un perfil es probable que se convierta o se pierda. Estos factores están compuestos por los siguientes atributos:<ul><li>Código: el perfil o atributo de comportamiento que influye positivamente en la puntuación prevista de un perfil. </li><li>Valor: Valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o atributo de comportamiento en la puntuación predicha (baja, media, alta)</li></ul> |

## Pasos siguientes {#next-steps}

Una vez que prepare los datos y se asegure de que todas sus credenciales y esquemas están en su lugar, consulte la guía [Configurar una instancia de inteligencia artificial aplicada al cliente](./user-guide/configure.md), que le guiará por un tutorial paso a paso para crear una instancia de inteligencia artificial aplicada al cliente.