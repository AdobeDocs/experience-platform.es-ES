---
keywords: Experience Platform;introducción;ai del cliente;temas populares;entrada de ayuda del cliente;salida de ai del cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Entrada y salida en Customer AI
topic-legacy: Getting started
description: Obtenga más información sobre los eventos, entradas y salidas necesarios que utiliza Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 1%

---

# Entrada y salida en Customer AI

El siguiente documento describe los diferentes eventos, entradas y salidas necesarios que se utilizan en Customer AI.

## Primeros pasos

La AI del cliente funciona analizando uno de los siguientes conjuntos de datos para predecir puntuaciones de tendencia de pérdida o conversión:

- Conjunto de datos de Evento de experiencia del consumidor (CEE)
- Datos de Adobe Analytics que utilizan el [Conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Datos de Adobe Audience Manager que utilizan el [conector de origen del Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>Los conectores de origen tardan hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe verificar que el conjunto de datos tenga la longitud mínima de datos requerida para Customer AI. Revise la sección [datos históricos](#data-requirements) para verificar que tiene datos suficientes para el objetivo de predicción.

Este documento requiere una comprensión básica del esquema CEE. Consulte la documentación de [Intelligent Services data preparation](../data-preparation.md) antes de continuar.

La siguiente tabla describe algunos términos comunes utilizados en este documento:

| Término | Definición |
| --- | --- |
| [Modelo de datos de experiencia (XDM)](../../xdm/home.md) | XDM es el marco fundamental que permite a Adobe Experience Cloud, con tecnología de Adobe Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se basa el Experience Platform, el sistema XDM, operacionaliza los esquemas del Modelo de datos de experiencia para que los utilicen los servicios de plataforma. |
| Esquema XDM | Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase XDM base y de cero o más grupos de campos de esquema. |
| Clase XDM | Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos determinado. |
| [Grupos de campo](../../xdm/schema/composition.md) | Componente que define uno o más campos de un esquema. Los grupos de campos refuerzan la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en cada esquema en el que están incluidos. Los grupos de campos solo son compatibles con clases específicas, tal como se identifican con su atributo `meta:intendedToExtend`. |
| [Tipo de datos](../../xdm/schema/composition.md) | Componente que también puede proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes. Los tipos de datos descritos en este documento son compatibles con los esquemas CEE y Adobe Analytics. |
| Pérdida | Medición del porcentaje de cuentas que cancelan o deciden no renovar sus suscripciones. Una tasa de pérdida alta puede afectar negativamente a los ingresos mensuales recurrentes (MRR) y también puede indicar insatisfacción con un producto o servicio. |
| [Perfil del cliente en tiempo real](../../profile/home.md) | El perfil del cliente en tiempo real proporciona un perfil de cliente centralizado para la administración de experiencias personalizadas y con un público objetivo. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que involucran al individuo que han tenido lugar en cualquiera de los sistemas que utiliza con el Experience Platform. |

## Datos de entrada de Customer AI

>[!TIP]
>
> La AI del cliente determina automáticamente qué eventos son útiles para las predicciones y genera una advertencia si los datos disponibles no son suficientes para generar predicciones de calidad.

Customer AI admite conjuntos de datos de CEE, Adobe Analytics y Adobe Audience Manager. El esquema CEE requiere que agregue grupos de campos durante el proceso de creación del esquema. Si utiliza conjuntos de datos de Adobe Analytics o Adobe Audience Manager, el conector de origen asigna directamente los eventos estándar (comercio, detalles de páginas web, aplicación y búsqueda) que se enumeran a continuación durante el proceso de conexión.

Para obtener más información sobre la asignación de datos de Adobe Analytics o datos de Audience Manager, consulte la guía [Analytics field mappings](../../sources/connectors/adobe-applications/analytics.md) o [Audience Manager field mappings](../../sources/connectors/adobe-applications/mapping/audience-manager.md) .

### Eventos estándar utilizados por Customer AI {#standard-events}

Los eventos de experiencia XDM se utilizan para determinar distintos comportamientos de los clientes. Según la estructura de sus datos, es posible que los tipos de eventos enumerados a continuación no abarquen todos los comportamientos de sus clientes. Depende de usted determinar qué campos tienen los datos necesarios que son necesarios para identificar clara e inequívocamente la actividad del usuario web. Según el objetivo de la predicción, los campos necesarios pueden cambiar.

La Customer AI se basa en diferentes tipos de eventos para crear funciones de modelo. Estos tipos de eventos se añaden automáticamente al esquema mediante varios grupos de campos XDM.

>[!NOTE]
>
>Si utiliza datos de Adobe Analytics o Adobe Audience Manager, el esquema se crea automáticamente con los eventos estándar necesarios para capturar los datos. Si está creando su propio esquema CEE personalizado para capturar datos, debe tener en cuenta qué grupos de campos son necesarios para capturar los datos.

No es necesario tener datos para cada uno de los eventos estándar enumerados a continuación, pero ciertos eventos son necesarios para determinados escenarios. Si tiene alguno de los datos de eventos estándar disponibles, se recomienda incluirlos en el esquema. Por ejemplo, si desea crear una aplicación de Customer AI para predecir eventos de compra, sería útil tener datos de los tipos de datos `Commerce` y `Web page details`.

Para ver un grupo de campos en la interfaz de usuario de Platform, seleccione la pestaña **[!UICONTROL Schemas]** en el carril izquierdo seguido de la pestaña **[!UICONTROL Field groups]** .

| Grupo de campos | Tipo de evento | Ruta de campo XDM |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | pedido | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | cierres de compra | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | compras | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | búsqueda | search.keywords |

Además, Customer AI puede utilizar los datos de suscripción para crear modelos de mejor reproducción. Se necesitan datos de suscripción para cada perfil que utiliza el formato de tipo de datos [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) . La mayoría de los campos son opcionales, sin embargo, para un modelo de pérdida óptimo es muy recomendable proporcionar datos para tantos campos como sea posible, como `startDate`, `endDate` y cualquier otro detalle relevante.

### Datos históricos {#data-requirements}

Customer AI requiere datos históricos para la formación de modelos, pero la cantidad de datos necesaria se basa en dos elementos clave: ventana de resultados y población elegible.

De forma predeterminada, Customer AI busca un usuario que haya tenido actividad en los últimos 120 días si no se proporciona ninguna definición de población apta durante la configuración de la aplicación. Además, Customer AI requiere un mínimo de 500 eventos calificativos y 500 eventos no calificativos (un total de 1000) de datos históricos basados en una definición de objetivo predicha.

Los siguientes ejemplos proporcionados utilizan una fórmula sencilla para ayudarle a determinar la cantidad mínima de datos necesaria. Si tiene más del requisito mínimo, es probable que el modelo proporcione resultados más precisos. Si tiene menos de la cantidad mínima requerida, el modelo fallará ya que no hay una cantidad suficiente de datos para la formación del modelo.

**Fórmula**:

Longitud mínima de los datos requeridos = población elegible + ventana de resultados

>[!NOTE]
>
> 30 es el número mínimo de días necesarios para la población elegible. Si no se proporciona, el valor predeterminado es 120 días.

Ejemplos :

- Desea predecir si es probable que un cliente compre un reloj en los próximos 30 días. También desea puntuar a los usuarios que tienen alguna actividad web en los últimos 60 días. En este caso, la longitud mínima de los datos requerida = 60 días + 30 días. La población elegible es de 60 días y el período de espera es de 30 días, con un total de 90 días.

- Desea predecir si es probable que el usuario compre un reloj en los próximos 7 días. En este caso, la longitud mínima de los datos requerida = 120 días + 7 días. La población elegible tiene un valor predeterminado de 120 días y la ventana de resultados es de 7 días, con un total de 127 días.

- Desea predecir si es probable que el cliente compre un reloj en los próximos 7 días. También desea puntuar a los usuarios que tienen alguna actividad web en los últimos 7 días. En este caso, la longitud mínima de los datos requerida = 30 días + 7 días. La población elegible requiere un mínimo de 30 días y la ventana de resultados es de 7 días, con un total de 37 días.

Además de los datos mínimos requeridos, la Customer AI también funciona mejor con los datos recientes. En este caso de uso, Customer AI está realizando una predicción para el futuro en función de los datos de comportamiento recientes de un usuario. En otras palabras, es probable que los datos más recientes proporcionen una predicción más precisa.

### Situaciones de ejemplo

En esta sección, se describen diferentes escenarios para instancias de Customer AI, así como los tipos de evento requeridos y recomendados. Consulte la [tabla de eventos estándar](#standard-events) anterior para obtener más información sobre el grupo de campos y su ruta de campo.

>[!NOTE]
>
> Los tipos de evento requeridos se utilizan para identificar de forma clara e inequívoca la actividad del usuario web. El número de tipos de evento requeridos cambiará según el objetivo de predicción y la estructura del esquema. Si no está seguro de que se necesite un tipo de evento determinado, se recomienda incluir ese tipo de evento al crear el esquema CEE. Si utiliza datos de Adobe Analytics o Adobe Audience Manager, los eventos estándar necesarios deberían estar disponibles en función de los datos que transmita.

### Escenario 1: Conversión de compra en un sitio web de comercio electrónico minorista

**Objetivo de predicción:** prediga la tendencia de conversión para que los perfiles elegibles compren cierto artículo de ropa en un sitio web.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- pedido
- cierres de compra
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 2: Conversión de suscripción en un sitio web de servicio de flujo continuo de medios

**Objetivo de predicción:** prediga la tendencia de conversión de suscripción para que los perfiles aptos se comprometan a un cierto nivel de suscripción, como un plan estándar o premium.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- pedido
- cierres de compra
- compras
- webVisit
- búsqueda

En este ejemplo, `order`, `checkouts` y `purchases` se utilizan para indicar que se compró una suscripción y su tipo.

Además, para un modelo preciso, se recomienda utilizar algunas de las propiedades disponibles en el [tipo de datos de suscripción](../../xdm/data-types/subscription.md).

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 3: Pérdida en un sitio web de comercio electrónico minorista

**Objetivo de predicción:** prediga la probabilidad de que no se produzca un evento de compra.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- pedido
- cierres de compra
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 4: Mejore la conversión en un sitio web de comercio electrónico minorista

**Objetivo de predicción:** prediga la tendencia de compra de la población que ha comprado un producto específico para adquirir un nuevo producto relacionado.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- pedido
- cierres de compra
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 5: Cancelación de suscripción (cancelación) en un medio de noticias en línea

**Objetivo de predicción:** prediga la propensión de la población elegible a cancelar la suscripción de un servicio el mes que viene.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- webVisit
- búsqueda

Además, para un modelo preciso, se recomienda utilizar algunas de las propiedades disponibles en el [tipo de datos de suscripción](../../xdm/data-types/subscription.md).

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 6: Iniciar aplicación móvil

**Objetivo de predicción:** prediga la propensión de perfiles elegibles a iniciar una aplicación móvil de pago en los X días siguientes. Esto es similar a la predicción del indicador de rendimiento clave (KPI) de &quot;Usuarios activos mensuales&quot;.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de Customer AI con este objetivo de predicción en particular. Es posible excluir un evento requerido en función del objetivo de la predicción, sin embargo, si se excluyen varios eventos, los resultados pueden ser deficientes.

- pedido
- cierres de compra
- compras
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

En este ejemplo, `order`, `checkouts` y `purchases` se utilizan cuando es necesario adquirir una aplicación móvil.

**Tipos de eventos estándar adicionales:**

Es posible que se requiera cualquiera de los [tipos de evento](#standard-events) restantes en función de la complejidad de su objetivo y población elegible al configurar la instancia de Customer AI. Se recomienda que, si los datos están disponibles para un tipo de datos determinado, se incluyan en el esquema.

### Escenario 7: Características realizadas (Adobe Audience Manager)

**Objetivo de predicción:** prediga la propensión a que se realicen algunos rasgos.

**Tipos de eventos estándar requeridos:**

Para utilizar los rasgos de Adobe Audience Manager, debe crear una conexión de origen utilizando el [conector de origen del Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). El conector de origen crea automáticamente el esquema con los grupos de campos adecuados. No es necesario añadir manualmente tipos de eventos adicionales para que el esquema funcione con Customer AI.

Al configurar una nueva instancia de IA de cliente, `audienceName` y `audienceID` se pueden usar para seleccionar un rasgo en particular para la puntuación al definir el objetivo.

## Datos de salida de Customer AI

La AI del cliente genera varios atributos para perfiles individuales que se consideran aptos. Existen dos formas de utilizar la puntuación (salida) en función de lo que haya aprovisionado. Si tiene un conjunto de datos habilitado para Perfil del cliente en tiempo real, puede consumir perspectivas de Perfil del cliente en tiempo real en el [Generador de segmentos](../../segmentation/ui/segment-builder.md). Si no tiene un conjunto de datos habilitado para Perfil, puede [descargar el conjunto de datos de salida de Customer AI](./user-guide/download-scores.md) disponible en el lago de datos.

>[!NOTE]
>
> El perfil del cliente en tiempo real consume los valores de salida, que se pueden utilizar para crear y definir segmentos.

La tabla siguiente describe los distintos atributos que se encuentran en la salida de Customer AI:

| Atributo | Descripción |
| ----- | ----------- |
| Puntuación | La probabilidad relativa de que un cliente logre el objetivo predicho dentro del lapso de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino como la probabilidad de un individuo en comparación con la población total. Esta puntuación va del 0 al 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil de alcanzar el objetivo predicho dentro del lapso de tiempo definido. Al comparar resultados entre objetivos diferentes, se recomienda tener en cuenta la probabilidad sobre el percentil o la puntuación. La probabilidad siempre debe utilizarse al determinar la probabilidad promedio entre la población elegible, ya que la probabilidad tiende a estar en el lado inferior para los eventos que no ocurren con frecuencia. Los valores para el rango de probabilidad están entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles de puntuación similar. Por ejemplo, un perfil con una clasificación de percentil de 99 para la pérdida indica que tiene un mayor riesgo de pérdida en comparación con el 99% de todos los demás perfiles que se clasificaron. Los percentiles varían de 1 a 100. |
| Tipo de propensión | El tipo de tendencia seleccionado. |
| Fecha de puntuación | Fecha en la que se produjo la puntuación. |
| Factores influyentes | Motivos predichos sobre por qué es probable que un perfil se convierta o produzca. Los factores se componen de los siguientes atributos:<ul><li>Código: El perfil o atributo de comportamiento que influye positivamente en la puntuación predicha de un perfil. </li><li>Valor: El valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o atributo de comportamiento que tiene en la puntuación predicha (baja, media, alta)</li></ul> |

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya establecido todas sus credenciales y esquemas, comience por seguir la guía [Configure a Customer AI Instance](./user-guide/configure.md). Esta guía lo acompaña durante la creación de una instancia para Customer AI.
